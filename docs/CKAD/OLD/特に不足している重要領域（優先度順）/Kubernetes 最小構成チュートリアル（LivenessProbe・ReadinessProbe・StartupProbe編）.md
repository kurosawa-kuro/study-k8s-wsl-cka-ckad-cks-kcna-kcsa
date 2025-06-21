以下に『LivenessProbe・ReadinessProbe・StartupProbe』を理解するための最小構成チュートリアルを作成しました。

## 📌 Kubernetes 最小構成チュートリアル（LivenessProbe・ReadinessProbe・StartupProbe編）

### 🚩 目的

KubernetesのPodライフサイクル管理で重要な以下3つのプローブをシンプルなPod構成で実践します。

- **StartupProbe**（起動確認）
    
- **ReadinessProbe**（稼働準備確認）
    
- **LivenessProbe**（正常稼働確認）
    

---

## 🛠️ 前提条件

- kindクラスタ構築済み
    
- kubectlセットアップ済み
    

### 📂 作業ディレクトリ準備

```bash
mkdir -p ~/dev/k8s-probe-sample && cd ~/dev/k8s-probe-sample
```

---

## 📌 マニフェスト作成（pod-probes.yaml）

シンプルなNginxコンテナで各プローブを設定します。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: probe-example
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80

      # 起動までに時間がかかる場合に使用（例：初回起動は最大30秒待機）
      startupProbe:
        httpGet:
          path: /
          port: 80
        failureThreshold: 30
        periodSeconds: 1

      # コンテナがリクエストを処理できるか確認（稼働準備確認）
      readinessProbe:
        httpGet:
          path: /
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 5
        successThreshold: 1
        failureThreshold: 3

      # コンテナが稼働中に問題ないか確認（問題がある場合、コンテナ再起動）
      livenessProbe:
        httpGet:
          path: /
          port: 80
        initialDelaySeconds: 15
        periodSeconds: 20
        failureThreshold: 3
```

---

## 🚀 マニフェスト適用

```bash
kubectl apply -f pod-probes.yaml
```

---

## 🧪 動作確認

### Podの状態確認

```bash
kubectl describe pod probe-example
```

プローブの各種ステータスが確認できます：

- **StartupProbe**：起動時にPodがHTTPレスポンスを返すまで最大30秒間、毎秒リトライ。
    
- **ReadinessProbe**：起動後5秒後からHTTPレスポンスを5秒間隔でチェック。成功するとService経由の通信対象に追加されます。
    
- **LivenessProbe**：起動後15秒後から20秒ごとにHTTPレスポンスをチェック。3回連続で失敗するとPodを再起動します。
    

---

## 🚨 障害時挙動の確認（LivenessProbe検証）

あえてPod内で障害を発生させ、LivenessProbeが動作するか確認します。

```bash
kubectl exec -it probe-example -- sh
```

コンテナ内で以下を実行し、Nginxを停止します。

```bash
# Nginx停止（異常状態を再現）
nginx -s stop
```

### Pod再起動を確認

外部でPodをモニタリングします。

```bash
kubectl get pods -w
```

約1分後にLivenessProbeが異常検知し、Podが再起動することを確認できます。

---

## 🧹 クリーンアップ

```bash
kubectl delete -f pod-probes.yaml
```

---

## ✅ 完了 🎉

これでLivenessProbe、ReadinessProbe、StartupProbeの基本動作をシンプルな構成で実践的に理解しました。  
実際の運用ではこれらのプローブを適切に設定し、堅牢なアプリケーション運用を目指しましょう。

`ReadinessProbe` と `LivenessProbe` の違いは次のように整理できます。

---

## 🔍 ReadinessProbe（準備完了確認）

- **目的：**
    
    - Podのアプリケーションが**リクエストを受け付けられる状態にあるか**を判断する。
        
    - ReadinessProbeが成功した後に、ServiceなどからのトラフィックがPodにルーティングされる。
        
- **失敗すると：**
    
    - Podは再起動されない。
        
    - **一時的にServiceから除外される。**
        
        - つまり、外部リクエストが来なくなる。
            
- **ユースケースの例：**
    
    - 起動後にDB接続やキャッシュの準備に時間がかかるアプリケーションで、準備が整ったあとにのみトラフィックを受け入れるようにする場合など。
        

---

## 🔍 LivenessProbe（正常稼働確認）

- **目的：**
    
    - Pod内のコンテナが稼働中、**正常な状態を維持しているか**を監視。
        
    - 稼働中に問題があった場合に自動でコンテナを再起動し、自己回復を試みる。
        
- **失敗すると：**
    
    - **コンテナが再起動される。**
        
    - 継続的に異常がある場合、再起動が繰り返される可能性がある。
        
- **ユースケースの例：**
    
    - 予期しないエラーやアプリケーションの異常終了を検知して、自動で復旧を行いたい場合。
        

---

## 📝 具体的な違いの整理

|項目|ReadinessProbe|LivenessProbe|
|---|---|---|
|チェック目的|トラフィックを受け入れ可能か？|稼働が正常に維持されているか？|
|チェック失敗時の動作|Serviceからのトラフィック除外のみ|コンテナの再起動|
|チェックの頻度|短め（数秒〜数十秒程度）|長め（数十秒〜数分程度）|
|再起動|❌|✅|

---

## 🚩 実務での使い分けイメージ

- **起動直後、初期化処理が完全に終わるまでトラフィックを受けたくない場合 → `ReadinessProbe`**
    
    - 例：アプリ起動時にデータベースや外部サービスへの初期接続が完了してからリクエストを受ける場合。
        
- **稼働中に異常が発生したらコンテナを自動再起動したい場合 → `LivenessProbe`**
    
    - 例：メモリリーク、無応答状態、アプリケーションクラッシュを検知して回復したい場合。
        

---

このように、**ReadinessProbeは「外部リクエストの受入れ管理」、LivenessProbeは「自己回復のための再起動」に利用されるもの**と区別して覚えるとわかりやすいでしょう。