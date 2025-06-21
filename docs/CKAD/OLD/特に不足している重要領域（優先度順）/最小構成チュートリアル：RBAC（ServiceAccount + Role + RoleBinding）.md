了解しました！以下は、CKAD試験レベルに対応した **最小構成のRBACチュートリアル（ServiceAccount + Role + RoleBinding）** です。  
Podが `get pods` を実行できるように権限を付与し、それが **許可されるケース** と **拒否されるケース** の違いを体感します。

---

## 🔐 最小構成チュートリアル：RBAC（ServiceAccount + Role + RoleBinding）

### ✅ 目的

- ServiceAccount を作成し、それを使う Pod を起動
    
- Role + RoleBinding を定義して `get pods` 権限を制御
    
- `kubectl exec` で Pod 内から `kubectl get pods` を試すことで、**RBACによるアクセスの違い**を実際に体感
    

---

### 📂 作業ディレクトリ

```bash
mkdir -p ~/dev/k8s-rbac && cd ~/dev/k8s-rbac
```

---

## 📄 1. ServiceAccount の作成

`sa.yaml`

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: api-sa
  namespace: default
```

---

## 📄 2. Role の作成（Podの一覧取得を許可）

`role.yaml`

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```

---

## 📄 3. RoleBinding の作成

`rolebinding.yaml`

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: bind-api-sa
  namespace: default
subjects:
- kind: ServiceAccount
  name: api-sa
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 📄 4. Pod を ServiceAccount 指定で起動

`pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: api-pod
spec:
  serviceAccountName: api-sa
  containers:
  - name: curl
    image: bitnami/kubectl:latest
    command: ["sleep", "3600"]
```

---

## 🚀 適用コマンド

```bash
kubectl apply -f sa.yaml
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
kubectl apply -f pod.yaml
```

---

## ✅ 動作確認（許可される）

```bash
kubectl exec -it api-pod -- sh
kubectl get pods
```

→ `default` Namespace の Pod一覧が表示されれば成功（Role + RoleBinding により get/list が許可されている）

---

## ❌ RoleBinding を削除して試す（拒否される）

```bash
kubectl delete rolebinding bind-api-sa

kubectl exec -it api-pod -- sh
kubectl get pods
```

→ `Error from server (Forbidden)` が出れば **RBACで制限されていることを確認**できたことになります。

---

## 🧹 クリーンアップ

```bash
kubectl delete -f pod.yaml
kubectl delete -f sa.yaml
kubectl delete -f role.yaml
```

---

## 🎯 ポイントまとめ

|リソース|役割|
|---|---|
|ServiceAccount|Podに割り当てる「身分証明書」|
|Role|「何ができるか（例：podsのget/list）」を定義|
|RoleBinding|身分と権限を「ひもづけ」る|

---

このチュートリアルを繰り返し行うことで、**ServiceAccountとRBACの関係性と制御の感覚**が実務レベルで身につきます。  
不明点があれば、いつでもフォローします！