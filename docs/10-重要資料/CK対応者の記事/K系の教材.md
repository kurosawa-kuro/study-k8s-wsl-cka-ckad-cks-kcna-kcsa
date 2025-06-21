以下に **KCNA** と **KCSA** それぞれの学習教材を「日本語対応 ◎／英語のみ ○」という観点でまとめました。
英会話は不要で、動画のリスニングと資料読解ができれば十分に回せる内容だけを選んでいます。

---

## 🐣 KCNA（Kubernetes & Cloud Native Associate）

| カテゴリ  | 教材                                                            | 言語   | メモ                                                                              |
| ----- | ------------------------------------------------------------- | ---- | ------------------------------------------------------------------------------- |
| 基礎講座  | **Linux Foundation公式 LFS250-JP** <br>「Kubernetesとクラウドネイティブ基礎」 | 日本語◎ | 本家の日本語版e-ラーニング。8〜10 hでKCNA範囲を網羅し、試験バンドルも選択可 ([training.linuxfoundation.org][1]) |
| ハンズオン | **KodeKloud KCNAコース**                                         | 英語○  | ブラウザだけで演習できる実機ラボ＋小テスト。解説は英語でも CLI 操作が中心なので聞き取り負荷は低い ([kodekloud.com][2])        |
| 模擬試験  | **Udemy Mock Exams（6回分）**                                     | 英語○  | 1回60問×90分で本番を忠実に再現。和訳は無いが問われる単語は試験本番と同じなので慣れに最適 ([udemy.com][3])                |
| 参考書   | **“Becoming KCNA Certified”**（D. Galkin）                      | 英語○  | 全ドメインをコンパクトにまとめた電子書籍。図版多めで読みやすい ([dev.to][4])                                   |
| 無料ガイド | **KCNA Exam Prep Guide（GitHub）**                              | 英語○  | ドメインごとに重要コマンドと Kubernetes docs へのリンクを整理 ([wrijugh.github.io][5])                |

> **試験言語**
> KCNA は **日本語版（KCNA-JP）** が用意されており、受験中に日⇔英で表示を切替可能。
> ただし監督官とのやり取りは英語チャット／英語音声のみです ([training.linuxfoundation.org][6])

---

## 🔐 KCSA（Kubernetes & Cloud Native Security Associate）

| カテゴリ    | 教材                                          | 言語       | メモ                                                                              |
| ------- | ------------------------------------------- | -------- | ------------------------------------------------------------------------------- |
| 公式情報    | **KCSA 試験ページ**                              | 英語○／日訳△  | 出題ドメインと試験要項。まずここで範囲確認 ([training.linuxfoundation.org][7])                       |
| 基礎＋演習   | **KodeKloud KCSAコース**                       | 英語○      | Trivy, Falco, Kyverno など OSS ツールの実機ラボ付き ([kodekloud.com][8])                    |
| 動画講座    | **LinkedIn Learning “KCSA Cert Prep”**      | 英語字幕○    | セキュリティベストプラクティスをデモ中心で解説。倍速視聴しても聞き取りやすい ([linkedin.com][9])                      |
| 模擬試験    | **KCSA Mock Exam Web App**                  | 英語○      | 有志が公開しているブラウザ模試（選択式）。無料で総仕上げに便利 ([kisama2000.cloud][10])                        |
| 体験談／まとめ | **Medium & Qiita 記事**                       | 日本語△／英語○ | 学習ログ・頻出トピックを俯瞰できる。英語版の試験しかない点への注意喚起あり ([medium.com][11], [qiita.com][12])       |
| 追加深掘り   | **LFS260 “Kubernetes Security Essentials”** | 英語○      | もともと CKS 用だが、Seccomp/AppArmor/PSS を体系的に学べる ([training.linuxfoundation.org][13]) |

> **言語面の注意**
> *2025年6月時点で KCSA-JP（日本語問題）は未提供*。問題文・UI とも英語のみなので、読解に自信がない場合は英単語リストを作ってから臨むと安心です ([qiita.com][12])

