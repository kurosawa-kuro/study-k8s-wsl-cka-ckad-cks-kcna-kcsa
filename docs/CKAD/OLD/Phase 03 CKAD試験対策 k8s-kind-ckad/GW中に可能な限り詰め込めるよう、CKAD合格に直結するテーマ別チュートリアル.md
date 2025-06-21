以下に、分かりやすく整理された **作業ディレクトリ構造案** を提案します。

CKADの試験範囲・実務での再利用性も考慮した構成です。

---

## 📂 推奨する作業ディレクトリ構成

```bash
~/dev/k8s-kind-ckad/
├── 01-pod-basic                 # Pod基礎（nginx, busybox）
├── 02-multicontainer-pod        # マルチコンテナPod（Express + busybox）
├── 03-job                       # Job（busybox）
├── 04-cronjob                   # CronJob（busybox or Express）
├── 05-configmap-secret          # ConfigMap / Secret（Express）
├── 06-probe                     # Probe - Liveness/Readiness（Express）
├── 07-volume-pvc                # Volume / PVC（Express）
├── 08-service-ingress           # Service / Ingress（Express）
├── 09-networkpolicy             # NetworkPolicy（Express + busybox）
├── 10-securitycontext           # SecurityContext（busybox）
├── 11-rbac                      # RBAC（bitnami/kubectl）
└── 12-logs-exec-debug           # ログ / exec / debug（Express）
```

---

## 🎯 構成のポイント・理由

- **番号付け (`01`, `02`,...)**:  
    演習の順序を明確にして迷いなく学習可能。試験対策として体系的。
    
- **テーマ名 (`pod-basic`, `multicontainer-pod`,...)**:  
    内容が直感的に分かり、後からも復習・再利用が容易。
    
- **使用するイメージ（nginx, busybox, express, bitnami/kubectl）**:  
    チュートリアル内容に即した、軽量かつ実践的な選択。
    

---

## 📌 これらのディレクトリの使用方法（再確認）

各ディレクトリ内には以下を含めます:

- YAMLマニフェスト（`kubectl create`で生成後に編集）
    
- 各チュートリアルのREADME.md（手順やポイントを明記）
    
- 必要に応じて検証スクリプト・ログなど（任意）
    

例：

```bash
01-pod-basic/
├── pod-basic.yaml
└── README.md
```

---

## 🚩 チュートリアルとイメージ対応表（再掲・再整理）

|No.|チュートリアルテーマ|使用イメージ|Ingress必要？|
|---|---|---|---|
|01|Pod基礎|✅ nginx or busybox|❌|
|02|マルチコンテナPod（サイドカー）|✅ express + busybox|△|
|03|Job|✅ busybox|❌|
|04|CronJob|✅ busybox or express|△|
|05|ConfigMap / Secret|✅ express|✅|
|06|Probe (Liveness/Readiness)|✅ express|✅|
|07|Volume / PVC|✅ express|△|
|08|Service / Ingress|✅ express|✅（必須）|
|09|NetworkPolicy|✅ express + busybox|✅|
|10|SecurityContext（ユーザー確認）|✅ busybox|❌|
|11|RBAC（get podsテスト）|✅ bitnami/kubectl|❌|
|12|ログ / exec / debug|✅ express|△|

---

## 🌟 CKAD試験・実務双方に適した構成

- CKADの試験項目を完全網羅
    
- 実務での再利用性も考慮した明確でシンプルな構成
    
- YAMLやIngress、ServiceなどCKAD必須項目を着実に習得可能
    

ぜひ、このディレクトリ構成を採用して、CKAD合格と実務力を同時に獲得しましょう！🔥


以下に、Ingressが必要かどうかを含め、最新版の情報を整理したマークダウン表を再作成しました。

---

## 📘 Kubernetesチュートリアル対応表（Ingressの必要性を含む最新版）

| チュートリアルテーマ                  | 推奨イメージ                   | 選定理由                                         | Ingress必要？ |
| --------------------------- | ------------------------ | -------------------------------------------- | ---------- |
| Pod基礎                       | ✅ `nginx` or `busybox`   | 起動確認・再起動動作・yaml練習には軽量な公式イメージが最適              | ❌          |
| マルチコンテナPod（サイドカー含む）         | ✅ `express` + `busybox`  | メインはExpress、自動リクエストやログ監視にBusyBoxなどを使用する      | △          |
| Job                         | ✅ `busybox`              | シンプルな一度きりのタスク（`echo`・`sleep`）に最適             | ❌          |
| CronJob                     | ✅ `busybox` or `express` | 定期タスクが軽量ならbusybox、HTTPリクエストなどならExpressが最適    | △          |
| ConfigMap / Secret          | ✅ `express`              | 設定変更がHTTPレスポンスに即時反映されるため、Expressが適任          | ✅          |
| Probe（Liveness / Readiness） | ✅ `express`              | `/healthz`経由でIngressを用いてKubernetes的な疎通性を評価可能 | ✅          |
| Volume / PVC                | ✅ `express`              | `/mnt/data`にデータを保持し、HTTPレスポンスに使うと実践的         | △          |
| Service / Ingress           | ✅ `express`              | Ingressによるルーティングや公開を主題とするため、Expressが最適       | ✅（必須）      |
| NetworkPolicy               | ✅ `express` + `busybox`  | Ingress経由でアクセス制御を実践的にテスト可能                   | ✅          |
| SecurityContext（ユーザー確認）     | ✅ `busybox`              | `id`確認だけならExpress不要、軽量CLI環境としてbusyboxがベスト    | ❌          |
| RBAC（get podsテスト）           | ✅ `bitnami/kubectl`      | Pod内でのkubectlコマンド実行テストには専用イメージが必要            | ❌          |
| ログ / exec / debug           | ✅ `express`              | HTTPリクエストを通じて明確なログが確認可能                      | △          |

---

## 🔁 補足：Ingressが特に効果的な場面

以下のテーマではIngressを含めて学習すると、実務やCKAD試験に直結します：

- **ConfigMap / Secret：** 設定変更の即時反映をIngress経由で検証可能
- **Probe系（Liveness / Readiness）：** 外部ルーティング経由のヘルスチェックを実施可能
- **Service / Ingress：** Ingressそのものがテーマの中心
- **NetworkPolicy：** ネットワーク制御の効果をIngress経由で評価可能

---

## 🎯 結論：Ingressの有用性まとめ

- Kubernetesの約7割以上の実践的テーマで、**Ingressを組み合わせた演習がCKAD合格および実務に非常に有効**です。
- 特に`express`のようにHTTPレスポンスを扱うアプリでは、Ingressの追加によって『よりリアルな学習』が可能です。

> 💡『最小構成 + Ingressルーティング』のテンプレートを用意すると、すべての演習を簡単かつ効果的に進められます。

Ingressを含めた基本的なテンプレートの作成や、それぞれの詳細な演習が必要になったらいつでもお知らせください！🚀
---

## 🔁 補足：Ingressが真に活きる場面

- **ConfigMap / Secret：** 設定変更後のレスポンス確認に便利
    
- **Probe系：** `/healthz` を経由してK8s的に「疎通性」を評価できる
    
- **NetworkPolicy：** パス単位アクセス制御と組み合わせると強力
    

---

## 🎯 結論

> 7割以上の実戦系テーマには、**Ingressがあった方がCKAD合格＆実務力向上に直結**します。

特に `/posts`, `/healthz` のようなレスポンス確認付きエンドポイントを持つ **Express APIとの親和性が高い** ので、  
「最小構成 + Ingressルーティング確認」は、**すべての演習で再利用できるテンプレ**になります。

---

必要であれば、すべてのチュートリアルで `Ingressルール付きExpress公開` を簡単に追加できるテンプレも提供可能です。  
お気軽にご依頼ください！🔥

以下に、**CKADハンズオンで使うイメージ選択の判断基準とおすすめ対応表**を、マークダウンスプレッドシート形式で整理しました。

---

## 📊 Kubernetesチュートリアル用イメージ選択：対応表

| チュートリアルテーマ                  | 推奨イメージ                  | 選定理由                                               |
| --------------------------- | ----------------------- | -------------------------------------------------- |
| Pod基礎                       | ✅ `nginx` or `busybox`  | 起動確認・再起動動作・yaml練習には軽量な公式イメージが最適                    |
| マルチコンテナPod（サイドカー含む）         | ✅ `express` + `busybox` | メイン側はExpress、自動リクエストやログ監視にはBusyBoxなどを使う            |
| Job                         | ✅ `busybox`             | `echo` や `sleep` を1回実行する用途に最適                      |
| CronJob                     | ✅ `busybox` or Express  | 定期実行の負荷が少ない内容ならbusybox。ExpressにPingするなどならexpressも可 |
| ConfigMap / Secret          | ✅ `express`             | 環境変数の変化やファイル注入によるアプリ挙動変化を確認するにはExpressが最も効果的       |
| Probe（Liveness / Readiness） | ✅ `express`             | `/healthz` や `/posts` を用いて実際の挙動確認ができる              |
| Volume / PVC                | ✅ `express`             | `/mnt/data` に書き込むなどの動作が確認しやすい                      |
| Service / Ingress           | ✅ `express`             | 外部アクセスが視覚的に確認しやすく、ポート8000を使うことで実務に近い設定を試せる         |
| NetworkPolicy               | ✅ `express` + `busybox` | Express側に通信し、busyboxなどからwget/curlテストする構成が現実的       |
| SecurityContext（ユーザー確認）     | ✅ `busybox`             | `id` コマンドが確実に使えるため。Expressは動作が複雑で不要                |
| RBAC（get podsテスト）           | ✅ `bitnami/kubectl`     | Pod内から `kubectl get pods` を試すにはkubectlが入っている必要がある  |
| ログ / exec / debug           | ✅ `express`             | ログがわかりやすく、異常時も再現しやすい                               |

