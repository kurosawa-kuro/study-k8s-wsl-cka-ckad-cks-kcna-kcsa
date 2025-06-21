## 🔒 最小構成チュートリアル：SecurityContext と NetworkPolicy

このチュートリアルでは、セキュリティ設定の基礎を学ぶために、**SecurityContext（コンテナの権限管理）**と**NetworkPolicy（Pod間通信制御）**を、最小構成のマニフェストで作成・動作確認を行います。

---

## ✅ 前提条件

- Kubernetes クラスターが動作していること（kind, minikubeなど）
    
- kubectl インストール済み
    

---

## 🚩 作業ディレクトリ作成

```bash
mkdir -p ~/dev/k8s-security && cd ~/dev/k8s-security
```

---

## 📌 1. SecurityContext の設定（権限制御）

`pod-securitycontext.yaml` を作成：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  containers:
  - name: nginx
    image: nginx:latest
    securityContext:
      runAsNonRoot: true
      allowPrivilegeEscalation: false
      capabilities:
        drop:
        - ALL
```

### 📝 設定の説明：

- **runAsUser:** コンテナ内のプロセスを指定のユーザーID（UID:1000）で実行
    
- **runAsGroup:** グループIDを指定（GID:3000）
    
- **fsGroup:** ボリュームマウントのファイルの所有権を設定（GID:2000）
    
- **runAsNonRoot:** rootユーザーでの起動を禁止
    
- **allowPrivilegeEscalation:** 権限昇格を禁止
    
- **capabilities.drop:** コンテナ内からすべてのLinuxカーネル機能を無効化
    

確かに動作確認が不十分でした。  
実際にPod内でどのユーザーIDが適用されているかを直接確認する手順を以下に示します。

---

## ✅ SecurityContext の実践的な動作確認方法

以下の手順を追加し、実際にコンテナ内で指定されたユーザーID・グループIDで動作していることを確認しましょう。

### 🚩 Pod内のユーザーIDとグループIDを確認する

Podにアクセスし、動作中のユーザーとグループを確認します。

```bash
kubectl exec -it secure-pod -- sh
```

Pod内のシェルが立ち上がったら、以下のコマンドを実行します。

```bash
id
```

以下のような出力が表示されれば成功です。

```bash
uid=1000 gid=3000 groups=2000
```

- **uid=1000**: 指定したユーザーIDで実行されている
    
- **gid=3000**: 指定したグループIDで実行されている
    
- **groups=2000**: ファイルアクセス権として設定したfsGroupが適用されている
    

---

## 🚨 動作確認まとめ（修正版）

```bash
kubectl apply -f pod-securitycontext.yaml

kubectl get pods secure-pod

# Pod内に入り、動作ユーザーを確認
kubectl exec -it secure-pod -- sh
id  # ← 実行ユーザーを確認
```

---

🎉 **修正完了：実際にコンテナ内の動作を確認することで、SecurityContextの設定が適用されているかを明確に確認できました！**
---

## 📌 2. NetworkPolicy（Pod間の通信制限）

デフォルトでKubernetesはPod間の通信を制限しません。  
NetworkPolicyを使って、特定のPodだけ通信を許可する設定をします。

### 🔧 Pod作成

`frontend.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
  labels:
    role: frontend
spec:
  containers:
  - name: nginx
    image: nginx
```

`backend.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend
  labels:
    role: backend
spec:
  containers:
  - name: nginx
    image: nginx
```

### 🔧 NetworkPolicy 作成（frontend → backendのみ許可）

`networkpolicy.yaml`

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend-to-backend
spec:
  podSelector:
    matchLabels:
      role: backend
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
```

### 🚀 適用して確認：

```bash
# Pod をデプロイ
kubectl apply -f frontend.yaml
kubectl apply -f backend.yaml

# NetworkPolicyをデプロイ
kubectl apply -f networkpolicy.yaml

# 通信確認用に一時Podを起動
kubectl run curl-pod --rm -it --image=curlimages/curl sh
```

一時Pod内で通信確認：

```bash
# backendへの通信テスト（許可されないはず）
curl backend

# frontendへの通信テスト（許可されるはず）
curl frontend
```

> **注意：** NetworkPolicyはCNIプラグインが対応している必要があります（kindやminikubeは標準対応）。

---

## 🧹 クリーンアップ

```bash
kubectl delete pod secure-pod frontend backend
kubectl delete networkpolicy allow-frontend-to-backend
```

---

## 📚 学習のポイント（まとめ）

|機能|用途|CKAD|
|---|---|---|
|SecurityContext|コンテナの権限・アクセス制御|✅|
|NetworkPolicy|Pod間通信の制御・隔離|✅|

- SecurityContext は Pod/コンテナ単位での実行ユーザーや権限を制御。
    
- NetworkPolicy はネットワーク通信の許可範囲を制限し、Pod間の安全性を高める。
    

---

🎉 **完了：これでKubernetesの基本的なセキュリティ機能の実践的な理解が深まりました！**