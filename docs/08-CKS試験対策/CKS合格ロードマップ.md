以下は **Certified Kubernetes Security Specialist（CKS）** に特化したロードマップです。
公式カリキュラムの最新ドメイン比率（2025 年6 月時点）を反映しています。([training.linuxfoundation.org][1])

---

## ✅ CKS 最速ロードマップ（7 日 “ぶっ通し” プラン）

> **前提**
>
> * CKA 合格済み（kubectl/kubeadm など基礎操作は体得済）
> * kind + vim + bash alias 環境あり
> * Trivy/Falco など OSS ツールは名前だけ知っている

| Day | ドメイン (比率)                            | 重点タスク                                                                               | 必須アウトプット                               |
| --- | ------------------------------------ | ----------------------------------------------------------------------------------- | -------------------------------------- |
| 1   | **Cluster Setup 15 %**               | \* CNI + NetworkPolicy 初期設定（Calico 例）<br>\* Ingress-Nginx + TLS & HSTS 有効化          | kind 3ノード構成を 30 分以内に再作成                |
| 2   | **Cluster Hardening 15 %**           | \* API Server RBAC 制限 / API Audit<br>\* デフォルト SA 無効化, PodSecurityAdmission enforced | CIS Bench benchmark スクリプトで “Info 0”    |
| 3   | **System Hardening 10 %**            | \* ノード OS 最小化（distroless）<br>\* seccomp / AppArmor プロファイル適用                         | AppArmor “baseline” → “restricted” を比較 |
| 4   | **Minimize Microservice Vulns 20 %** | \* PSP→PSS 移行シナリオ<br>\* Secret encryption at rest + external-secrets                | Pod 3種を 25 分以内に harden                 |
| 5   | **Supply Chain Security 20 %**       | \* SBOM (syft) 生成→cosign 署名→policy-controller 検証<br>\* imagePolicyWebhook シミュレート    | “break-glass” 対応フローを markdown 1枚       |
| 6   | **Monitoring/Logging/Runtime 20 %**  | \* Falco rule 書換え & test<br>\* Prometheus + Trivy Operator で CVE アラート               | 侵入検知アラート → Slack Webhook 通知            |
| 7   | **総合模試 ×2**                          | killer.sh / KodeKloud CKS ラボ                                                        | 15 問を 120 分 → 復習メモを 60 分で整理            |

---

## ✅ CKS じっくりロードマップ（14 日 “定着” プラン）

| 期間      | ゴール                            | 補足ポイント                                       |
| ------- | ------------------------------ | -------------------------------------------- |
| Day 1-2 | Cluster Setup & Ingress TLS    | kubeadm/kind の再構築をコピペ禁止で                     |
| Day 3-4 | NetworkPolicy & CNI 深掘り        | Calico → Cilium へ換装し eBPF 周辺を体験              |
| Day 5-6 | Cluster Hardening              | kube-api / etcd 証明書ローテーション手順書を作る             |
| Day 7   | System Hardening               | seccomp-profile-loader, AppArmor Loader を自動化 |
| Day 8   | PSS / Kyverno / OPA Gatekeeper | deny-by-default → namespace-level 例外許可       |
| Day 9   | Secrets & Key Management       | KMS provider (AWS KMS or HashiCorp Vault) 連携 |
| Day 10  | Supply Chain Security          | Tekton + cosign で 署名付き CI/CD パイプライン          |
| Day 11  | Runtime Security               | eBPF-based Falco Sidekick, Sysdig Inspect 基礎 |
| Day 12  | ログ & 監査                        | AuditPolicy を “requestResponse” にし Loki へ転送  |
| Day 13  | 模試①（killer.sh）                 | 正答率 ≤ 80 % を洗い出し再演習                          |
| Day 14  | 模試② & タイムマネジメント                | alias/.vimrc を本番仕様に凍結、2 h 完走練習               |

---

### 🧠 共通チートシート

```bash
# ~/.bashrc
alias k='kubectl'
alias kgp='kubectl get pods -o wide'
alias ksys='kubectl -n kube-system'
alias tscan='trivy image'
alias ftrace='falco --trace'

# ~/.vimrc
set ts=2 sts=2 sw=2 et
autocmd BufWritePost *.yaml !kaf %
```

* **画像署名フロー**

  1. `docker build -t app:v1 .`
  2. `cosign sign --key cosign.key app:v1`
  3. `kubectl annotate imagepolicy security.sigstore.dev/...`

* **PSS “restricted” 最速パッチ**

```yaml
kubectl label ns secure \
  pod-security.kubernetes.io/enforce=restricted \
  --overwrite
```

---

### 追加支援メニュー

| サービス             | 内容                                    |
| ---------------- | ------------------------------------- |
| 演習 YAML セット      | ドメイン別 “問題 → 解答” を GitHub repo 化       |
| 模試ログ分析シート        | 誤答原因 / 修正コマンドを CSV で自動生成              |
| Supply-Chain Lab | Tekton + cosign + Kyverno demo マニフェスト |

---

**ご希望のプランはどちらでしょうか？**
演習リポジトリや模試ログ整理もすぐ用意できますので、気軽にお知らせください！

[1]: https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/ "Certified Kubernetes Security Specialist (CKS) - Linux Foundation - Education"