---

## ✅ 結論：どう使い分けるべき？

- **基本構文の練習・構成理解だけなら → `nginx` や `busybox` が軽くて速い**
    
- **設定値や動作の効果をアプリに反映させたいなら → `Express API（黒澤ECR）` 一択**
    
- **RBACやkubectl exec用途だけは `bitnami/kubectl` が便利**
    

---

## ✨ おすすめ運用方針

1. **最初は busybox / nginx で構文確認と成功体験**
    
2. **Express API に置き換えて「動きのある」確認（効果の実感）**
    
3. **本番想定では Express で通し演習 → CKADの合格精度UP**
    

---

必要であれば、それぞれのケースで `kubectl create` に使うおすすめコマンド雛形も共有できます。  
この表をベースに、チュートリアルに応じたイメージ選択を使い分けていきましょう 💪

了解しました。EC2のkind環境で、Express API（GitHub: container-nodejs-api-8000）をベースに、GW中に可能な限り詰め込めるよう、CKAD合格に直結するテーマ別チュートリアルを順番付きでリストアップします。

それぞれのテーマは、独立して動作確認できるよう最小構成で設計し、確実に練度を上げられるように構成します。完了次第、順次ご共有しますので、しばらくお待ちください。

# CKAD合格を目指す Kubernetes テーマ別チュートリアル一覧

