# 📘 CKAD試験対策チュートリアル: ログ管理とデバッグ

## ✅ 作業ディレクトリ

- `~/dev/k8s-kind-ckad/12-logs-exec-debug`
    

## ✅ 使用コンテナイメージ

- **選定イメージ**: Node.js Express API (AWS ECR)
    
- **理由**: 実際のHTTPリクエストログを確認可能なため、ログとデバッグ操作を現実的に体感できる。
    

| 項目       | 詳細                                                                                      |
| -------- | --------------------------------------------------------------------------------------- |
| イメージ     | `986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5`    |
| Gitリポジトリ | [container-nodejs-api-8000](https://github.com/kurosawa-kuro/container-nodejs-api-8000) |
| ポート      | 8000                                                                                    |

---

## ✅ YAML作成方法（CKAD試験スタイル）

既存のPodまたはDeploymentを利用（新規マニフェスト作成不要）。

---

## ✅ CKAD試験対策ポイント

- **ログ確認 (`kubectl logs`)**
    
- **コンテナ内操作 (`kubectl exec`)**
    
- **エフェメラルコンテナの追加 (`kubectl debug`)**
    

これらを迅速かつ正確に実行することが合格への鍵。

---

## 🚀 チュートリアル手順

### 📌 Podのログ確認

1. Podの名前を確認
    

```bash
kubectl get pods
```

2. ログ出力を確認
    

```bash
kubectl logs <Pod名>
```

3. HTTPリクエストを送信しログを確認
    

```bash
kubectl port-forward <Pod名> 8000:8000
curl http://localhost:8000/posts
kubectl logs <Pod名>
```

### 📌 コンテナ内でコマンド実行（exec）

```bash
kubectl exec -it <Pod名> -- /bin/sh
```

コンテナ内で以下の操作を試す:

- 環境変数確認 (`env`)
    
- ファイル確認 (`ls -l`)
    

### 📌 エフェメラルコンテナを使ったデバッグ

デバッグ用コンテナを追加:

```bash
kubectl debug -it <Pod名> --image=busybox --target=<既存コンテナ名>
```

エフェメラルコンテナ内で操作:

- curl, wgetでのHTTPレスポンス確認
    
- psでのプロセス確認
    

Podの状態を確認:

```bash
kubectl get pods <Pod名> -o yaml
```

`ephemeralContainers` セクションが表示されていることを確認。

---

## ✅ 重要ポイント再確認（CKAD試験観点）

- YAMLは既存マニフェストを活用し、新規作成は不要。
    
- Podのログとコンテナ内操作を迅速に行う。
    
- エフェメラルコンテナで迅速なデバッグ。
    

---

## ✅ 推奨環境

|項目|バージョン|
|---|---|
|OS|Ubuntu 22.04|
|kind|v0.23.0|
|kubectl|v1.29.x|
|Helm|v3.14.x|
|Docker|24.0+|
|AWS CLI|v2 (ECR認証用)|

---

## ✅ GitHubへのPush

```bash
cd ~/dev/k8s-kind-ckad
git add 12-logs-exec-debug
git commit -m "CKAD試験向けログ管理とデバッグチュートリアル"
git push origin main
```

---

## ✅ 今後の拡張への配慮

このチュートリアルは以下の高度なテーマへの基礎となります。

- マルチコンテナ（サイドカー）運用
    
- ConfigMap / Secretの動的更新
    
- Probe設定による自動復旧
    
- Service / Ingressによる外部公開
    
- NetworkPolicyの通信制御
    

---

## 🎯 チュートリアル達成ゴール

- CKAD試験のログ確認・デバッグ問題を迅速かつ正確に解決できる。
    
- Kubernetes環境下での実践的デバッグ手法を習得し、実務にも応用できる。
    

以上の手順で、効率よくCKAD試験合格に向けて必要なスキルを身につけてください。