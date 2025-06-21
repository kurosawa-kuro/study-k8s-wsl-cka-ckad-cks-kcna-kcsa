### ✅ CKAD対策テーマ表 v3（カテゴリ付き・一枚表）

|カテゴリ|チュートリアルテーマ|推奨イメージ例|理由・出題傾向|Ingress必要？|
|---|---|---|---|---|
|🧱 Pod操作|Pod基礎|`nginx`, `busybox`|起動・再起動・yaml操作練習に最適な標準公式イメージ|❌|
|🧱 Pod操作|マルチコンテナPod（サイドカー）|`nginx` + `busybox`|ログやバッチ系処理との組み合わせテストで十分|△|
|🔁 Job/CronJob|Job|`busybox`|一時的な`echo`や`sleep`を実行。出題頻度高|❌|
|🔁 Job/CronJob|CronJob|`busybox`|1分ごとの定期タスク（ps auxなど）|△|
|🧩 Config/Probe/Volume|ConfigMap / Secret|**`bitnami/express`（必要時）**, `nginx`|`/env`などの反映確認を明確にしたい場合にbitnami/express、通常はnginxで可|✅|
|🧩 Config/Probe/Volume|Probe（Liveness / Readiness）|**`bitnami/express`（必要時）**, `nginx`|`/live`, `/ready`レスポンス確認にHTTPサーバーが必要。nginxでも可|✅|
|🧩 Config/Probe/Volume|Volume / PVC|`nginx`, `redis`, `busybox`|emptyDir / hostPath / PVCマウントで構成しやすい|△|
|🌐 ネットワーク|Service / Ingress|`nginx`, `httpd`|HTTPサーバーとしてルーティング検証に最適|✅（必須）|
|🌐 ネットワーク|NetworkPolicy|`nginx` + `busybox`|busyboxからcurlする通信確認で出題される|✅|
|🔐 セキュリティ|SecurityContext|`busybox`, `redis:alpine`|UID/CAPテスト用、シンプルに記述可能|❌|
|🔐 セキュリティ|RBAC|`bitnami/kubectl`|ServiceAccount / get pods 権限の動作確認に専用|❌|
|🔍 調査・デバッグ|ログ / exec / debug|`nginx`, `busybox`, **`bitnami/express`（必要時）**|`kubectl logs`や`exec`による動作確認に適|△|
|🔁 デプロイ戦略|Deployment戦略（RollingUpdate）|`redis:alpine`, `nginx`|maxSurge, maxUnavailable 設定テスト|❌|
|🔧 リソース制御|リソース制限（LimitRange）|`nginx`, `alpine`|CPU/メモリ制限構文の確認|❌|
|🧪 応用デプロイ|Canary Deployment|`nginx`, **`bitnami/express`（必要時）**|labelごとのPod分離＋20%配分確認（視覚レスポンス不要ならnginxで十分）|✅|
|💾 ストレージ|PVC→PV Pending修正|`nginx`, `redis`|PV/PVCのBound条件理解用|❌|
|🐞 障害調査|Pod起動失敗の調査|`redis:alpine`, `nginx`|イメージタグや構文エラー調査に頻出|❌|

---

**CKA（Certified Kubernetes Administrator）対策向けに構成した表**です。  
CKADと異なり、クラスタ管理・トラブルシューティング・コントロールプレーン操作など**管理者視点の内容**を中心に、カテゴリ付きで整理しています。

---

### ✅ CKA対策チュートリアル一覧（カテゴリ付き・一枚表）

| カテゴリ             | チュートリアルテーマ                              | 推奨イメージ例                      | 理由・出題傾向                                                              | Ingress必要？ |
| ---------------- | --------------------------------------- | ---------------------------- | -------------------------------------------------------------------- | ---------- |
| ⚙️ クラスタ構築・修復     | `kubeadm`によるクラスタ構築                      | -                            | `kubeadm init` / `join` / `reset` 実行。クラスタ構成の基本                       | ❌          |
| ⚙️ クラスタ構築・修復     | コントロールプレーンの静的Pod修正（manifest編集）          | -                            | `/etc/kubernetes/manifests` 配下でのマニフェスト編集・自動再起動の確認                    | ❌          |
| ⚙️ クラスタ構築・修復     | etcd バックアップと復元                          | -                            | `etcdctl` コマンドによるバックアップ／復元操作。証明書付き接続も含む                              | ❌          |
| 🔧 ノード操作         | ノードのDrain / Cordon / Uncordon           | -                            | ノード障害時の対応操作。Pod再スケジュールの確認に必須                                         | ❌          |
| 🔧 ノード操作         | kubelet 設定変更と再起動                        | -                            | `/var/lib/kubelet/config.yaml` 編集 → `systemctl restart kubelet` 実行など | ❌          |
| 🔧 ノード操作         | ログ・メトリクス調査                              | -                            | `journalctl -u kubelet` や `/var/log` 調査、Podイベント解析                    | ❌          |
| 📦 Pod管理         | Static Pod の直接定義                        | `nginx`, `busybox`           | コントロールプレーン経由でなく、Node直下にPod定義ファイルを配置                                  | ❌          |
| 🔁 Podスケジューリング   | nodeSelector / affinity / anti-affinity | `nginx`, `busybox`           | 指定ノードへのPod配置を実践的に確認                                                  | ❌          |
| 🔁 Podスケジューリング   | Taints / Tolerations                    | `nginx`, `busybox`           | 汚染されたノードへのスケジュール制御                                                   | ❌          |
| 🔒 セキュリティと認証     | TLS証明書のローテーション確認                        | -                            | kubeletの自動証明書更新の仕組み理解                                                | ❌          |
| 🔒 セキュリティと認証     | TLS bootstrapping                       | -                            | `bootstrap.kubeconfig` からのkubelet登録                                  | ❌          |
| 🔒 セキュリティと認証     | Certificate Signing Request (CSR) の承認   | -                            | `kubectl certificate approve` の使用など                                  | ❌          |
| 🔐 RBAC / セキュリティ | Role / ClusterRole / Binding の作成        | `bitnami/kubectl`            | 権限委譲テスト：namespace限定とクラスタ全体の使い分け                                      | ❌          |
| 📄 マニフェスト管理      | リソースの編集 / パッチ適用                         | `nginx`, `busybox`           | `kubectl edit`, `patch`, `replace` の違いを確認                            | ❌          |
| 🧪 調査・復旧         | Pod / Service / Deployment のトラブルシュート    | `nginx`, `redis`, `busybox`  | イメージPull失敗、PVC Pending、ラベル不一致など実際の障害再現で経験値を積む                        | △（構成による）   |
| 📡 ネットワークとDNS    | CoreDNSの設定調査と修復                         | `busybox`, `alpine`          | 名前解決不全時の `/etc/coredns/Corefile` 修正や再起動                              | ❌          |
| 📡 ネットワークとDNS    | ネットワーク疎通確認（nslookup / dig / curl）       | `busybox`, `curlimages/curl` | クラスタ内外の名前解決と疎通確認                                                     | ❌          |
| 📜 監査とロギング       | Audit Policy 設定と有効化                     | -                            | `audit-policy.yaml` によるAPIアクセスログ収集設定                                 | ❌          |
| 📁 ストレージ管理       | PV/PVC/StorageClass 定義とマッチング            | `nginx`, `redis`             | `accessModes`, `storageClassName` の一致とPending解消                      | ❌          |

---