1. **Pod基礎：単一コンテナPodのデプロイ**
    
    - **目的**: Kubernetesにおける最小デプロイ単位であるPodの基本を学びます。Node.js Expressアプリコンテナを1つ持つPodを作成し、Podのライフサイクルや基本操作に習熟することが目的です。
        
    - **使用マニフェスト**: `Pod`（`apiVersion: v1`, `kind: Pod`）のYAMLマニフェスト。コンテナイメージにExpress API（ポート8000）を指定し、必要なら`restartPolicy: Always`など基本フィールドを設定します。
        
    - **確認内容**: Podが正常に`Running`状態になることを確認します。`kubectl get pods`でステータスを確認し、`kubectl port-forward`等を使ってPod内のExpress API（ポート8000）にアクセスします。ブラウザやcurlで`http://<ポートフォワード先>/posts`等のエンドポイントにリクエストを送り、HTTP 200レスポンスが返ることを検証します。 ([ConfigMap | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/configmap/#:~:text=ConfigMap%E3%81%AF%E3%80%81%20%E6%A9%9F%E5%AF%86%E6%80%A7%E3%81%AE%E3%81%AA%E3%81%84%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E3%82%AD%E3%83%BC%E3%81%A8%E5%80%A4%E3%81%AE%E3%83%9A%E3%82%A2%E3%81%A7%E4%BF%9D%E5%AD%98%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BAPI%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%A7%E3%81%99%E3%80%82Pod%E3%81%AF%E3%80%81%E7%92%B0%E5%A2%83%E5%A4%89%E6%95%B0%E3%80%81%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E5%BC%95%E6%95%B0%E3%80%81%E3%81%BE%20%E3%81%9F%E3%81%AF%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E5%86%85%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%A8%E3%81%97%E3%81%A6ConfigMap%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82)) ([Secret | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/secret/#:~:text=Secret%E3%81%A8%E3%81%AF%E3%80%81%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%82%84%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E3%80%81%E3%82%AD%E3%83%BC%E3%81%AA%E3%81%A9%E3%81%AE%E5%B0%91%E9%87%8F%E3%81%AE%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%80%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%93%E3%81%A8%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E6%83%85%E5%A0%B1%E3%81%AF%E3%80%81Secret%E3%82%92%E7%94%A8%E3%81%84%E3%81%AA%E3%81%84%E3%81%A8Pod%E3%81%AE%E5%AE%9A%E7%BE%A9%E3%82%84%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E7%9B%B4%E6%8E%A5%E8%A8%98%E8%BC%89%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%97%E3%81%BE%E3%81%86%E3%81%8B%E3%82%82%E3%81%97%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82%20Secret%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8C%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AB%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%81%E3%82%8B%E5%BF%85%E8%A6%81%E3%81%8C%E3%81%AA%E3%81%8F%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82))
        
2. **マルチコンテナPod：サイドカーパターンの利用**
    
    - **目的**: 1つのPod内で複数コンテナを動かす設計パターンを学びます。メインのExpress APIコンテナと補助コンテナ（サイドカー）を同じPodで稼働させ、コンテナ間の連携やデータ共有を確認します。サイドカーコンテナによって、メインアプリの機能拡張や補助サービス提供がどのように行われるか理解することが目標です ([サイドカーコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/sidecar-containers/#:~:text=%E3%82%B5%E3%82%A4%E3%83%89%E3%82%AB%E3%83%BC%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%83%A1%E3%82%A4%E3%83%B3%E3%81%AE%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A8%E5%90%8C%E3%81%98Pod%E5%86%85%E3%81%A7%E5%AE%9F%E8%A1%8C%E3%81%95%E3%82%8C%E3%82%8B%E3%82%BB%E3%82%AB%E3%83%B3%E3%83%80%E3%83%AA%E3%83%BC%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%82%8C%E3%82%89%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E4%B8%BB%E8%A6%81%E3%81%AA%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%20%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E7%9B%B4%E6%8E%A5%E5%A4%89%E6%9B%B4%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AA%E3%81%8F%E3%80%81%E3%83%AD%E3%82%AE%E3%83%B3%E3%82%B0%E3%80%81%E3%83%A2%E3%83%8B%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0%E3%80%81%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%80%81%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E5%90%8C%E6%9C%9F%E3%81%AA%E3%81%A9%E3%81%AE%E8%BF%BD%E5%8A%A0%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%82%84%E6%A9%9F%E8%83%BD%E3%82%92%E6%8F%90%E4%BE%9B%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%82%88%E3%82%8A%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%A9%9F%E8%83%BD%E3%82%92%E5%BC%B7%20%E5%8C%96%E3%81%BE%E3%81%9F%E3%81%AF%E6%8B%A1%E5%BC%B5%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: `Pod`のYAMLで`spec.containers`に2つのコンテナ定義を含めます。1つはExpress APIコンテナ、もう1つは補助用のコンテナ（例：BusyBoxやCurlイメージ）です。2コンテナ間で共有する`emptyDir`ボリュームを定義し、メインコンテナがログファイル等を出力しサイドカーがそれを読み取る、といった設定を行います（ボリュームマウントを双方のコンテナで設定） ([エフェメラルボリューム | Kubernetes](https://kubernetes.io/ja/docs/concepts/storage/ephemeral-volumes/#:~:text=))。
        
    - **確認内容**: Pod内の複数コンテナが全て`Running`になり動作していることを確認します（`kubectl get pod -o wide`でコンテナステータスを見る）。サイドカーコンテナの役割を検証するため、例えばサイドカーからメインのExpressサービスへHTTPリクエストを送るスクリプトを実行させ、そのログ出力を確認します。また、`kubectl logs <Pod名> -c <サイドカー名>`でサイドカーコンテナのログを取得し、メインコンテナの補助動作（ログ収集やヘルスチェックなど）が行われていることを確認します。これにより、サイドカーパターンによるコンテナ間協調動作を体感できます ([サイドカーコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/sidecar-containers/#:~:text=%E3%82%B5%E3%82%A4%E3%83%89%E3%82%AB%E3%83%BC%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%83%A1%E3%82%A4%E3%83%B3%E3%81%AE%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A8%E5%90%8C%E3%81%98Pod%E5%86%85%E3%81%A7%E5%AE%9F%E8%A1%8C%E3%81%95%E3%82%8C%E3%82%8B%E3%82%BB%E3%82%AB%E3%83%B3%E3%83%80%E3%83%AA%E3%83%BC%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%82%8C%E3%82%89%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E4%B8%BB%E8%A6%81%E3%81%AA%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%20%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E7%9B%B4%E6%8E%A5%E5%A4%89%E6%9B%B4%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AA%E3%81%8F%E3%80%81%E3%83%AD%E3%82%AE%E3%83%B3%E3%82%B0%E3%80%81%E3%83%A2%E3%83%8B%E3%82%BF%E3%83%AA%E3%83%B3%E3%82%B0%E3%80%81%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%80%81%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E5%90%8C%E6%9C%9F%E3%81%AA%E3%81%A9%E3%81%AE%E8%BF%BD%E5%8A%A0%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%82%84%E6%A9%9F%E8%83%BD%E3%82%92%E6%8F%90%E4%BE%9B%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%82%88%E3%82%8A%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%A9%9F%E8%83%BD%E3%82%92%E5%BC%B7%20%E5%8C%96%E3%81%BE%E3%81%9F%E3%81%AF%E6%8B%A1%E5%BC%B5%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))。
        
3. **Jobによるバッチ処理実行**
    
    - **目的**: 短命なバッチ処理を実行するKubernetesリソースであるJobの使い方を学びます。一定の処理を実行して完了するワークロードをPodで行い、その完了状態の管理や再試行を確認することで、Jobリソースの動作理解を深めます。
        
    - **使用マニフェスト**: `Job`（`apiVersion: batch/v1`）のYAMLマニフェスト。コンテナには簡単なスクリプト（例：`echo "Hello CKAD"`や一定時間待機）を実行する軽量イメージ（BusyBoxなど）を使用し、`.spec.template`内でRestartPolicyや並行実行数（`parallelism`）を必要に応じ設定します。
        
    - **確認内容**: `kubectl apply`でJobを作成後、`kubectl get jobs`で`SUCCESSFUL`コンテナ数が1になること、`kubectl get pods`で完了状態(`Completed`)のPodが生成されることを確認します。`kubectl logs <Jobが生成したPod名>`でジョブ実行結果のログを確認し、期待通りの出力が得られていることを検証します。加えて、`kubectl describe job <Job名>`でJobの再試行回数や完了状況を確認し、指定した処理が一度だけ実行され正常終了したことを確認します。
        
4. **CronJobによるスケジュール実行**
    
    - **目的**: 定期実行タスクをスケジューリングするCronJobリソースを学びます。Linuxのcronのようにスケジュール設定に従ってジョブを繰り返し実行させることで、定期バッチ処理の管理方法を理解します ([CronJobを使用して自動化タスクを実行する | Kubernetes](https://kubernetes.io/ja/docs/tasks/job/automated-tasks-with-cron-jobs/#:~:text=match%20at%20L860%20CronJob%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E3%81%A8%E3%80%81Job%E3%82%92%E6%99%82%E9%96%93%E3%83%99%E3%83%BC%E3%82%B9%E3%81%AE%E3%82%B9%E3%82%B1%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%A7%E5%AE%9F%E8%A1%8C%E3%81%A7%E3%81%8D%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82%E3%81%93%E3%81%AE%E8%87%AA%E5%8B%95%E5%8C%96%E3%81%95%E3%82%8C%E3%81%9FJob%E3%81%AF%E3%80%81Linux%E3%81%BE%E3%81%9F%E3%81%AFUNIX%E3%82%B7%20%E3%82%B9%E3%83%86%E3%83%A0%E4%B8%8A%E3%81%AECron%E3%81%AE%E3%82%88%E3%81%86%E3%81%AB%E5%AE%9F%E8%A1%8C%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: `CronJob`（`apiVersion: batch/v1`）のYAMLマニフェスト。例えば毎分実行されるジョブとして、先の項目のBusyBoxコンテナで日時を出力するスクリプトをスケジュールします。`.spec.schedule`にcron形式で実行間隔（例：`"* * * * *"`毎分）を設定し、`.spec.jobTemplate`に実行するJobテンプレートを記述します ([CronJobを使用して自動化タスクを実行する | Kubernetes](https://kubernetes.io/ja/docs/tasks/job/automated-tasks-with-cron-jobs/#:~:text=CronJob%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B))。必要に応じて`startingDeadlineSeconds`や`concurrencyPolicy`などを設定し、スケジュール遅延時の挙動も指定します。
        
    - **確認内容**: CronJob作成後、まず`kubectl get cronjob`でスケジュールが正しく設定されたCronJobが存在することを確認します。その後、設定した間隔でジョブが実行されているかを`kubectl get jobs,pods`で監視します。毎分新しいJobとPodが生成され、完了後一定時間でPodが終了する様子を確認できます。`kubectl logs`でそれぞれのPodのログを確認し、CronJobにより定期的に指定コマンド（例：日時の出力やExpress APIへのHTTPリクエスト）が実行されていることを検証します ([CronJobを使用して自動化タスクを実行する | Kubernetes](https://kubernetes.io/ja/docs/tasks/job/automated-tasks-with-cron-jobs/#:~:text=CronJob%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B))。不要になったら`kubectl delete cronjob <名前>`でリソースと関連Podを削除し、定期実行が停止することも確認します。
        
5. **データ永続化：PersistentVolume と PersistentVolumeClaim の利用**
    
    - **目的**: コンテナの状態を永続化する仕組みを学びます。Pod消滅後も残るストレージを使用して、データを保存・再利用できるようにする方法を理解します。具体的にはホストマシン上のディレクトリや外部ストレージをPV(永続ボリューム)として扱い、PVC(永続ボリューム要求)を通じてPodにマウントする練習を行います。
        
    - **使用マニフェスト**: `PersistentVolume`（`apiVersion: v1`）のYAMLマニフェストを作成し、`hostPath`を使ってローカルディスク上のパス（例えば`/mnt/data`）をボリュームとして定義します ([永続ボリューム | Kubernetes](https://kubernetes.io/ja/docs/concepts/storage/persistent-volumes/#:~:text=PersistentVolume%20))。次に、それを要求する`PersistentVolumeClaim`（`apiVersion: v1`）のYAMLを作成し、容量やアクセスモード（ReadWriteOnceなど）を指定します。最後に、Expressコンテナを含む`Pod`または`Deployment`のマニフェストで、先のPVCを`volumeMounts`としてコンテナにマウントします。
        
    - **確認内容**: `kubectl get pv`でPVが`Available`になっていること、`kubectl get pvc`でPVCが`Bound`状態でPVとバインドされたことを確認します ([永続ボリューム | Kubernetes](https://kubernetes.io/ja/docs/concepts/storage/persistent-volumes/#:~:text=PersistentVolume%20))。そのPVCを使ったPodを起動後、`kubectl exec`でコンテナ内に入り、マウントされたパス上でファイルを作成します（例：`echo "test" > /mnt/data/test.txt`）。Podを削除した後、新たに同じPVCをマウントした別のPodを起動し、コンテナ内で`/mnt/data/test.txt`を表示して先ほどの内容が残っていることを確認します。これにより、PersistentVolumeを用いることでPodの寿命を超えてデータが永続化されることを検証できます ([永続ボリューム | Kubernetes](https://kubernetes.io/ja/docs/concepts/storage/persistent-volumes/#:~:text=PersistentVolume%20))。
        
6. **ConfigMapによる設定の外部化**
    
    - **目的**: アプリケーションの非機密設定をコンテナイメージから分離し、柔軟に変更可能にする方法を学びます。ConfigMapリソースを利用して環境変数や設定ファイルをPodに注入し、アプリケーション設定を外部化することで、ビルドせずに挙動を変えられるようにするのが目的です ([ConfigMap | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/configmap/#:~:text=ConfigMap%E3%81%AF%E3%80%81%20%E6%A9%9F%E5%AF%86%E6%80%A7%E3%81%AE%E3%81%AA%E3%81%84%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E3%82%AD%E3%83%BC%E3%81%A8%E5%80%A4%E3%81%AE%E3%83%9A%E3%82%A2%E3%81%A7%E4%BF%9D%E5%AD%98%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BAPI%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%A7%E3%81%99%E3%80%82Pod%E3%81%AF%E3%80%81%E7%92%B0%E5%A2%83%E5%A4%89%E6%95%B0%E3%80%81%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E5%BC%95%E6%95%B0%E3%80%81%E3%81%BE%20%E3%81%9F%E3%81%AF%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E5%86%85%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%A8%E3%81%97%E3%81%A6ConfigMap%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: `ConfigMap`（`apiVersion: v1`）のYAMLマニフェスト。例えばキー`WELCOME_MSG`に任意のメッセージ文字列を設定したConfigMapを作成します。続いて、Express APIコンテナをデプロイする`Deployment`または`Pod`マニフェストで、そのConfigMapを環境変数としてコンテナに渡します（`.spec.containers.env.valueFrom.configMapKeyRef`を使用）。あるいはConfigMapをボリュームとしてマウントし、コンテナ内でファイル経由で設定を読み込む方法も記述します ([ConfigMap | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/configmap/#:~:text=ConfigMap%E3%81%AF%E3%80%81%20%E6%A9%9F%E5%AF%86%E6%80%A7%E3%81%AE%E3%81%AA%E3%81%84%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E3%82%AD%E3%83%BC%E3%81%A8%E5%80%A4%E3%81%AE%E3%83%9A%E3%82%A2%E3%81%A7%E4%BF%9D%E5%AD%98%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BAPI%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%A7%E3%81%99%E3%80%82Pod%E3%81%AF%E3%80%81%E7%92%B0%E5%A2%83%E5%A4%89%E6%95%B0%E3%80%81%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E5%BC%95%E6%95%B0%E3%80%81%E3%81%BE%20%E3%81%9F%E3%81%AF%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E5%86%85%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%A8%E3%81%97%E3%81%A6ConfigMap%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **確認内容**: `kubectl apply -f configmap.yaml`でConfigMapを作成し、`kubectl get configmaps <名前> -o yaml`でキーと値が正しく保存されていることを確認します。次にそのConfigMapを使うPodを起動し、`kubectl exec <pod名> -- printenv WELCOME_MSG`などでコンテナ内の環境変数を出力して、ConfigMapから注入された値が反映されていることを確認します。もしExpressアプリが環境変数を読み取って動作を変える実装であれば、実際にアプリにリクエストを送り設定反映を検証します。例えば、環境変数によって表示メッセージが変わるなら、該当APIエンドポイントのレスポンス内容が変更されていることを確認します。これにより、ConfigMapによる設定外部化の効果を実感できます ([ConfigMap | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/configmap/#:~:text=ConfigMap%E3%81%AF%E3%80%81%20%E6%A9%9F%E5%AF%86%E6%80%A7%E3%81%AE%E3%81%AA%E3%81%84%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E3%82%AD%E3%83%BC%E3%81%A8%E5%80%A4%E3%81%AE%E3%83%9A%E3%82%A2%E3%81%A7%E4%BF%9D%E5%AD%98%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BAPI%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%A7%E3%81%99%E3%80%82Pod%E3%81%AF%E3%80%81%E7%92%B0%E5%A2%83%E5%A4%89%E6%95%B0%E3%80%81%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3%E5%BC%95%E6%95%B0%E3%80%81%E3%81%BE%20%E3%81%9F%E3%81%AF%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E5%86%85%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%A8%E3%81%97%E3%81%A6ConfigMap%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。
        
7. **Secretによる機密情報の管理**
    
    - **目的**: パスワードやAPIキーなど機密性の高い設定情報を安全に扱う方法を学びます。Secretリソースを用いて平文でPodマニフェストに書き込まずに機密データを提供し、アプリケーションがそれを参照する仕組みを習得することが目的です ([Secret | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/secret/#:~:text=Secret%E3%81%A8%E3%81%AF%E3%80%81%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%82%84%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E3%80%81%E3%82%AD%E3%83%BC%E3%81%AA%E3%81%A9%E3%81%AE%E5%B0%91%E9%87%8F%E3%81%AE%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%80%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%93%E3%81%A8%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E6%83%85%E5%A0%B1%E3%81%AF%E3%80%81Secret%E3%82%92%E7%94%A8%E3%81%84%E3%81%AA%E3%81%84%E3%81%A8Pod%E3%81%AE%E5%AE%9A%E7%BE%A9%E3%82%84%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E7%9B%B4%E6%8E%A5%E8%A8%98%E8%BC%89%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%97%E3%81%BE%E3%81%86%E3%81%8B%E3%82%82%E3%81%97%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82%20Secret%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8C%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AB%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%81%E3%82%8B%E5%BF%85%E8%A6%81%E3%81%8C%E3%81%AA%E3%81%8F%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: `Secret`（`apiVersion: v1`）のYAMLマニフェスト（タイプ`Opaque`）を作成します。例えばキー`DB_PASSWORD`に対しBase64エンコードしたパスワード文字列を設定します。次にExpress APIコンテナをデプロイする際に、このSecretを環境変数として渡す定義（`.spec.containers.env.valueFrom.secretKeyRef`）や、Secretをボリュームマウントしてファイル経由で渡す方法を記述します ([Secret | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/secret/#:~:text=Secret%E3%81%A8%E3%81%AF%E3%80%81%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%82%84%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E3%80%81%E3%82%AD%E3%83%BC%E3%81%AA%E3%81%A9%E3%81%AE%E5%B0%91%E9%87%8F%E3%81%AE%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%80%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%93%E3%81%A8%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E6%83%85%E5%A0%B1%E3%81%AF%E3%80%81Secret%E3%82%92%E7%94%A8%E3%81%84%E3%81%AA%E3%81%84%E3%81%A8Pod%E3%81%AE%E5%AE%9A%E7%BE%A9%E3%82%84%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E7%9B%B4%E6%8E%A5%E8%A8%98%E8%BC%89%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%97%E3%81%BE%E3%81%86%E3%81%8B%E3%82%82%E3%81%97%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82%20Secret%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8C%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AB%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%81%E3%82%8B%E5%BF%85%E8%A6%81%E3%81%8C%E3%81%AA%E3%81%8F%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **確認内容**: `kubectl apply -f secret.yaml`でSecretを作成し、`kubectl get secrets`で存在を確認します（`kubectl describe secret <名前>`で中身を直接表示するとBase64データが見えますが平文は確認しません）。Secretを使用したPodを起動後、`kubectl exec`でコンテナ内に入り`printenv DB_PASSWORD`で環境変数に秘密値がセットされていること、またはマウントされたファイル内に正しい値が格納されていることを確認します。さらに、Secretが平文でPod定義に露出しないこと（例えば`kubectl get pod -o yaml`で環境変数の値が隠蔽されていること）も合わせて確認し、Secret経由で機密情報が安全に渡せていることを検証します ([Secret | Kubernetes](https://kubernetes.io/ja/docs/concepts/configuration/secret/#:~:text=Secret%E3%81%A8%E3%81%AF%E3%80%81%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%82%84%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E3%80%81%E3%82%AD%E3%83%BC%E3%81%AA%E3%81%A9%E3%81%AE%E5%B0%91%E9%87%8F%E3%81%AE%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%80%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%81%93%E3%81%A8%E3%81%A7%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E6%83%85%E5%A0%B1%E3%81%AF%E3%80%81Secret%E3%82%92%E7%94%A8%E3%81%84%E3%81%AA%E3%81%84%E3%81%A8Pod%E3%81%AE%E5%AE%9A%E7%BE%A9%E3%82%84%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E7%9B%B4%E6%8E%A5%E8%A8%98%E8%BC%89%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%97%E3%81%BE%E3%81%86%E3%81%8B%E3%82%82%E3%81%97%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82%20Secret%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8C%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AB%E6%A9%9F%E5%AF%86%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%90%AB%E3%82%81%E3%82%8B%E5%BF%85%E8%A6%81%E3%81%8C%E3%81%AA%E3%81%8F%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82))。
        
8. **リソース要求と制限の設定（Resource Requests/Limits）**
    
    - **目的**: PodやコンテナごとにCPUやメモリのリソース割り当てを制御する方法を学びます。適切なリソース**Requests**（最低保証）と**Limits**（上限）を設定することで、安定したアプリケーション動作と効率的なリソース利用を両立させるのが目的です ([Kubernetesのリミットとリクエストについて理解する – Sysdig](https://sysdig.jp/blog/kubernetes-limits-requests/#:~:text=Kubernetes%E3%81%A7%E3%81%AF%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%20%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%81%AE%E6%9C%80%E5%A4%A7%E9%87%8F%20%E3%82%92%20Limits%20%E3%81%A8%E5%AE%9A%E7%BE%A9%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: 任意のPodまたは`Deployment`マニフェストにおいて、各コンテナの定義に`resources:`セクションを追加します。例として、Expressコンテナに対し「0.5 CPU・128MiメモリをRequest、1 CPU・256MiメモリをLimit」といった設定をYAMLに記述します ([コンテナおよびPodへのCPUリソースの割り当て | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/assign-cpu-resource/#:~:text=%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%ABCPU%E3%81%AE%E8%A6%81%E6%B1%82%E3%82%92%E6%8C%87%E5%AE%9A%E3%81%99%E3%82%8B%E3%81%AB%E3%81%AF%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%83%9E%E3%83%8B%E3%83%95%E3%82%A7%E3%82%B9%E3%83%88%E3%81%AB%20))。また、クラスター全体でのリソースクオータを見るため、Namespaceに対する`ResourceQuota`を設定するYAML（例：CPUとメモリの合計使用量上限を制限）も用意します。
        
    - **確認内容**: 設定適用後、`kubectl describe pod <Pod名>`または`kubectl describe deployment <名前>`で各コンテナに指定したRequests/Limitsが反映されていることを確認します。さらに、過剰なリソース要求をした場合の挙動も実験します（例：ノード容量を超えるRequestを設定してPodが`Pending`になるケースや、Limitを下回るRequestであればスケジューリング可能になること）。`kubectl get quota`でNamespaceに設定したリソースクオータ状況を確認し、制限値を超えるPod作成がブロックされ“exceeded quota”エラーが発生することも検証します。以上により、Requestsは最低保証、Limitsは上限であること（Requestsはスケジューラがノード選択時に考慮し、Limitsは実行時に超過を防ぐ役割であること）を理解します ([Kubernetesのリミットとリクエストについて理解する – Sysdig](https://sysdig.jp/blog/kubernetes-limits-requests/#:~:text=Kubernetes%E3%81%A7%E3%81%AF%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%20%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E3%81%AE%E6%9C%80%E5%A4%A7%E9%87%8F%20%E3%82%92%20Limits%20%E3%81%A8%E5%AE%9A%E7%BE%A9%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82))。
        
9. **ServiceAccountとRBACによる認可設定**
    
    - **目的**: Podがデフォルトとは異なるサービスアカウント権限で実行されるよう設定し、Kubernetes APIアクセス権を細かく制御する方法を学びます。開発者視点で最低限、ServiceAccountの切り替え方法とロールの割当（RBAC）を理解し、Podのセキュリティを高めるのが目的です。
        
    - **使用マニフェスト**: `ServiceAccount`（`apiVersion: v1`）のYAMLマニフェストを作成します。例えば`app-sa`という名前のServiceAccountを作成した上で、Express API Pod（またはDeployment）の`.spec.serviceAccountName`に`app-sa`を指定します。さらに、必要に応じてRBACの`Role`や`RoleBinding`のYAMLも用意します（例：`app-sa`に対し特定Namespace内での`get, list`権限のみ与えるRoleを作成し、`RoleBinding`でそのSAに紐付ける）。
        
    - **確認内容**: `kubectl get serviceaccounts`で新規ServiceAccountが作成されていることを確認します（デフォルトで各Namespaceに存在する`default` SAとは別にリストされます）。該当Podが起動したら、`kubectl describe pod <Pod名>`で`Service Account: app-sa`となっていることを確認します。また、Pod内にマウントされたトークンファイル（`/var/run/secrets/kubernetes.io/serviceaccount/token`）が新しいSAに対応したものであることを確認できます。RBAC権限を設定した場合、意図した操作のみ許可されているかをテストします（例えば、許可していない`kubectl exec <Pod> -- kubectl get pods`コマンドをコンテナ内から試みて権限エラーになることを確認するなど）。以上で、ServiceAccountごとにアイデンティティと権限を分離できることを理解します ([サービスアカウント | Kubernetes](https://kubernetes.io/ja/docs/concepts/security/service-accounts/#:~:text=%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E3%81%AF%E3%80%81Kubernetes%E3%81%AB%E3%81%8A%E3%81%84%E3%81%A6%E3%80%81Kubernetes%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%86%85%E3%81%A7%E5%9B%BA%E6%9C%89%E3%81%AE%E3%82%A2%E3%82%A4%E3%83%87%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%82%92%E6%8F%90%E4%BE%9B%E3%81%99%E3%82%8B%E4%BA%BA%E9%96%93%E4%BB%A5%E5%A4%96%E3%81%AE%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E3%81%AE%E4%B8%80%E7%A8%AE%E3%81%A7%E3%81%99%E3%80%82%20%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%20%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3Pod%E3%80%81%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%82%B3%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%8D%E3%83%B3%E3%83%88%E3%80%81%E3%81%8A%E3%82%88%E3%81%B3%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%86%85%E5%A4%96%E3%81%AE%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%81%AF%E3%80%81%E7%89%B9%E5%AE%9A%E3%81%AEServiceAccount%E3%81%AE%E8%AA%8D%E8%A8%BC%E6%83%85%E5%A0%B1%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%81%9D%E3%81%AEServiceAccou%20nt%E3%81%A8%E3%81%97%E3%81%A6%E8%AD%98%E5%88%A5%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%A2%E3%82%A4%E3%83%87%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%81%AF%E3%80%81API%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%81%B8%E3%81%AE%E8%AA%8D%E8%A8%BC%E3%82%84%E3%82%A2%E3%82%A4%E3%83%87%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%83%99%E3%83%BC%E3%82%B9%E3%81%AE%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%81%AE%E5%AE%9F%E8%A3%85%E3%81%AA%E3%81%A9%E3%80%81%E3%81%95%E3%81%BE%E3%81%96%E3%81%BE%E3%81%AA%E7%8A%B6%E6%B3%81%E3%81%A7%E5%BD%B9%E7%AB%8B%E3%81%A1%E3%81%BE%E3%81%99%E3%80%82))。
        
10. **セキュリティコンテキストの設定（SecurityContext）**
    
    - **目的**: Podやコンテナのセキュリティ強化設定を学びます。コンテナ実行ユーザーの指定や権限（Capability）の制御、root権限の制限などを行うSecurityContextの使い方を理解し、コンテナ実行環境のセキュリティを高める手法を習得します ([Podとコンテナにセキュリティコンテキストを設定する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/security-context/#:~:text=%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AFPod%E3%83%BB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E7%89%B9%E6%A8%A9%E3%82%84%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%AB%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%92%E5%AE%9A%E7%BE%A9%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%AB%E3%81%AF%E4%BB%A5%E4%B8%8B%E3%81%AE%E3%82%82%E3%81%AE%E3%81%8C%E5%90%AB%E3%81%BE%E3%82%8C%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E3%81%93%E3%82%8C%E3%82%89%E3%81%AB%E9%99%90%E5%AE%9A%E3%81%AF%E3%81%95%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82))。
        
    - **使用マニフェスト**: `Pod`または各`Container`のマニフェスト内で`securityContext`フィールドを設定します。例として、Expressコンテナについて`securityContext.runAsUser: 1000`や`runAsNonRoot: true`を指定し、コンテナが非rootユーザーで動作するようにします。また必要に応じて`readOnlyRootFilesystem: true`や、特定のLinux Capabilityを削除する設定（例えば`capabilities.drop: ["NET_RAW"]`）も追加します ([Podとコンテナにセキュリティコンテキストを設定する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/security-context/#:~:text=%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AFPod%E3%83%BB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E7%89%B9%E6%A8%A9%E3%82%84%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%AB%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%92%E5%AE%9A%E7%BE%A9%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%AB%E3%81%AF%E4%BB%A5%E4%B8%8B%E3%81%AE%E3%82%82%E3%81%AE%E3%81%8C%E5%90%AB%E3%81%BE%E3%82%8C%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E3%81%93%E3%82%8C%E3%82%89%E3%81%AB%E9%99%90%E5%AE%9A%E3%81%AF%E3%81%95%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82))。Podレベルのセキュリティコンテキストでは`fsGroup`を設定してボリュームのファイル権限を調整する例も含めます。
        
    - **確認内容**: Pod起動後、`kubectl exec <Pod名> -- id`コマンドでコンテナ内の実行ユーザーIDを確認し、指定したUID（例：1000）でプロセスが動いていることを検証します。また、必要なら`kubectl exec -- ls -l /`でルートファイルシステムが読み取り専用になっているかなどを確認します。さらに、`kubectl describe pod <Pod名>`でSecurityContext設定項目が適用されていること（非特権モードになっている等）を確認します。これらにより、SecurityContextを適切に設定することでコンテナの特権を制限し、より安全な実行環境になっていることを理解します ([Podとコンテナにセキュリティコンテキストを設定する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/security-context/#:~:text=%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AFPod%E3%83%BB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E7%89%B9%E6%A8%A9%E3%82%84%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%82%B3%E3%83%B3%E3%83%88%E3%83%AD%E3%83%BC%E3%83%AB%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%92%E5%AE%9A%E7%BE%A9%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%82%B3%E3%83%B3%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%AB%E3%81%AF%E4%BB%A5%E4%B8%8B%E3%81%AE%E3%82%82%E3%81%AE%E3%81%8C%E5%90%AB%E3%81%BE%E3%82%8C%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E3%81%93%E3%82%8C%E3%82%89%E3%81%AB%E9%99%90%E5%AE%9A%E3%81%AF%E3%81%95%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82))。
        
11. **Deploymentによるアプリケーションのデプロイとローリング更新**
    
    - **目的**: Deploymentリソースを使ったアプリケーションの管理手法を学びます。複数レプリカのPodを作成し、ローリングアップデート戦略でイメージ更新や設定変更を行って無停止でリリースする方法、また障害時のロールバックを習得することが目的です。
        
    - **使用マニフェスト**: `Deployment`（`apiVersion: apps/v1`）のYAMLマニフェスト。`.spec.replicas`に例えば2～3など適当なレプリカ数を指定し、テンプレート部分にExpress APIコンテナの定義を記述します。デプロイ戦略はデフォルトのローリング更新（`RollingUpdate`）を利用し、`.spec.strategy`で`maxSurge`や`maxUnavailable`の値を必要に応じて調整します。
        
    - **確認内容**: `kubectl apply -f deployment.yaml`でDeploymentを作成後、`kubectl get deployment`で望むレプリカ数のPodが起動していること（`AVAILABLE`列が適切な数になっていること）を確認します。`kubectl get pods`で同一Deployment由来のPodが均一に稼働しているのを確認したら、イメージの新バージョンへの更新を試します（マニフェスト内のコンテナイメージタグを変更し`kubectl apply`）。その後`kubectl rollout status deployment/<名前>`でローリング更新の進行状況をモニターし、古いPodから新しいPodへ順次入れ替わり、サービス継続したまま更新が完了することを確認します ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,and%20update%20pods%20and%20deployments))。更新に問題があった場合には、`kubectl rollout undo deployment/<名前>`で以前のバージョンにロールバックし、Podが元のイメージに戻ることも検証します。これらの操作により、Deploymentを用いることでアプリケーションの継続稼働とアップデート管理が容易になることを体感します。
        
12. **サービス(Service)によるPodのアクセス公開とロードバランシング**
    
    - **目的**: KubernetesにおけるServiceリソースの役割を理解し、Pod集合へのネットワークアクセス方法を習得します。Serviceを使って内部・外部から安定したアクセスポイントを提供し、複数Pod間でのロードバランシングやサービスディスカバリが可能になることを学ぶのが目的です。
        
    - **使用マニフェスト**: `Service`（`apiVersion: v1`）のYAMLマニフェスト。Express API Deploymentで起動したPod（ラベルで選択）を対象に、`spec.selector`にPodのラベルを指定します。まずはクラスター内部向けのClusterIPタイプでポート8000をエクスポートし、必要に応じて外部アクセス用に`type: NodePort`を指定します ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,Connecting%20applications%20with%20Services))（NodePortを30000番台に固定設定しておけばEC2の該当ポートを解放することで外部アクセスも可能になります）。`.spec.ports`で`port: 8000`とし、ターゲットの`targetPort: 8000`をExpressコンテナのポートに合わせます。
        
    - **確認内容**: `kubectl apply -f service.yaml`でService作成後、`kubectl get svc <名前>`でサービスが作成され、クラスタ内部IPとポートが割り当てられたことを確認します ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,Connecting%20applications%20with%20Services))。`ENDPOINTS`欄にPodのIPが表示されていれば対象Podが正しく紐付いています。ClusterIP型サービスの場合、クラスター内別Pod（例：busybox）から`wget http://<ClusterIP>:8000`でExpressサービスにアクセスし、レスポンスを得られることを確認します。NodePort型の場合、EC2のNodeのIPおよび割り当てポートに対しホストOSから`curl`して応答を確認します（本環境ではポート8000を開放済みなので、NodePortが例えば30080ならEC2のセキュリティグループで30080も許可するか、もしくはServiceのnodePortを8000に設定してアクセスします）。複数Podのレプリカがある場合は、Service経由でリクエストを複数回送り、背後でロードバランシングされ各Podに分散される様子（レスポンスにホスト名を出すなどして確認）も検証します。これにより、Serviceを介してPod群へ安定したアクセスが提供されることを学びます ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,Connecting%20applications%20with%20Services))。
        
13. **Ingressによる外部からのHTTPアクセス制御**
    
    - **目的**: Ingressリソースを利用して、クラスター外部から内部ServiceへのHTTP/HTTPSアクセスを集約制御する方法を学びます。IngressとIngressコントローラを用いることで、ロードバランシングやリバースプロキシ設定をKubernetesネイティブに管理できることを理解するのが目的です ([Ingress | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/ingress/#:~:text=Ingress%E3%81%AF%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%A4%96%E3%81%8B%E3%82%89%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%86%85Service%E3%81%B8%E3%81%AEHTTP%E3%81%A8HTTPS%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%88%E3%82%92%E5%85%AC%E9%96%8B%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%83%88%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AFIn%20gress%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E4%B8%8A%E3%81%A7%E5%AE%9A%E7%BE%A9%E3%81%95%E3%82%8C%E3%82%8B%E3%83%AB%E3%83%BC%E3%83%AB%E3%81%AB%E3%82%88%E3%81%A3%E3%81%A6%E5%88%B6%E5%BE%A1%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **使用マニフェスト**: `Ingress`（`apiVersion: networking.k8s.io/v1`）のYAMLマニフェスト。まずクラスターにIngressコントローラ（例：NGINX Ingress Controller）がデプロイされている前提で、Express ServiceへのルーティングルールをIngressリソースで定義します。`.spec.rules`にホスト名やパスを記述し、例えば`/api/*`パスのトラフィックをExpress Serviceの8000番ポートに転送するよう設定します ([Ingress | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/ingress/#:~:text=Ingress%E3%81%AF%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%A4%96%E3%81%8B%E3%82%89%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%86%85Service%E3%81%B8%E3%81%AEHTTP%E3%81%A8HTTPS%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%88%E3%82%92%E5%85%AC%E9%96%8B%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%83%88%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AFIn%20gress%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E4%B8%8A%E3%81%A7%E5%AE%9A%E7%BE%A9%E3%81%95%E3%82%8C%E3%82%8B%E3%83%AB%E3%83%BC%E3%83%AB%E3%81%AB%E3%82%88%E3%81%A3%E3%81%A6%E5%88%B6%E5%BE%A1%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))（テスト環境ではホスト名は省略可能なのでパスベースで設定）。TLSを試す場合は自己署名証明書のSecretを作成し、Ingressの`.spec.tls`に指定します。
        
    - **確認内容**: Ingressリソース適用後、`kubectl get ingress <名前>`でADDRESS（IngressコントローラのIP）や設定が反映されていることを確認します。EC2上でIngressコントローラが稼働しポート80/443が許可されていれば、ブラウザから`http://<EC2のホスト>/api/`でExpress APIにアクセスでき、Ingress経由でServiceにルーティングされることを確認します ([Ingress | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/ingress/#:~:text=Ingress%E3%81%AF%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%A4%96%E3%81%8B%E3%82%89%E3%82%AF%E3%83%A9%E3%82%B9%E3%82%BF%E3%83%BC%E5%86%85Service%E3%81%B8%E3%81%AEHTTP%E3%81%A8HTTPS%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%88%E3%82%92%E5%85%AC%E9%96%8B%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%83%88%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AFIn%20gress%E3%83%AA%E3%82%BD%E3%83%BC%E3%82%B9%E4%B8%8A%E3%81%A7%E5%AE%9A%E7%BE%A9%E3%81%95%E3%82%8C%E3%82%8B%E3%83%AB%E3%83%BC%E3%83%AB%E3%81%AB%E3%82%88%E3%81%A3%E3%81%A6%E5%88%B6%E5%BE%A1%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))（本環境では必要に応じてEC2のセキュリティグループにポートを追加許可）。もし外部アクセスが難しい場合は、IngressコントローラのServiceを`NodePort`にしてcurlで確認するか、別PodからIngressの`<hostname>/api`に対しHTTPリクエストを送りHTTP 200が返ることを確認します。Ingressによって、複数サービスへの経路を一元管理できること、またパスやホストベースのルーティング・TLS終端が実現できていることを検証します ([Ingress | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/ingress/#:~:text=Ingress%E3%81%AF%E8%B2%A0%E8%8D%B7%E5%88%86%E6%95%A3%E3%80%81SSL%E7%B5%82%E7%AB%AF%E3%80%81%E5%90%8D%E5%89%8D%E3%83%99%E3%83%BC%E3%82%B9%E3%81%AE%E4%BB%AE%E6%83%B3%E3%83%9B%E3%82%B9%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AE%E6%A9%9F%E8%83%BD%E3%82%92%E6%8F%90%E4%BE%9B%E3%81%97%E3%81%BE%E3%81%99%E3%80%82))。
        
14. **NetworkPolicyによる通信制御**
    
    - **目的**: ネットワークポリシーを用いてPod間通信の許可/拒否を細かく制御する方法を学びます。デフォルトではオープンなPod間ネットワークに対し、NetworkPolicyリソースでアクセスをホワイトリスト方式に絞り、安全なアプリケーション間通信を構築できることを理解するのが目的です ([ネットワークポリシー | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/network-policies/#:~:text=etes%E3%81%AE%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%82%92%E6%A4%9C%E8%A8%8E%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%E3%80%82%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%81%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E4%B8%AD%E5%BF%83%E3%81%AE%E6%A7%8B%E9%80%A0%E3%81%A7%E3%81%82%E3%82%8A%E3%80%81Pod%E3%81%8C%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%92%E4%BB%8B%E3%81%97%E3%81%A6%E5%A4%9A%20%E6%A7%98%E3%81%AA%E3%80%8C%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%80%8D))。
        
    - **使用マニフェスト**: `NetworkPolicy`（`apiVersion: networking.k8s.io/v1`）のYAMLマニフェスト。まずExpress API Podが属するNamespaceに対し、全てのIngress通信をデフォルト拒否するポリシーを定義します（`podSelector: {}`で全Pod対象、`ingress: []`空リストで全拒否）。次に、特定のラベルを持つPodからの通信のみ許可するルールを追加します（例：`from`に`podSelector: <ラベル>`を指定し、Express APIサービスのポート8000へのIngressを許可）。必要に応じてEgressルールも同様に定義します ([ネットワークポリシー | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/network-policies/#:~:text=etes%E3%81%AE%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%82%92%E6%A4%9C%E8%A8%8E%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%E3%80%82%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%81%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E4%B8%AD%E5%BF%83%E3%81%AE%E6%A7%8B%E9%80%A0%E3%81%A7%E3%81%82%E3%82%8A%E3%80%81Pod%E3%81%8C%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%92%E4%BB%8B%E3%81%97%E3%81%A6%E5%A4%9A%20%E6%A7%98%E3%81%AA%E3%80%8C%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%80%8D))。
        
    - **確認内容**: NetworkPolicy適用前後で通信の挙動が変わることを検証します。まず適用前に、任意のPod（BusyBoxなど）からExpress ServiceのClusterIP:8000へ`wget`して成功することを確認します。次にNetworkPolicyを`kubectl apply`し、再度同じ操作を行うとタイムアウトになる（通信拒否される）ことを確認します。また、許可したラベルを持つPodを新たに作成し（例：`kubectl run test --labels app=test --image=busybox`）、そこからはExpress APIにアクセス可能であることを確認します。`kubectl describe networkpolicy <名前>`でポリシーの内容を再確認し、意図したPodセレクタとポートが設定されていることも確認します。以上により、NetworkPolicyによりPod間のネットワークアクセスが制限できることを理解します ([ネットワークポリシー | Kubernetes](https://kubernetes.io/ja/docs/concepts/services-networking/network-policies/#:~:text=etes%E3%81%AE%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%82%92%E6%A4%9C%E8%A8%8E%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%E3%80%82%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%81%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E4%B8%AD%E5%BF%83%E3%81%AE%E6%A7%8B%E9%80%A0%E3%81%A7%E3%81%82%E3%82%8A%E3%80%81Pod%E3%81%8C%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%92%E4%BB%8B%E3%81%97%E3%81%A6%E5%A4%9A%20%E6%A7%98%E3%81%AA%E3%80%8C%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%80%8D))。
        
15. **ヘルスチェック(プローブ)の設定と動作確認**
    
    - **目的**: KubernetesのLivenessProbeとReadinessProbeを設定し、アプリケーションのヘルスチェックを自動化する方法を学びます。適切なプローブ設定によって、アプリケーションの自己復旧とサービス公開制御が行われる仕組みを理解することが目的です。
        
    - **使用マニフェスト**: Express APIコンテナの定義に`livenessProbe`および`readinessProbe`セクションを追加します ([Kubernetes: Liveness probeと Readiness probeについて - Qiita](https://qiita.com/KentOhwada_AlibabaCloudJapan/items/f9261806e441e6cf4001#:~:text=Kubernetes%3A%20Liveness%20probe%E3%81%A8%20Readiness%20probe%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6,Qiita%20liveness%20probe%E3%81%AF%E3%80%81pod%E3%81%8C%E7%94%9F%E5%AD%98%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E3%81%A9%E3%81%86%E3%81%8B%E3%82%92%E3%83%81%E3%82%A7%E3%83%83%E3%82%AF%E3%81%97%E3%80%81readiness%20probe%E3%81%AF%E3%80%81pod%E3%81%8C%E5%A4%96%E9%83%A8%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%82%92%E6%8F%90%E4%BE%9B%E3%81%99%E3%82%8B%E6%BA%96%E5%82%99%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E3%81%A9%E3%81%86%E3%81%8B%E3%82%92%E3%83%81%E3%82%A7%E3%83%83%E3%82%AF%E3%81%97%E3%81%BE%E3%81%99))。例えば、`httpGet`プローブを使い、`/metrics`や`/health`エンドポイント（なければ`/posts`など応答があるURL）に対してプローブする設定を記述します。`initialDelaySeconds`, `periodSeconds`, `failureThreshold`等も適宜設定します。ReadinessProbeではExpress起動直後は一時的に`NotReady`とみなすよう`initialDelaySeconds`を短めにし、LivenessProbeでは応答がなくなった場合にコンテナ再起動させるようにします ([Liveness Probe、Readiness ProbeおよびStartup Probeを使用する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#:~:text=kubelet%E3%81%AF%E3%80%81Readiness%20Probe%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E3%83%88%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%82%92%E5%8F%97%E3%81%91%E5%85%A5%E3%82%8C%E3%82%89%E3%82%8C%E3%82%8B%E7%8A%B6%E6%85%8B%E3%81%A7%E3%81%82%E3%82%8B%E3%81%8B%E3%82%92%E8%AA%8D%E8%AD%98%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20Pod%E3%81%8C%E6%BA%96%E5%82%99%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%84%E3%82%8B%E3%81%A8%E8%A6%8B%E3%81%AA%E3%81%95%E3%82%8C%E3%82%8B%E3%81%AE%E3%81%AF%E3%80%81Pod%E5%86%85%E3%81%AE%E5%85%A8%E3%81%A6%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%BA%96%E5%82%99%E3%81%8C%E6%95%B4%E3%81%A3%E3%81%9F%E3%81%A8%E3%81%8D%E3%81%A7%E3%81%99%E3%80%82%20%E4%B8%80%E4%BE%8B%E3%81%A8%E3%81%97%E3%81%A6%E3%80%81%E3%81%93%E3%81%AE%E3%82%B7%E3%82%B0%E3%83%8A%E3%83%AB%E3%81%AFService%E3%81%AE%E3%83%90%E3%83%83%E3%82%AF%E3%82%A8%E3%83%B3%E3%83%89%E3%81%A8%E3%81%97%E3%81%A6%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BPod%E3%82%92%E5%88%B6%E5%BE%A1%E3%81%99%E3%82%8B%E3%81%A8%E3%81%8D%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82%20Pod%E3%81%AE%E6%BA%96%E5%82%99%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%84%E3%81%AA%E3%81%84%E5%A0%B4%E5%90%88%E3%80%81%E3%81%9D%E3%81%AEPod%E3%81%AFService%E3%81%AE%E3%83%AD%E3%83%BC%E3%83%89%E3%83%90%E3%83%A9%E3%83%B3%E3%82%B7%E3%83%B3%E3%82%B0%E3%81%8B%E3%82%89%E5%88%87%E3%82%8A%E9%9B%A2%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82)) ([Liveness Probe、Readiness ProbeおよびStartup Probeを使用する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#:~:text=kubelet%E3%81%AF%E3%80%81Liveness%20Probe%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%92%E3%81%84%E3%81%A4%E5%86%8D%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B%E3%81%8B%E3%82%92%E8%AA%8D%E8%AD%98%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20%E4%BE%8B%E3%81%88%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E8%87%AA%E4%BD%93%E3%81%AF%E8%B5%B7%E5%8B%95%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8C%E3%80%81%E5%87%A6%E7%90%86%E3%82%92%E7%B6%99%E7%B6%9A%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%AA%E3%81%84%E3%83%87%E3%83%83%E3%83%89%E3%83%AD%E3%83%83%E3%82%AF%E7%8A%B6%E6%85%8B%E3%82%92%E6%A4%9C%E7%9F%A5%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E7%8A%B6%E6%85%8B%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%92%E5%86%8D%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%A7%E3%80%81%E3%83%90%E3%82%B0%E3%81%8C%E3%81%82%E3%82%8B%E5%A0%B4%E5%90%88%E3%81%A7%E3%82%82%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E5%8F%AF%E7%94%A8%E6%80%A7%E3%82%92%E9%AB%98%E3%82%81%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **確認内容**: Pod起動後、`kubectl describe pod <Pod名>`でプローブの設定が適用されていることを確認し、しばらく待ってから`kubectl get pods`でPodの`READY`列が適切に反映されていることを確認します（readinessプローブ成功までは`0/1`、成功後に`1/1`となる）。意図的にプローブを失敗させるテストも行います。例えばLivenessProbeのパスを存在しないものに変更し`kubectl apply`で更新すると、一定回数失敗後に`kubectl describe pod`のイベントに「Liveness probe failed」が記録され、コンテナが再起動される（RESTARTSカウンタが増える）ことを確認します ([Liveness Probe、Readiness ProbeおよびStartup Probeを使用する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#:~:text=kubelet%E3%81%AF%E3%80%81Liveness%20Probe%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%92%E3%81%84%E3%81%A4%E5%86%8D%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B%E3%81%8B%E3%82%92%E8%AA%8D%E8%AD%98%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20%E4%BE%8B%E3%81%88%E3%81%B0%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E8%87%AA%E4%BD%93%E3%81%AF%E8%B5%B7%E5%8B%95%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8C%E3%80%81%E5%87%A6%E7%90%86%E3%82%92%E7%B6%99%E7%B6%9A%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%AA%E3%81%84%E3%83%87%E3%83%83%E3%83%89%E3%83%AD%E3%83%83%E3%82%AF%E7%8A%B6%E6%85%8B%E3%82%92%E6%A4%9C%E7%9F%A5%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82%20%E3%81%93%E3%81%AE%E3%82%88%E3%81%86%E3%81%AA%E7%8A%B6%E6%85%8B%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%92%E5%86%8D%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%A7%E3%80%81%E3%83%90%E3%82%B0%E3%81%8C%E3%81%82%E3%82%8B%E5%A0%B4%E5%90%88%E3%81%A7%E3%82%82%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E5%8F%AF%E7%94%A8%E6%80%A7%E3%82%92%E9%AB%98%E3%82%81%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。ReadinessProbe失敗時は`kubectl get endpoints`で当該PodがServiceのエンドポイントから一時的に外れることも確認できます。これらにより、プローブ設定がPodの健全性維持やトラフィック制御に寄与することを学びます ([Liveness Probe、Readiness ProbeおよびStartup Probeを使用する | Kubernetes](https://kubernetes.io/ja/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#:~:text=kubelet%E3%81%AF%E3%80%81Readiness%20Probe%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E3%83%88%E3%83%A9%E3%83%95%E3%82%A3%E3%83%83%E3%82%AF%E3%82%92%E5%8F%97%E3%81%91%E5%85%A5%E3%82%8C%E3%82%89%E3%82%8C%E3%82%8B%E7%8A%B6%E6%85%8B%E3%81%A7%E3%81%82%E3%82%8B%E3%81%8B%E3%82%92%E8%AA%8D%E8%AD%98%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%20Pod%E3%81%8C%E6%BA%96%E5%82%99%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%84%E3%82%8B%E3%81%A8%E8%A6%8B%E3%81%AA%E3%81%95%E3%82%8C%E3%82%8B%E3%81%AE%E3%81%AF%E3%80%81Pod%E5%86%85%E3%81%AE%E5%85%A8%E3%81%A6%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%BA%96%E5%82%99%E3%81%8C%E6%95%B4%E3%81%A3%E3%81%9F%E3%81%A8%E3%81%8D%E3%81%A7%E3%81%99%E3%80%82%20%E4%B8%80%E4%BE%8B%E3%81%A8%E3%81%97%E3%81%A6%E3%80%81%E3%81%93%E3%81%AE%E3%82%B7%E3%82%B0%E3%83%8A%E3%83%AB%E3%81%AFService%E3%81%AE%E3%83%90%E3%83%83%E3%82%AF%E3%82%A8%E3%83%B3%E3%83%89%E3%81%A8%E3%81%97%E3%81%A6%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%82%8BPod%E3%82%92%E5%88%B6%E5%BE%A1%E3%81%99%E3%82%8B%E3%81%A8%E3%81%8D%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82%20Pod%E3%81%AE%E6%BA%96%E5%82%99%E3%81%8C%E3%81%A7%E3%81%8D%E3%81%A6%E3%81%84%E3%81%AA%E3%81%84%E5%A0%B4%E5%90%88%E3%80%81%E3%81%9D%E3%81%AEPod%E3%81%AFService%E3%81%AE%E3%83%AD%E3%83%BC%E3%83%89%E3%83%90%E3%83%A9%E3%83%B3%E3%82%B7%E3%83%B3%E3%82%B0%E3%81%8B%E3%82%89%E5%88%87%E3%82%8A%E9%9B%A2%E3%81%95%E3%82%8C%E3%81%BE%E3%81%99%E3%80%82))。
        
16. **ログ管理とデバッグ（kubectl logs/exec やエフェメラルコンテナ）**
    
    - **目的**: 実行中のコンテナのログ収集とコンテナ内デバッグ方法を習得します。`kubectl logs`や`kubectl exec`による基本的なトラブルシュートに加え、必要に応じてエフェメラルコンテナを利用したデバッグ手法を理解し、CKAD試験で求められるアプリケーションデバッグスキルを身につけることが目的です。
        
    - **使用マニフェスト**: 既存のExpress Deploymentを利用（新たなマニフェストは不要）します。エフェメラルコンテナを試す場合、公式にはPodのマニフェスト変更ではなく`kubectl debug`コマンドを使用します。例えば`kubectl debug -it <Pod名> --image=busybox --target=<コンテナ名>`のようにして、BusyBoxシェルを持つエフェメラルコンテナを対象Podに追加します ([エフェメラルコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/ephemeral-containers/#:~:text=%E3%81%93%E3%81%AE%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%A7%E3%81%AF%E3%80%81%E7%89%B9%E5%88%A5%E3%81%AA%E7%A8%AE%E9%A1%9E%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%82%E3%82%8B%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%A6%82%E8%A6%81%E3%82%92%E8%AA%AC%E6%98%8E%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AA%E3%81%A9%E3%81%AE%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%81%8C%E9%96%8B%E5%A7%8B%E3%81%99%E3%82%8B%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%20%E3%83%B3%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E3%80%81%E3%81%99%E3%81%A7%E3%81%AB%E5%AD%98%E5%9C%A8%E3%81%99%E3%82%8BPod%E5%86%85%E3%81%A7%E4%B8%80%E6%99%82%E7%9A%84%E3%81%AB%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%99%E3%80%82%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E6%A7%8B%E7%AF%89%E3%81%A7%E3%81%AF%E3%81%AA%E3%81%8F%E3%80%81service%E3%81%AE%E8%AA%BF%E6%9F%BB%20%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AB%E5%88%A9%E7%94%A8%E3%81%97%E3%81%BE%E3%81%99%E3%80%82))。
        
    - **確認内容**: まず`kubectl logs <Pod名>`でExpressコンテナの標準出力ログが取得できることを確認します。Expressアプリにリクエストを送り、そのリクエストログが`kubectl logs`出力に現れることを見て、ログ監視の手法を確認します。次に`kubectl exec -it <Pod名> -- /bin/sh`でコンテナ内シェルに入り、簡単な調査（環境変数確認や依存サービスへの疎通確認など）を実施します。さらに、コンテナイメージにデバッグツールが含まれていないケースを想定し、`kubectl debug`コマンドでエフェメラルコンテナを追加してみます。追加後、`kubectl get pods <Pod名> -o yaml`で`ephemeralContainers`セクションにデバッグコンテナが存在することを確認し、そのコンテナ内で必要なツール（例えば`curl`や`ps`コマンドなど）を使った調査を行います ([エフェメラルコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/ephemeral-containers/#:~:text=%E3%81%93%E3%81%AE%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%A7%E3%81%AF%E3%80%81%E7%89%B9%E5%88%A5%E3%81%AA%E7%A8%AE%E9%A1%9E%E3%81%AE%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%82%E3%82%8B%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E6%A6%82%E8%A6%81%E3%82%92%E8%AA%AC%E6%98%8E%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AA%E3%81%A9%E3%81%AE%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%81%8C%E9%96%8B%E5%A7%8B%E3%81%99%E3%82%8B%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%20%E3%83%B3%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AB%E3%80%81%E3%81%99%E3%81%A7%E3%81%AB%E5%AD%98%E5%9C%A8%E3%81%99%E3%82%8BPod%E5%86%85%E3%81%A7%E4%B8%80%E6%99%82%E7%9A%84%E3%81%AB%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7%E3%81%99%E3%80%82%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E6%A7%8B%E7%AF%89%E3%81%A7%E3%81%AF%E3%81%AA%E3%81%8F%E3%80%81service%E3%81%AE%E8%AA%BF%E6%9F%BB%20%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AB%E5%88%A9%E7%94%A8%E3%81%97%E3%81%BE%E3%81%99%E3%80%82)) ([エフェメラルコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/ephemeral-containers/#:~:text=match%20at%20L888%20%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E3%82%AF%E3%83%A9%E3%83%83%E3%82%B7%E3%83%A5%E3%81%97%E3%81%A6%E3%81%97%E3%81%BE%E3%81%A3%E3%81%9F%E3%82%8A%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E3%83%87%E3%83%90%E3%83%83%E3%82%B0%E7%94%A8%E3%83%A6%E3%83%BC%E3%83%86%E3%82%A3%E3%83%AA%E3%83%86%E3%82%A3%E3%81%8C%E5%90%8C%E6%A2%B1%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%AA%E3%81%84%E5%A0%B4%E5%90%88%E3%81%AA%E3%81%A9%E3%80%81,%E3%81%A7%E3%81%AF%E4%B8%8D%E5%8D%81%E5%88%86%E3%81%AA%E3%81%A8%E3%81%8D%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%83%96%E3%81%AA%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%92%E8%A1%8C%E3%81%86%E3%81%9F%E3%82%81%E3%81%AB%E5%BD%B9%E7%AB%8B%E3%81%A1%E3%81%BE%E3%81%99%E3%80%82))。調査終了後、Podを削除すればエフェメラルコンテナも消滅します。以上の手順で、Kubernetes環境下でのログ確認とオンザフライなデバッグ方法を習得し、問題発生時に適切に対処できるスキルを養います ([エフェメラルコンテナ | Kubernetes](https://kubernetes.io/ja/docs/concepts/workloads/pods/ephemeral-containers/#:~:text=match%20at%20L888%20%E3%82%A8%E3%83%95%E3%82%A7%E3%83%A1%E3%83%A9%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AF%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%8C%E3%82%AF%E3%83%A9%E3%83%83%E3%82%B7%E3%83%A5%E3%81%97%E3%81%A6%E3%81%97%E3%81%BE%E3%81%A3%E3%81%9F%E3%82%8A%E3%80%81%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB%E3%83%87%E3%83%90%E3%83%83%E3%82%B0%E7%94%A8%E3%83%A6%E3%83%BC%E3%83%86%E3%82%A3%E3%83%AA%E3%83%86%E3%82%A3%E3%81%8C%E5%90%8C%E6%A2%B1%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%AA%E3%81%84%E5%A0%B4%E5%90%88%E3%81%AA%E3%81%A9%E3%80%81,%E3%81%A7%E3%81%AF%E4%B8%8D%E5%8D%81%E5%88%86%E3%81%AA%E3%81%A8%E3%81%8D%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%83%96%E3%81%AA%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%92%E8%A1%8C%E3%81%86%E3%81%9F%E3%82%81%E3%81%AB%E5%BD%B9%E7%AB%8B%E3%81%A1%E3%81%BE%E3%81%99%E3%80%82))。