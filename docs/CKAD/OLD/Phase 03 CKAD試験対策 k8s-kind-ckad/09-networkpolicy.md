# 📘 CKAD試験対策チュートリアル：NetworkPolicyによる通信制御

## 🚩 作業ディレクトリ

作業ディレクトリは以下を使用します。

```
~/dev/k8s-kind-ckad/09-networkpolicy
```

---

## ✅ コンテナイメージの選定

本チュートリアルでは **Option B: Node.js Express API (AWS ECRプライベートイメージ)** を使用します。

### 理由

- 実際のHTTPリクエストで挙動を検証することで、ネットワークポリシーの実践的な効果を明確に把握できます。
    
- CKAD試験においてもリアルな環境を想定したシナリオが重要です。
    

---

## ✅ YAMLマニフェストの作成方法（CKAD試験スタイル）

### 1. 初期YAMLの迅速生成

```bash
kubectl create deployment express-api --image=986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5 --dry-run=client -o yaml > deployment.yaml
```

### 2. 最小限の必須フィールド修正（差分形式）

```diff
 spec:
   replicas: 2
   selector:
     matchLabels:
+      app: express-api
   template:
     metadata:
       labels:
+        app: express-api
     spec:
       containers:
         - name: container-nodejs-api-8000
           image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
+          ports:
+            - containerPort: 8000
```

---

## ✅ NetworkPolicyの作成

### 全Ingress通信をデフォルトで拒否

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-ingress
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress: []
```

### 特定ラベルPodからのみ通信許可

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-express-api-ingress
spec:
  podSelector:
    matchLabels:
      app: express-api
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          access: allowed
    ports:
    - protocol: TCP
      port: 8000
```

---

## ✅ 確認方法

1. NetworkPolicy適用前の通信確認
    

```bash
kubectl run test-deny --image=busybox --restart=Never --rm -it -- wget -qO- http://express-api:8000/posts
```

2. NetworkPolicyの適用後
    

```bash
kubectl apply -f default-deny-ingress.yaml
kubectl apply -f allow-express-api-ingress.yaml
```

再度同じテストを行い、拒否されることを確認します。

3. 通信許可ラベルを持つPodを作成
    

```bash
kubectl run allowed-test --labels access=allowed --image=busybox --restart=Never --rm -it -- wget -qO- http://express-api:8000/posts
```

この操作が成功することを確認します。

---

## ✅ CKAD試験で重要なポイント

- YAMLはゼロから作成せず、迅速な生成手順を使用
    
- 必須フィールド (`labels`, `containerPort`) の設定を忘れない
    
- PodのRunning状態確認と通信制御挙動の確認
    
- NetworkPolicyを用いた通信制御の設定および検証
    

---

## ✅ 推奨使用環境

|項目|バージョン例|
|---|---|
|OS|Ubuntu 22.04|
|kind|v0.23.0|
|kubectl|v1.29.x|
|Helm|v3.14.x|
|Docker|24.0+|
|AWS CLI|v2 (ECR認証必須)|

---

## ✅ GitHubへのPush

```bash
cd ~/dev/k8s-kind-ckad
git add 09-networkpolicy
git commit -m "CKAD試験対策: NetworkPolicyによる通信制御"
git push origin main
```

---

## ✅ 今後のチュートリアル拡張性

今回の内容は以下の高度なトピックにつながります。

- マルチコンテナPodの作成
    
- ConfigMap/Secretを活用した設定管理
    
- ProbeによるPodのヘルスチェック
    
- Service / IngressによるPodの公開
    

---

## ✅ チュートリアル完了時のゴール

- CKAD試験でNetworkPolicyを迅速・正確に設定し、Pod通信制御を理解
    
- Kubernetesでの安全なPod間通信の設計を実務で即応用可能なスキルを習得