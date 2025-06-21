具体的なコマンドと手順を、CKAD試験に合わせて丁寧に示します。

---

# 📘 CKADチュートリアル: マルチコンテナPod（サイドカー含む）【Express + BusyBox】

CKAD試験では、以下の流れでマニフェスト作成を迅速に進めます。

- `kubectl create`コマンドでYAML生成
    
- 最低限の修正で完成させる
    
- 動作確認を迅速・確実に行う
    

---

## 📂 作業ディレクトリ構造

```bash
~/dev/k8s-kind-ckad/02-multicontainer-pod
└── multicontainer-pod.yaml  # YAML生成・編集用
```

---

## 🚀 手順詳細（Step-by-Step）

### ✅ Step 1: クラスタ状態の確認（CKAD本番でも推奨）

作業前にクラスター状態をチェックします。

```bash
kubectl get nodes
kubectl get pods --all-namespaces
```

---

### ✅ Step 2: YAMLの初期生成（kubectl createで迅速生成）

まずはメインコンテナ（Express）のYAMLを生成：

```bash
cd ~/dev/k8s-kind-ckad/02-multicontainer-pod

kubectl run express-pod \
  --image=986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5 \
  --dry-run=client -o yaml > multicontainer-pod.yaml
```

初期YAML（生成直後）:

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: express-pod
  name: express-pod
spec:
  containers:
  - image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
    name: express-pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

---

### 🛠 Step 3: 必須フィールドの修正（差分形式で明示）

**[修正箇所①]** Podとコンテナ名を明確に指定：

```diff
metadata:
- name: express-pod
+ name: multicontainer-pod
  labels:
-   run: express-pod
+   app: multicontainer-app
```

**[修正箇所②]** コンテナ名・ポート番号を追加：

```diff
spec:
  containers:
  - image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
-   name: express-pod
+   name: express-container
+   ports:
+     - containerPort: 8000
```

**[修正箇所③]** サイドカー（BusyBox）コンテナ追加：

```diff
  containers:
  - image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
    name: express-container
    ports:
      - containerPort: 8000
+ - name: busybox-sidecar
+   image: busybox
+   command: ["/bin/sh"]
+   args: ["-c", "while true; do wget -qO- http://localhost:8000/posts; sleep 5; done"]
```

**[修正箇所④]** emptyDirボリューム共有を設定：

```diff
spec:
+ volumes:
+   - name: shared-data
+     emptyDir: {}

  containers:
  - image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
    name: express-container
    ports:
      - containerPort: 8000
+   volumeMounts:
+     - name: shared-data
+       mountPath: /usr/src/app/shared

  - name: busybox-sidecar
    image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do wget -qO- http://localhost:8000/posts; sleep 5; done"]
+   volumeMounts:
+     - name: shared-data
+       mountPath: /shared
```

---

### ✅ Step 4: 完成版YAML（CKAD試験レベルの最終版）

最終YAML（`multicontainer-pod.yaml`）:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multicontainer-pod
  labels:
    app: multicontainer-app
spec:
  volumes:
    - name: shared-data
      emptyDir: {}

  containers:
    - image: 986154984217.dkr.ecr.ap-northeast-1.amazonaws.com/container-nodejs-api-8000:v1.0.5
      name: express-container
      ports:
        - containerPort: 8000
      volumeMounts:
        - name: shared-data
          mountPath: /usr/src/app/shared

    - name: busybox-sidecar
      image: busybox
      command: ["/bin/sh"]
      args: ["-c", "while true; do wget -qO- http://localhost:8000/posts; sleep 5; done"]
      volumeMounts:
        - name: shared-data
          mountPath: /shared

  restartPolicy: Always
```

---

### ✅ Step 5: YAML適用 & Pod状態確認

Podデプロイ：

```bash
kubectl apply -f multicontainer-pod.yaml
```

リアルタイムでPodを確認：

```bash
kubectl get pods -w
```

状態が `Running`になるまで確認します。

---

### ✅ Step 6: PodのHTTPアクセス確認（port-forward）

Expressコンテナにアクセス可能か確認します：

```bash
kubectl port-forward pod/multicontainer-pod 8080:8000
```

別ターミナルでアクセス：

```bash
curl http://localhost:8080/posts
```

正常なレスポンスを確認できること：

```json
[{"id":1,"title":"Post 1"},{"id":2,"title":"Post 2"}]
```

---

### ✅ Step 7: サイドカーの動作確認（ログ）

BusyBoxコンテナがExpress APIに定期的にアクセスしていることを確認：

```bash
kubectl logs multicontainer-pod -c busybox-sidecar
```

レスポンスが表示されることを確認できます。

---

### 🧹 Step 8: 動作確認後のクリーンアップ

Podの削除：

```bash
kubectl delete -f multicontainer-pod.yaml
```

削除を確認：

```bash
kubectl get pods
```

---

## 📌 CKAD試験ポイント再整理

- **`kubectl create`** を使った迅速なYAML生成が重要
    
- 必須フィールドの追加は正確かつ最小限に（labels, containerPort, volumesなど）
    
- Pod状態確認（Running）と実際の動作確認（curl）が重要
    
- 作業スピードと正確性が合格の鍵
    

---

## 🎖 今後の学習ステップ

- ConfigMap / Secret連携
    
- Probe（Liveness / Readiness）設定
    
- Service / Ingress公開
    
- NetworkPolicy設定
    

---

🎯 以上でCKAD試験を意識した『マルチコンテナPod』の作成・確認方法を完璧に習得できました！