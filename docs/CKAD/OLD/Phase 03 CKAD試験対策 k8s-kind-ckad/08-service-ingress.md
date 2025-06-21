# 📘 CKAD試験対策チュートリアル：ServiceとIngressによるPodの公開

## 🚩 作業ディレクトリ

作業ディレクトリは以下を使用します。

```
~/dev/k8s-kind-ckad/08-service-ingress
```

---

## ✅ コンテナイメージの選定

本チュートリアルでは **Option B: Node.js Express API (AWS ECRプライベートイメージ)** を使用します。

### 理由

- 実際のHTTPリクエストで挙動を検証できるため、ServiceとIngressを用いたリアルな運用をシミュレーション可能
    
- CKAD試験でも実務に近い状況が求められるため、実践的な検証が可能なExpressイメージが最適
    

---

## ✅ YAMLマニフェストの作成方法（CKAD試験スタイル）

### 1. 初期YAMLの迅速生成

```bash
kubectl create deployment express-api --image=986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5 --dry-run=client -o yaml > deployment.yaml
```

### 2. 最小限の必須フィールド修正（差分形式）

```diff
 spec:
   replicas: 3
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

## ✅ Serviceの作成

### Serviceマニフェスト (ClusterIP)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: express-service
spec:
  selector:
    app: express-api
  ports:
    - protocol: TCP
      port: 8000
      targetPort: 8000
  type: ClusterIP
```

### 確認方法

```bash
kubectl apply -f service.yaml
kubectl get svc express-service
kubectl run test-pod --image=busybox --restart=Never --rm -it -- wget -qO- http://express-service:8000/posts
```

---

## ✅ Ingressの作成

### 前提: NGINX Ingress Controllerが導入済み

### Ingressマニフェスト

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: express-ingress
spec:
  rules:
    - http:
        paths:
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: express-service
                port:
                  number: 8000
```

### 確認方法

```bash
kubectl apply -f ingress.yaml
kubectl get ingress express-ingress

# ローカル環境またはEC2で公開ポートが許可されている場合
curl http://<IngressコントローラのIP>/api/posts
```

---

## ✅ CKAD試験で重要なポイント

- YAMLはゼロから書かず、必ず `kubectl create` を利用
    
- 必須フィールド (`labels`, `containerPort`) の明示的設定
    
- PodがRunning状態になることを必ず確認
    
- ServiceとIngressによるPodアクセス公開の挙動を具体的に検証
    
- 作業のスピードと正確性が合格の鍵
    

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
git add 08-service-ingress
git commit -m "CKAD試験対策: Service・IngressによるPod公開"
git push origin main
```

---

## ✅ 今後のチュートリアル拡張性

本チュートリアルでの経験は、以下の発展的内容へと繋がります。

- マルチコンテナPodの作成
    
- ConfigMap/Secretとの設定連携
    
- Liveness/Readiness Probeの活用
    
- NetworkPolicyを使ったアクセス制御
    

---

## ✅ チュートリアル完了時のゴール

- CKAD試験においてServiceとIngressの設定を迅速・正確に完了できる
    
- Kubernetesの基本機能を理解し、実務でも即応用可能なスキルを習得する