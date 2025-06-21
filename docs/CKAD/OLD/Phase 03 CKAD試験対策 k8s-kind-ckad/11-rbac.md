# 📘 CKAD試験対策チュートリアル: ServiceAccountとRBACによる認可設定

## ✅ 作業ディレクトリ

```bash
~/dev/k8s-kind-ckad/11-rbac
```

## ✅ 使用イメージの選定

**推奨イメージ:** `bitnami/kubectl`

**理由:**

- Kubernetes APIとのやり取りや権限確認に特化した軽量で実務的なイメージです。
    
- コンテナ内で直接kubectlコマンドを実行でき、RBACの検証が容易に行えます。
    

## ✅ CKAD試験を意識したYAML作成方法

以下の手順で素早くYAMLを作成・修正します。

### 1. ServiceAccount 作成

```bash
kubectl create serviceaccount app-sa -o yaml --dry-run=client > serviceaccount.yaml
```

- **修正ポイント:** 必要に応じてlabelsを追加
    

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: app-sa
  labels:
    app: express-api
```

### 2. Role 作成

特定Namespace内でPodの`get`、`list`権限を持つRoleを作成します。

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  labels:
    app: express-api
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list"]
```

### 3. RoleBinding 作成

上記RoleをServiceAccountに紐付けます。

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  labels:
    app: express-api
subjects:
  - kind: ServiceAccount
    name: app-sa
    namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

### 4. Pod作成（kubectl createコマンド利用）

```bash
kubectl run rbac-test --image=bitnami/kubectl --dry-run=client -o yaml > pod.yaml
```

- **修正ポイント:** labels、serviceAccountNameを追加
    

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: rbac-test
  labels:
    app: express-api
spec:
  serviceAccountName: app-sa
  containers:
  - name: rbac-test
    image: bitnami/kubectl
    command: ["sleep", "3600"]
```

## ✅ 動作確認

Podをデプロイして動作確認します。

```bash
kubectl apply -f serviceaccount.yaml
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
kubectl apply -f pod.yaml
```

Podが正常に`Running`状態であることを確認します。

```bash
kubectl get pods
```

Pod内での権限をテストします。

```bash
kubectl exec -it rbac-test -- kubectl get pods  # 成功するはずです（許可された操作）
kubectl exec -it rbac-test -- kubectl delete pod rbac-test  # 失敗するはずです（許可されていない操作）
```

## ✅ CKAD試験ポイント再確認

- `kubectl create`を活用して素早くYAMLを生成すること
    
- 必須項目(labels, serviceAccountName)を明確に追加すること
    
- Podが正常に起動し権限が適用されていることを確認
    
- コンテナ内で実際の操作を行い、RBAC設定の検証を行うこと
    

## ✅ 使用環境

|項目|推奨バージョン例|
|---|---|
|OS|Ubuntu 22.04|
|kind|v0.23.0|
|kubectl|v1.29.x|
|Helm|v3.14.x|
|Docker|24.0+|
|AWS CLI|v2|

## ✅ GitHubへのPush

完成したYAMLファイルをPushします。

```bash
cd ~/dev/k8s-kind-ckad
git add 11-rbac
git commit -m "CKAD試験向けRBAC設定チュートリアル"
git push origin main
```

## ✅ 今後の拡張への配慮

今回のRBAC設定は以下の内容につながる基盤となります：

- マルチコンテナPod（SA権限分離）
    
- ConfigMap/Secretの権限管理
    
- NetworkPolicyによる通信制御と組み合わせた高度なセキュリティ設定
    

## ✅ チュートリアル完成後のゴール

- CKAD試験で素早くRBACとSAの設定ができるようになる
    
- 実務でもRBACとServiceAccountを使ったセキュリティ設計を自信を持って行えるようになる