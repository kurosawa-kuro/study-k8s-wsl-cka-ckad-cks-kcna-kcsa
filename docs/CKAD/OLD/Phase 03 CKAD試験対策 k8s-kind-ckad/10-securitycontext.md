# 📘 CKAD合格対策チュートリアル

## 🚩 10. セキュリティコンテキストの設定（SecurityContext）

### 📌 目的

Podやコンテナのセキュリティを強化するため、SecurityContextを設定して特権を制限します。

### 📂 作業ディレクトリ

```bash
~/dev/k8s-kind-ckad/10-securitycontext
```

### 🚩 コンテナイメージ選定理由

**パブリック軽量イメージ（busybox）** を使用します。

- busyboxはシンプルで高速に起動し、ユーザー権限やセキュリティ設定確認に最適です。
    

### 🛠️ YAML作成手順（CKADスタイル）

1. **kubectl runで初期YAML生成**
    

```bash
kubectl run secure-pod --image=busybox --dry-run=client -o yaml -- sleep 3600 > secure-pod.yaml
```

2. **YAMLの修正箇所**
    

YAMLを以下のように修正します：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
  labels:
    app: secure-app  # 明確なラベルを設定
spec:
  securityContext:
    runAsUser: 1000         # 非rootユーザーでPod全体を実行
    fsGroup: 2000           # ファイルアクセスのグループ権限を設定
  containers:
  - name: secure-pod
    image: busybox
    command: ["sleep", "3600"]
    securityContext:
      runAsNonRoot: true                # rootとして実行しない
      readOnlyRootFilesystem: true      # ルートファイルシステムを読み取り専用に
      capabilities:
        drop: ["NET_RAW"]              # 特定のLinuxケーパビリティを無効化
```

### 🔍 動作確認手順

1. **Podの作成**
    

```bash
kubectl apply -f secure-pod.yaml
```

2. **Podの状態確認**
    

```bash
kubectl get pods
kubectl describe pod secure-pod
```

3. **コンテナ内でのユーザー確認**
    

```bash
kubectl exec secure-pod -- id
```

- 結果に`uid=1000`が表示されれば成功です。
    

4. **ルートファイルシステムの確認**
    

```bash
kubectl exec secure-pod -- touch /testfile
```

- 読み取り専用のエラーが出れば成功です。
    

### 🎯 CKAD試験ポイント再確認

- YAMLは`kubectl run`で初期作成し、最低限の変更で済ませます。
    
- `labels`と`securityContext`を明確に設定します。
    
- 必ずPodがRunningになっていることを確認します。
    
- コンテナ内でユーザーIDや権限の設定を検証します。
    
- 正確かつ迅速な作業がCKAD試験では重要です。
    

### 🌱 今後のチュートリアルへのつながり

この設定は次のチュートリアルとも関連し、セキュリティや構成管理をさらに深めます。

- マルチコンテナPod（サイドカーコンテナ）
    
- ConfigMap/Secretとの連携
    
- Service / Ingress
    
- NetworkPolicy
    

### 🏅 完成後のゴール

- CKAD試験でSecurityContextを迅速かつ正確に設定できる。
    
- Podのセキュリティ設定の基礎を習得し、実務でも即活用可能。