---

### 📌 使い分けのコツ

1. **日本語で概念 → 英語で演習**
   KCNA は LFS250-JP で全体像を掴み、演習は英語解説でもコマンド主体の KodeKloud に移る流れが効率的。
2. **KCSA は“実機→模試→復習”ループ**
   セキュリティ用語は聞き取りよりタイピングが多いので、動画を倍速視聴→ラボ→Web模試で用語定着を図る。
3. **字幕／トランスクリプトを最大活用**
   Udemy と LinkedIn Learning は英語字幕が出せる。聞き取れない単語は即停止→字幕確認→メモ。

---

### 次のアクション

* **演習リポジトリ** を GitHub に scaffold してお渡しすることも可能です（KCNA と KCSA でブランチ分け）。
* もし **模試ログを自動で日本語サマリ化** したい場合は、jq＋GPT スクリプト例も提供できます。

気になる教材やサポートがあれば、遠慮なくどうぞ！

[1]: https://training.linuxfoundation.org/training/kubernetes-and-cloud-native-essentials-lfs250-jp/?utm_source=chatgpt.com "Kuberbetesとクラウドネイティブ基礎 (LFS250-JP)"
[2]: https://kodekloud.com/courses/kubernetes-and-cloud-native-associate-kcna?utm_source=chatgpt.com "Kubernetes and Cloud-Native Associate (KCNA) - KodeKloud"
[3]: https://www.udemy.com/course/kubernetes-and-cloud-native-associate-kcna-exams/?srsltid=AfmBOooogYiUvKhqwRILdXXdDSaayUBdSGnpW4VauQLMKgiu9CNgY9Rc&utm_source=chatgpt.com "Kubernetes and Cloud Native Associate (KCNA) - Mock Exams"
[4]: https://dev.to/juliafmorgado/how-to-pass-the-kcna-kubernetes-and-cloud-native-associate-2hod?utm_source=chatgpt.com "How to Pass the KCNA - Kubernetes And Cloud Native Associate"
[5]: https://wrijugh.github.io/kcna/?utm_source=chatgpt.com "Exam Prep Guide for KCNA"
[6]: https://training.linuxfoundation.org/certification/kubernetes-and-cloud-native-associate-kcna-jp/?utm_source=chatgpt.com "Kubernetes and Cloud Native Associate (KCNA) Exam"
[7]: https://training.linuxfoundation.org/certification/kubernetes-and-cloud-native-security-associate-kcsa/?utm_source=chatgpt.com "Kubernetes and Cloud Native Security Associate (KCSA)"
[8]: https://kodekloud.com/courses/kubernetes-and-cloud-native-security-associate-kcsa?utm_source=chatgpt.com "Kubernetes and Cloud Native Security Associate (KCSA) - KodeKloud"
[9]: https://www.linkedin.com/learning/kubernetes-and-cloud-native-security-associate-kcsa-cert-prep?utm_source=chatgpt.com "Kubernetes and Cloud Native Security Associate (KCSA) Cert Prep"
[10]: https://kisama2000.cloud/roadtokubestronaut-fin/?utm_source=chatgpt.com "kubestronautへの道 ~完結編・勉強法総まとめ"
[11]: https://medium.com/%40wattsdave/kubernetes-cloud-native-security-associate-kcsa-study-notes-and-exam-prep-f4c8f84d1c4f?utm_source=chatgpt.com "Kubernetes & Cloud Native Security Associate (KCSA) Study Notes ..."
[12]: https://qiita.com/takahiro_fukushima/items/ca6872344e6513b33f3c?utm_source=chatgpt.com "Kubernetes and Cloud Native Security Associate (KCSA)に合格 - Qiita"
[13]: https://training.linuxfoundation.org/training/kubernetes-security-essentials-lfs260/?utm_source=chatgpt.com "Kubernetes Security Essentials (LFS260) - Linux Foundation"
