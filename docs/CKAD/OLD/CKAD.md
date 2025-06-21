下記をCKAD-JPにリファクタリング依頼
https://lpi.or.jp/k8s/

了解しました。2025年のゴールデンウィークに学習へ集中し、GW明けのCKAD受験を目標にした戦略ドキュメント（Markdown形式）を作成します。

以下を含めた内容で調査・構成を進めます：
- CKAD試験範囲に基づいたセクション別の学習ガイド
- GW期間（2025/4/27〜5/6）の集中学習スケジュール
- Udemyやオンライン環境など、実践的でおすすめの教材
- 各項目ごとにGPT向けの練習用プロンプトテンプレート
- 試験直前チェックリスト＆本番準備Tips

出来上がり次第、すぐにご案内いたします。

# CKAD試験対策ゴールデンウィーク学習戦略 (2025年) #

**目的:** 2025年のゴールデンウィーク（4/27〜5/6の10日間）を活用して、Certified Kubernetes Application Developer (CKAD) 試験の全範囲を集中的に学習し、連休明けに合格できる実力を養成するための戦略をまとめます。セクションごとに試験概要、学習計画、スケジュール、教材、演習方法、直前対策を整理しました。

---

## 1. CKAD試験概要と出題範囲の要点

**試験形式と概要:** CKAD試験はオンラインで実施される実技試験で、与えられたKubernetesクラスタ上でタスクを解決する形式です ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=1,Here%20are%20some%20essential%20details))。試験時間は**2時間**、出題数は**約15〜20問（通常16問）**です ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,upgraded%20with%20new%20Kubernetes%20versions))。合格には**66%前後のスコア**が必要で、不完全な解答にも部分点が与えられます ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=CKA%2CCKAD%2066%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20CKS%2067%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20%E5%90%84%E8%A9%A6%E9%A8%93%E3%81%AB%E3%81%AF%E9%87%8D%E3%81%BF%E4%BB%98%E3%81%8C%E3%81%82%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E9%85%8D%E7%82%B9%E3%81%8C%E5%A4%9A%E3%81%84%E3%82%82%E3%81%AE%E3%81%AF%E3%81%A7%E3%81%8D%E3%82%8C%E3%81%B0%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E3%80%82,%E5%B9%B8%E9%81%8B%E3%81%AA%E3%81%93%E3%81%A8%E3%81%AB%E3%80%81%E9%83%A8%E5%88%86%E7%82%B9%E3%81%8C%E3%81%82%E3%82%8B%E3%81%9F%E3%82%81%E3%80%81%E9%9B%A3%E3%81%97%E3%81%84%E3%81%A8%E6%84%9F%E3%81%98%E3%81%AA%E3%81%8C%E3%82%89%E3%82%82%E3%82%84%E3%82%8C%E3%82%8B%E3%81%A8%E3%81%93%E3%82%8D%E3%81%BE%E3%81%A7%E3%82%84%E3%82%8B%E3%81%A8%E3%80%81%E5%90%88%E6%A0%BC%E7%8E%87%E3%81%8C%E3%81%8B%E3%81%AA%E3%82%8A%E4%B8%8A%E6%98%87%E3%81%97%E3%81%BE%E3%81%99%E3%80%82))。試験中は公式のKubernetesドキュメントを参照可能な「オープンブック形式」ですが、時間制限が厳しいため事前の習熟が不可欠です ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=The%20test%20environment%20includes%20access,Pods%2C%20ConfigMaps%2C%20and%20troubleshooting%20services))。問題ごとに重み付け（配点割合）があり、合計100点満点です ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=You%20need%2066,tasks%20related%20to%20the%20scenario))。  

**出題ドメインと範囲:** CNCFが公開している最新カリキュラムによれば、CKAD試験は以下の5つのドメイン（出題カテゴリ）に分類されています ([Certified Kubernetes Application Developer (CKAD) | CNCF](https://www.cncf.io/certification/ckad/#:~:text=This%20exam%20curriculum%20includes%20these,their%20weights%20on%20the%20exam))。各ドメインの重要ポイントをまとめます。

- **Application Design and Build（20%）** – **Podの設計とビルド**に関する分野です。単一コンテナおよびマルチコンテナPodの基礎、コンテナイメージの利用、YAMLマニフェストの記述法などを含みます。具体的には**Podの基本構成**、マルチコンテナPodパターン（例：サイドカー、アンバサダー、アダプター） ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Multi,and%20Annotations%20State%20Persistence%208))、Pod間の連携方法など、Kubernetes上にアプリケーションを**デプロイ設計**するスキルが問われます。

- **Application Deployment（20%）** – **アプリケーションのデプロイ**と管理に関する分野です。デプロイオブジェクト(Deployments)を使ったローリングアップデートとロールバック ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=sidecar%29%20Pod%20Design%2020,PersistentVolumeClaims%20for%20storage%20Configuration%2018))、レプリカセットによるスケーリング、Job/CronJobによるバッチ処理実行 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=sidecar%29%20Pod%20Design%2020,PersistentVolumeClaims%20for%20storage%20Configuration%2018))などが出題されます。ラベルやセレクタを用いたオブジェクトのグルーピングや選択 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20Deployments%20and%20how,Understand%20ConfigMaps%20%E2%80%A2%20Understand%20SecurityContexts))も重要です。要するに、**継続的なリリースやスケーリング**に関する知識が問われます。

- **Application Observability and Maintenance（15%）** – **アプリケーションの可観測性と維持管理**に関する分野です。稼働中のコンテナのログ取得、トラブルシューティング手法、およびLiveness/Readinessプローブの設定 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Create%20%26%20consume%20Secrets,%E2%80%A2%20Understand%20debugging%20in%20Kubernetes))など、**動作確認とデバッグ**に関するスキルが問われます。具体例として、Podの状態監視、`kubectl logs`や`kubectl exec`によるデバッグ、Probe失敗時の挙動分析などが含まれます。

- **Application Environment, Configuration and Security（25%）** – **アプリケーションの実行環境設定とセキュリティ**に関する分野です。ConfigMapやSecretによる設定注入 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging))、環境変数の利用、リソース要求と制限（リソースクオータ） ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging))、SecurityContextによるコンテナのセキュリティ設定 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging))、およびServiceAccountの利用 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20SecurityContexts%20%E2%80%A2%20Define,consume%20Secrets%20%E2%80%A2%20Understand%20ServiceAccounts))などが含まれます。**永続ストレージ**（PersistentVolumeとPersistentVolumeClaim）の使用方法も実務上重要で、この範囲に関連して出題される可能性があります。

- **Services and Networking（20%）** – **サービスとネットワーク**に関する分野です。ClusterIP, NodePort, LoadBalancerなど**Serviceリソース**の種類と用途、外部からのアクセスに必要な **Ingressリソース**の設定、基本的なNetworkPolicyの概念 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20debugging%20in%20Kubernetes,Demonstrate%20basic%20understanding%20of%20NetworkPolicies))などが問われます。サービスディスカバリやDNS、Ingressコントローラによるルーティング設定など、**コンテナ間および外部との通信**に関する知識が必要です。特にIngressの設定方法とNetworkPolicyによる通信制限は受験者がつまずきやすいポイントとして指摘されています ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=By%20this%20point%2C%20I%20was,exercises))。

※上記各カテゴリのパーセンテージは試験スコアへの配点割合を示しています ([Certified Kubernetes Application Developer (CKAD) | CNCF](https://www.cncf.io/certification/ckad/#:~:text=Domain%20Weight%20Application%20Design%20and,Services%20and%20Networking%2020))。例えば「Environment, Configuration and Security」は試験全体の25%を占める重要分野です。満遍なく取り組む必要がありますが、特に配点の高い領域は重点的に対策しましょう ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=CKA%2CCKAD%2066%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20CKS%2067%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20%E5%90%84%E8%A9%A6%E9%A8%93%E3%81%AB%E3%81%AF%E9%87%8D%E3%81%BF%E4%BB%98%E3%81%8C%E3%81%82%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E9%85%8D%E7%82%B9%E3%81%8C%E5%A4%9A%E3%81%84%E3%82%82%E3%81%AE%E3%81%AF%E3%81%A7%E3%81%8D%E3%82%8C%E3%81%B0%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E3%80%82,%E5%B9%B8%E9%81%8B%E3%81%AA%E3%81%93%E3%81%A8%E3%81%AB%E3%80%81%E9%83%A8%E5%88%86%E7%82%B9%E3%81%8C%E3%81%82%E3%82%8B%E3%81%9F%E3%82%81%E3%80%81%E9%9B%A3%E3%81%97%E3%81%84%E3%81%A8%E6%84%9F%E3%81%98%E3%81%AA%E3%81%8C%E3%82%89%E3%82%82%E3%82%84%E3%82%8C%E3%82%8B%E3%81%A8%E3%81%93%E3%82%8D%E3%81%BE%E3%81%A7%E3%82%84%E3%82%8B%E3%81%A8%E3%80%81%E5%90%88%E6%A0%BC%E7%8E%87%E3%81%8C%E3%81%8B%E3%81%AA%E3%82%8A%E4%B8%8A%E6%98%87%E3%81%97%E3%81%BE%E3%81%99%E3%80%82))。

**試験対策全般のポイント:** CKADはオープンブックとはいえ**実践スキル重視**の試験です。公式ドキュメントを素早く参照できるようにしつつ、コマンド入力やYAML編集のスピードが鍵となります ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=,interact%20with%20the%20Kubernetes%20environment))。受験者は`kubectl`コマンドに習熟し、主要なリソース定義を素早く書けるように練習してください。また、試験ではクラスタのコンテキスト切り替えや名前空間の指定を誤ると正答にならないため、**環境の使い方**にも注意が必要です ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,If%20there%20is%20no))。

---

## 2. 出題カテゴリ別：学習アクションと実践練習方針

CKAD合格のためには、各カテゴリごとに**「知識の習得」＋「手を動かす練習」**をセットで行うことが重要です ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=3.%20Hands,Get%20comfortable%20with))。以下に、ドメイン別の具体的な学習アクションと、実践すべき演習内容の方針を示します。実際にKubernetes環境を操作しながら進めましょう（ローカルにMinikubeをセットアップするか、後述のKillercodaなどオンライン環境を利用します）。

### 2.1 Application Design and Build（アプリケーション設計とビルド）

- **基礎のインプット:** まずPodとは何か、YAMLマニフェストの基本構造、`kubectl`によるリソース操作方法を学びます。Udemy等の講座序盤やKubernetes公式チュートリアルで、**PodとDeploymentの基本**をインプットしましょう。合わせてDeploymentによるレプリカ管理やローリングアップデートの概念も把握しておくと後の学習がスムーズです。

- **マルチコンテナPod設計の理解:** サイドカーやInitコンテナなど、複数コンテナで1つのPodを構成するパターンを学びます ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Multi,and%20Annotations%20State%20Persistence%208))。**アクション:** サンプルとして以下を練習します:
  - Initコンテナ付きPodのYAMLを書く（例: 初期設定用のInitコンテナ＋メインコンテナ）  
  - ロギング用サイドカーコンテナを組み込んだPodを定義し、メインコンテナのログをサイドカーで集約するパターンを試す  
  - アンバサダーパターン（proxyコンテナ）やアダプタパターン（データ変換コンテナ）の例を読み、どのようにYAML定義するか理解する  

  これらを実際にデプロイして動作確認することで、複数コンテナ運用の感覚を掴みます。

- **コンテナイメージの取り扱い:** Kubernetes上でアプリを動かす前提として、Dockerイメージの基礎にも触れておきます。**アクション:** 簡単なHello WorldアプリのDockerイメージを作成してDocker Hubにプッシュし、それをKubernetesのPodで動かす一連の手順を試します（Dockerコマンド練習を含む） ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=Another%20useful%20tip%20I%20found,valuable%20points%20in%20little%20time))。試験本番でもDockerイメージの指定や簡単な操作を問われる可能性があるため、基本的な`docker build`/`push`や`kubectl run`でイメージを起動する操作に慣れておきましょう。

- **YAMLとimperativeコマンドの使い分け練習:** CKADではYAMLを直接編集する場面が多いですが、時間短縮のために**命令型コマンド**で雛形を出力し、それを編集する方法が有効です ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=same.%20,file%20and%20edit%20the%20same))。**アクション:**  
  - `kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deploy.yaml` のようにしてYAMLを迅速に生成し、必要箇所を編集する練習をする。  
  - PodやServiceについて、`kubectl run`や`kubectl expose`によるワンライナー生成と、`kubectl edit`による編集を組み合わせてみる。  

  こうしたテクニックを**手を動かして体得**しておくと、本番で大幅な時間短縮になります ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,file%20and%20edit%20the%20same))。

### 2.2 Application Deployment（アプリケーションのデプロイ）

- **デプロイメントの操作:** Deploymentリソースを用いたアプリケーション展開と更新方法を習得します。**アクション:**  
  - Deploymentを作成してから、`kubectl scale`でレプリカ数を変更する操作を試す。  
  - `kubectl rollout undo`でロールバックするシナリオを練習（意図的に不正なイメージを適用→失敗確認→ロールバック）。  

  また、Deployment定義YAML内で`strategy`（RollingUpdate戦略など）のパラメータを変更する演習も行います。ローリングアップデート/ロールバック手順は頻出事項です ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=sidecar%29%20Pod%20Design%2020,PersistentVolumeClaims%20for%20storage%20Configuration%2018))。

- **Job/CronJobの活用:** 短命なバッチ処理にはJob、定期実行にはCronJobを使います。**アクション:**  
  - シンプルなJobを作成し、完了後の状態(`kubectl describe jobs`)を確認。  
  - CronJobで1分おきに実行するジョブを設定し、期待通り定期Podが立ち上がることを確認する。  

  CronJobはスケジューリング表記やHistory制御オプション（`successfulJobsHistoryLimit`等）も含め設定方法を学びます。

- **ラベルとセレクタの練習:** Kubernetesオブジェクトにおける**Label/Selector**の使い方は非常に重要です。**アクション:**  
  - DeploymentやPodに任意のラベルを付与し、`kubectl get pods -l <label>`でフィルタする。  
  - 複数のPodに共通ラベルを与え、そのラベルをselectorに持つServiceを作成して通信を確認。  

  試験でも「特定のラベルを持つリソースのみ操作する」シナリオがあり得るため、ラベル/アノテーション操作は自在にできるよう練習します ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20Deployments%20and%20how,Understand%20ConfigMaps%20%E2%80%A2%20Understand%20SecurityContexts))。

- **スケジューリング設定:** （CKAD範囲ではありますが、詳細なノード選択や親和性/忌避はCKA寄りなので最低限で可。）Node SelectorやTaints/Tolerationsの基本に触れておきます。余力があれば、DeploymentにnodeSelectorを設定して特定ノードにPodを配置する演習も行いましょう。  

### 2.3 Application Observability and Maintenance（可観測性と運用管理）

- **Liveness/Readinessプローブ設定:** アプリケーションのヘルスチェック方法を習得します。**アクション:**  
  - 任意のWebアプリケーションコンテナに対し、`livenessProbe`と`readinessProbe`を設定したPodをデプロイ。正常時とわざと失敗するケース（例えば異なるパスをチェック）を作り、`kubectl describe pod`でProbe失敗による挙動（再起動や未Ready状態）を確認する ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Create%20%26%20consume%20Secrets,%E2%80%A2%20Understand%20debugging%20in%20Kubernetes))。  
  - Probeの種類（HTTP GET、コマンド実行、TCP）それぞれを試して設定方法の違いを把握する。

- **ログと監視:** Kubernetesでのアプリログ取得・監視方法を練習します。**アクション:**  
  - `kubectl logs`でPodのログを追跡する練習。特にマルチコンテナPodでは`-c`オプションでコンテナを指定する点に注意。  
  - `kubectl exec`でコンテナ内に入り、簡単な診断コマンド（`ls`, `cat /path/to/log`など）を実行してみる。  

  また、時間があればPrometheusやGrafanaによるアプリメトリクス監視の概要に触れても良いですが、試験範囲としてはログとプローブ、簡単なデバッグ中心で十分です。

- **トラブルシューティング演習:** いくつか意図的に問題を起こし、原因を突き止めて解決する練習をします（CKADはトラブル対応問題も出ます ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,file%20and%20edit%20the%20same))）。**シナリオ例:**  
  - PodがCrashLoopBackOffになるケース: コンテナコマンドを誤って失敗させ、`kubectl describe`や`kubectl logs`で原因調査し、YAMLを修正。  
  - Serviceが機能しないケース: 間違ったポートやセレクタを設定してPodに届かない状況を作り、`kubectl describe service`等で問題点を発見。  

  これらの練習で、問題の切り分け手順（まずPod状態を見る→イベントを見る→ログを見る→設定を見る）を体に染み込ませます。

- **コンテナのライフサイクル**も理解しましょう。特に**短命のPod**を起動する際は`restartPolicy: Never`にしないと予期せぬ再起動が起きる点など注意が必要です ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=namespace.%20,exam%20page%20once%20you%20register))。手を動かす中でこのようなKubernetes特有の挙動にも慣れておきます。

### 2.4 Application Environment, Configuration and Security（環境設定とセキュリティ）

- **ConfigMapとSecretの利用:** アプリケーション設定を分離管理する方法を習得します。**アクション:**  
  - ConfigMapを作成し、それを環境変数としてPodに注入する演習。【例】簡易な設定値を持つConfigMapを作成し、Pod内のコンテナで`env:`からその値を読み込む。  
  - Secretを作成し、ボリュームとしてマウントする演習。マウント後にコンテナ内でファイルとしてシークレット値が利用できることを確認。  

  また、ConfigMap・Secretを使って**コマンドライン引数や設定ファイルを書き換える**パターンも試します（試験ではマニフェストへの差し込み方を問われる可能性があります）。

- **リソース要求と制限:** コンテナごとのリソース（CPU/メモリ）要求・制限を設定する練習をします。**アクション:**  
  - Podの定義に`resources:`セクションを追加し、`requests`と`limits`を設定。実行中のPodに対し`kubectl describe pod`で設定が反映されていることを確認 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging))。  
  - リソース制限を極端に小さくしてコンテナがOOMキルされる状況を作り、イベントメッセージを確認する。  

  併せて、Namespace単位のResourceQuotaやLimitRangeを設定する方法も理解しておくと良いでしょう（時間が許せば演習）。

- **セキュリティコンテキストとサービスアカウント:** Pod/コンテナのセキュリティ設定、およびServiceAccountの利用法を学びます。**アクション:**  
  - Podの`securityContext`でLinuxカーネルパラメータを調整する例を試す（例えば非rootユーザで動作させるため`runAsUser`を指定する等 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging))）。  
  - デフォルトとは異なるServiceAccountを用いてPodを起動するYAMLを書き、`kubectl describe pod`で実際に当該ServiceAccountが使われていることを確認 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20SecurityContexts%20%E2%80%A2%20Define,consume%20Secrets%20%E2%80%A2%20Understand%20ServiceAccounts))。  

  これらにより、**アプリケーションの動作環境を適切に設定し保護する**スキルを身につけます。

- **永続ボリューム（ストレージ）の扱い:** CKADではストレージ周りの比重は高くありませんが、アプリ開発者として**PersistentVolumeClaim(PVC)**を介したストレージ使用方法は理解しておきましょう。**アクション:**  
  - シンプルなPersistentVolumeとPersistentVolumeClaimを作成し、Podからそれを`volumeMount`する練習。Minikubeの場合はホストパスボリュームなどで試せます。  
  - PVCのリソースがバインドされる流れや、PVC未バインド時のPodの挙動を確認する。  

  （ストレージは出題されるなら基本的なPVC利用が中心です。）

- **その他セキュリティ事項:** NetworkPolicy（接続制御）はネットワーク範囲で扱いますが、時間があればPodSecurity Standards（旧PodSecurityPolicyの代替）やイメージ署名なども概要を掴んでおくと現場で役立ちます（試験直接出題は少なめ）。

### 2.5 Services and Networking（サービスとネットワーク）

- **Serviceのタイプ別設定:** Kubernetesサービスの種類と用途を実践で覚えます。**アクション:**  
  - ClusterIP Serviceを作成し、同一クラスタ内からアクセスできることを確認。  
  - 上記のServiceをNodePortタイプに変更して再デプロイし、Minikube環境の場合ホストの該当ポートにアクセスしてサービス経由で応答が得られることを確認。  
  - LoadBalancer Service（Minikubeの場合は代替手段として`minikube service`コマンド等）も試し、外部IPが割り当てられる挙動を理解。  

  加えて、Serviceのセレクタを意図的に間違えてPodが紐付かないケースを作り、`Endpoints`が空になることなども確認しておくと理解が深まります。

- **Ingressリソースの設定:** Ingressはサービスを外部HTTP(S)アクセス可能にする重要リソースです。**アクション:**  
  - シンプルなIngressを設定し、ホスト名やパスベースで異なるServiceにルーティングするシナリオを構築（例：`/app1`はService A、`/app2`はService Bに振り分け）。  
  - Ingressコントローラ（Minikubeならデフォルトで`ingress-nginx`アドオンを有効化可能）を導入し、実際にホスト名でアクセスして期待通り振り分けられるかテスト。  
  - TLS対応Ingressについて、時間があれば自己署名証明書+Secretで設定する練習（試験で詳細なTLS設定は稀ですが、yaml項目として知識があると安心です）。  

  Ingressは設定項目が多いので、まず**公式ドキュメントのシンプルな例** ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=By%20this%20point%2C%20I%20was,exercises))を動かし、その設定を暗記ではなく理解することを目指します。

- **NetworkPolicyの基礎:** NetworkPolicyによる通信許可/拒否も開発者に関連する場合があります（アプリのネットワーク要件定義として）。**アクション:**  
  - 2つのNamespaceまたは2つの異なるラベルを持つPodグループ間でNetworkPolicyを適用し、一方からの接続のみブロックするルールを作成。適用前後でPod間通信（`curl`など）の結果が変わることを確認 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20debugging%20in%20Kubernetes,Demonstrate%20basic%20understanding%20of%20NetworkPolicies))。  

  NetworkPolicyは全てを網羅する必要はありませんが、**ポート・対象選択（podSelector, namespaceSelector）**の書き方を押さえ、デフォルト許可/拒否の挙動を理解しておきます。

- **DNSとサービス発見:** Cluster内DNSを使ってService名で他サービスにアクセスする方法も確認します（`my-service.my-namespace.svc.cluster.local`の形式）。演習として、BusyBoxコンテナを起動し、`nslookup`や`ping`で別サービス名解決を試すのも良いでしょう。

---

## 3. 10日間集中学習スケジュール（4/27〜5/6）

ゴールデンウィーク10日間の**日別学習計画**です。各日ごとにテーマを設定し、対応するToDoリストをこなしていきます。計画には適宜休憩も織り交ぜ、無理のないペース配分を心掛けましょう（1日あたり5〜8時間学習想定）。実際の進捗に応じて柔軟に調整してください。

1. **4/27 (Day 1)：学習準備とKubernetes基礎**  
   - [ ] **環境準備：** 学習用のKubernetes環境をセットアップする（ローカルにMinikube or Kindをインストール。またはブラウザで使える ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=3.%20dgkanatsios%2FCKAD))**Killercoda**のKubernetes Sandboxを利用開始）。  
   - [ ] **CKAD概要把握：** 本ドキュメントのセクション1を再確認し、試験形式・範囲を把握する。公式ハンドブックに目を通すとなお良い。  
   - [ ] **K8s基礎講座視聴：** Udemy等の教材でKubernetes基礎セクションを視聴（Kubernetesアーキテクチャ概要、Pod/Node/Serviceなど主要リソースの概要説明）。  
   - [ ] **基本操作演習：** 手元のクラスターで`kubectl get nodes`, `kubectl create namespace`など基本コマンドを実行し、環境に慣れる。  
   - [ ] **Linuxコマンド確認：** 必要に応じてgrepやvim操作などターミナル操作の基礎をおさらい（試験ではvimでYAML編集するため最低限の操作に慣れる） ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=introductory%20course%2C%20which%20gave%20me,hit%20my%20first%20bottleneck%3A%20vi%2Fvim))。

2. **4/28 (Day 2)：Podの基本とDeployment入門**  
   - [ ] **講義視聴：** Podの作成方法、Deploymentによる管理を解説する部分を視聴（例：Udemyコースの「Pods」「Deployments」章）。  
   - [ ] **単一コンテナPod演習：** `kubectl run`コマンドでNginxコンテナをPodとして起動し、そのPod詳細を確認。YAMLをエクスポートして内容を理解。  
   - [ ] **Deployment演習：** `kubectl create deployment`で簡単なDeploymentを作成し、`kubectl scale`でレプリカを増減させてみる。Podの再作成や削除の様子を観察。  
   - [ ] **YAMLハンズオン：** Deployment YAMLを一から書く練習。Udemy講座付属のラボや公式チュートリアル（Katacodaシナリオがあれば尚可）でPod定義YAMLの編集演習に取り組む。  
   - [ ] **理解チェック：** なぜDeploymentが必要なのか、Podを直接管理しない理由などを言語化して説明してみる（理解の定着を図る）。

3. **4/29 (Day 3)：マルチコンテナPodとJob/CronJob**  
   - [ ] **講義視聴：** マルチコンテナPodパターン（Initコンテナ、サイドカーなど）やJob/CronJobについての講義部分を視聴。  
   - [ ] **マルチコンテナ演習：** Initコンテナ付きPodのYAMLを作成しデプロイ。Initコンテナで作成したファイルをメインコンテナが読むなど連携を確認。【Todo例】公式ドキュメントのサイドカーアーキテクチャの例を参考に実装 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Multi,and%20Annotations%20State%20Persistence%208))。  
   - [ ] **Job演習：** バッチ処理用のJobを作成。完了ステータスを確認し、再実行されないことを確認する。失敗するJobをあえて作り、`restartPolicy`や失敗時の振る舞いも確認。  
   - [ ] **CronJob演習：** CronJobを作成し、スケジュール通りにPodが作成されるか観察。`kubectl get cronjob,job,pod`を連続的に実行して挙動を追う。  
   - [ ] **復習とメモ:** ここまで学んだPod/Deployment/Job関連のキーポイントをノート整理。分からなかった点は公式ドキュメントで調べて補足。

4. **4/30 (Day 4)：サービス周りの基礎（Service, ConfigMap, Secret）**  
   - [ ] **講義視聴：** Kubernetesサービス（ClusterIP/NodePortなど）の章、およびConfigMapとSecretに関する章を視聴。  
   - [ ] **Service演習：** 簡単なDeployment（例：nginxのレプリカ3つ）を用意し、ClusterIP Serviceで内部通信を確認。その後NodePortにタイプ変更して外部アクセス検証。  
   - [ ] **ConfigMap演習：** 環境変数を外部定義するConfigMapを作成し、Podにマウント（envFromまたはvolume）して値を読み取るアプリケーションを実行。`kubectl exec`で中の環境変数をチェック。  
   - [ ] **Secret演習：** Secretを作成し、同様にPodに注入（環境変数またはボリューム）する演習。特殊なエンコードに注意しつつ、動作を確認。  
   - [ ] **応用確認：** ConfigMap/Secretを使ってアプリの設定を書き換えるシナリオを検討（例：環境によってログレベルを切り替えるなど）。  

5. **5/1 (Day 5)：セキュリティ設定とリソース制限**  
   - [ ] **講義視聴：** SecurityContextやServiceAccount、Resource Limit/Requestに関する章を視聴。ネットワークポリシーにも目を通す。  
   - [ ] **Resource Limit演習：** 制限付きコンテナを作成（低いメモリ制限でメモリ大量消費プログラムを実行）し、`kubectl describe pod`で制限発動を確認。LimitRangeリソースも作成してNamespace全体のデフォルト制限を試す。  
   - [ ] **SecurityContext演習：** PodのYAMLにsecurityContextを追加し、コンテナを非rootユーザで動かす設定を試す。実際にPod内で`id`コマンドを実行してUIDを確認。  
   - [ ] **ServiceAccount演習：** 新規ServiceAccountを作成し、それを用いるPodをデプロイ。`kubectl describe pod`でServiceAccount欄が期待通りかチェック。  
   - [ ] **NetworkPolicy演習：** 2つのNamespace間通信を禁止するNetworkPolicyを適用。Netpol適用前後で`curl`の通り具合を比較し、ポリシーの効果を確認。（Minikubeの場合は`calico`などネットワークプラグイン前提。Killercodaでは事前にネットワークポリシー対応環境が用意されています。）  
   - [ ] **ストレージ演習（任意）:** 余裕があればPersistentVolume/PVCを作成し、簡単な永続データを書き込むPodを動かしてみる。

6. **5/2 (Day 6)：可観測性とトラブルシューティング**  
   - [ ] **講義視聴：** Probe設定とログ/デバッグに関する章を視聴。過去問レビューがあれば、典型的なトラブルシューティング問題の解き方を確認。  
   - [ ] **Liveness/Readiness演習：** アプリにわざと不備を入れてLivenessProbeが失敗する状況を作り、KubernetesがPod再起動する様子を確認。設定を修正して正常になることも確認。  
   - [ ] **ログ収集演習：** `kubectl logs -f`でリアルタイムログを追跡。マルチコンテナのPodで各コンテナのログを個別に確認。  
   - [ ] **デバッグ演習：** `kubectl exec`でPod内に入り、アプリプロセスの動作確認や設定ファイルの中身をチェック。必要に応じて`kubectl cp`でファイルを取得して調査。  
   - [ ] **シナリオ練習:** 過去のCKAD受験記や演習問題集からトラブル系シナリオを2〜3題解いてみる（例：「Podが起動しない」「Service経由で接続できない」など）。問題文を自分で作ってChatGPTに投げ、答え合わせするのも良いでしょう。

7. **5/3 (Day 7)：サービスとIngress実践**  
   - [ ] **講義視聴：** Ingressに関する章を重点的に視聴。Ingressリソースの構成要素（ホスト、パス、バックエンドService、オプションTLS等）を把握。  
   - [ ] **Ingress演習：** 2つの簡易Webアプリを異なるパスでサービス公開し、単一のIngressでルーティングする設定を実施。Ingressリソース作成後、正しくルーティングされるかcurlでテスト。  
   - [ ] **Ingressトラブル確認：** 意図的にIngressのService名やパスを間違えて設定し、`kubectl describe ingress`でエラーやマッピング状況を確認する。修正して正しく動作する状態に戻す。  
   - [ ] **外部アクセス検証:** Minikubeの場合は`minikube tunnel`などを利用してIngressに外部からアクセスし、レスポンスを得る（コントローラを起動していれば可能）。Killercoda等ではシナリオに従って検証。  
   - [ ] **付随知識整理:** Service/Ingress/NetworkPolicyと、前日までのConfig/Secret設定が一連のアプリにどう関与するかを整理。例として「あるWebアプリを外部公開しつつ、設定情報はSecretで渡し、プローブで監視する」というシナリオを頭の中で組み立ててみる。

8. **5/4 (Day 8)：総復習と模擬試験準備**  
   - [ ] **分野別おさらい:** ここまでの各カテゴリ内容を総ざらい。まだ手を動かしていない項目や不安が残るトピックを洗い出し、公式ドキュメントを読み直したり小テスト問題を解いたりして補強する ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=3.%20udemy%2C%20kodecloud%E3%81%8C%E4%B8%80%E9%80%9A%E3%82%8A%E7%B5%82%E3%82%8F%E3%81%A3%E3%81%9F%E3%82%89%E3%80%81kodecloud%E3%81%AB%E3%81%82%E3%82%8B%E3%80%81%E3%80%8C%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%80%8D%E3%80%81%E3%80%8CLightning%20Labs%E3%80%8D%E3%80%81%E3%80%8Cexam%20mock1,%E7%86%B1%E3%81%8C%E5%86%B7%E3%82%81%E3%81%AA%E3%81%84%E3%81%86%E3%81%A1%E3%81%AB%E8%A9%A6%E9%A8%93%E6%97%A5%E3%82%922%E9%80%B1%E9%96%93%E5%85%88%E3%81%BB%E3%81%A9%E3%81%AB%E8%A8%AD%E5%AE%9A%E3%81%97%E3%81%A6%E3%81%8A%E3%81%8F%E3%80%82%28%E8%A9%A6%E9%A8%93%E6%97%A5%E3%81%AF%E5%B9%B3%E6%97%A5%E6%9C%A8%E6%9B%9C%E6%97%A5%E3%81%82%E3%81%9F%E3%82%8A%E3%81%A8%E3%81%8B%E3%81%8C%E8%89%AF%E3%81%84%E3%81%8B%E3%82%82%E3%81%97%E3%82%8C%E3%81%AA%E3%81%84%E3%81%A7%E3%81%99%E3%80%82))。  
   - [ ] **ライトニングラボ実施:** KodeKloudのコース受講者であれば、用意されているLightning Labs（時間制限付きミニ模試）を解く。無い場合は、dgkanatsiosのCKAD練習問題集 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=,exercises))からランダムにいくつかピックアップし、**制限時間を設けて**解答してみる。  
   - [ ] **解答速度向上:** 解いた問題の解説を確認しつつ、もっと速く解く方法がないか検討。Imperativeコマンドで時短できたか、ドキュメント参照せずにできた部分はどこか、などを振り返る。  
   - [ ] **明日の模擬試験準備:** 明日実施する模擬試験（killer.sh想定）に向け、環境（ブラウザ、ネット回線、メモリ等）をチェック。可能ならLinux Foundation提供のシステムテストを事前に実行しておく。  

9. **5/5 (Day 9)：模擬試験（Killer.sh模試を本番同様に実施）**  
   - [ ] **試験シミュレーション:** 朝から2時間、公式提供の模擬試験環境**Killer.sh**を本番と同じ緊張感で実施（CKAD購入者は2回まで無料で利用可。未購入の場合は**29.99€**で2回分購入可能 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))）。必ずタイマーをセットし、途中で回答に詰まった問題は飛ばして、解けるものから解答する ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=You%20need%2066,tasks%20related%20to%20the%20scenario))。  
   - [ ] **模試結果分析:** 模試終了後、スコアと解けなかった問題を確認。スコアが66%を下回っていても気落ちせず、**解けなかった問題の解説を精読**します。特に時間切れで落とした問題は、どの部分に時間を浪費したか分析します（環境切り替えのロス、YAML書き込みミスなど）。  
   - [ ] **弱点補強:** 模試でミスしたトピックを再復習。必要なら同種の問題を練習環境で再現して解き直す ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=My%20exam%20was%20scheduled%20for,helping%20to%20clear%20up%20misunderstandings))。例：「Ingressのパス書き間違い」で失点したなら、改めてIngress定義を書き起こす。また、誤解していたコマンドやオプションがあれば公式ドキュメントで正確な使い方を確認。  
   - [ ] **メンタル調整:** 本番形式の練習を一度経験したことで疲労も出る頃です。夜は早めに休み、十分な睡眠をとります。試験当日にピークのパフォーマンスを発揮できるよう体調管理も大切です。

10. **5/6 (Day 10)：最終確認と直前準備**  
    - [ ] **総仕上げ復習:** 朝に全ドメインの重要ポイントをざっと復習します。自作のまとめノートやチェックリストがあれば見直し、不安箇所がないか確認。特にIngressやNetworkPolicy、Storageなど**直前まで不安が残りやすい項目**を重点的におさらい ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=I%20also%20started%20to%20identify,and%20understanding%20of%20these%20concepts))。  
    - [ ] **頻出コマンド最終チェック:** `kubectl`の主要コマンド（特に`create`, `apply`, `run`, `expose`, `logs`, `exec`, `describe`, `get -o yaml`など）やオプションを頭に入れておきます。また`kubectl explain <リソース>`でリソースのフィールド構造を素早く確認する方法も思い出しておきます。  
    - [ ] **試験環境リハーサル:** 試験当日に使用するPCで、Linux Foundationのテスト環境にログインし、ブラウザの動作や画面操作を確認（受験システムの事前チェックが提供されている場合、必ず実施）。特に**ブラウザ上でのコピー&ペースト操作**を試してみます ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E8%A9%A6%E9%A8%93%E5%86%85%E5%AE%B9%E3%81%8C%E6%95%B0%E5%9B%9E%E5%BF%83%E3%82%92%E6%8A%98%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E8%B8%8F%E3%82%93%E5%BC%B5%E3%82%8B%EF%BC%81%E5%86%85%E5%AE%B9%E5%89%B2%E6%84%9B%20%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E4%B8%8A%E3%81%AE%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%80%81%E3%82%BF%E3%83%BC%E3%83%9F%E3%83%8A%E3%83%AB%E9%96%93%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E7%B7%B4%E7%BF%92%E3%81%AF%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%20%E6%9C%AC%E7%95%AA%E8%A9%A6%E9%A8%93%E3%81%AE%E5%90%88%E5%90%A6%E3%81%AB%E9%96%A2%E3%82%8F%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。リモートデスクトップ上でテキストを選択・貼り付けするショートカットに慣れておきましょう。  
    - [ ] **受験準備確認:** 受験要項（身分証や顔写真の準備、静かな個室の確保など）を再度確認。当日のプロクター対応に備え、試験開始30分前にはログインできるようスケジュールを立てます ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,9%20them))。  
    - [ ] **リラックス:** 最後に深呼吸して緊張をほぐします。ここまで頑張った自分を信じ、明日に備えて早めに就寝しましょう。

---

## 4. おすすめの学習教材とリソース

CKAD合格者の多くが活用している評価の高い教材を、日本語・英語問わず紹介します。オンライン講座から公式ドキュメント、模擬試験まで**実践的なコンテンツ**を優先しています。併せて、費用感や評価も可能な範囲で記載します。

- **Udemy: Kubernetes Certified Application Developer (CKAD)コース**（講師:Mumshad Mannambeth 他） ([Kubernetes Certified Application Developer (CKAD) Training - Udemy](https://www.udemy.com/course/certified-kubernetes-application-developer/?srsltid=AfmBOoorjrNZAkrRCOGk77jvNfRRG1wEMDiIYGX7IKrY1rFJlAax0vq_#:~:text=Udemy%20www,English))  
  世界で最も人気のCKAD講座です。Kubernetesの基礎からCKAD範囲を網羅し、各セクションにハンズオンラボが付属しています。**評価:★4.7/5**（35,000以上のレビュー）と高評価 ([Kubernetes Certified Application Developer (CKAD) Training - Udemy](https://www.udemy.com/course/certified-kubernetes-application-developer/?srsltid=AfmBOoorjrNZAkrRCOGk77jvNfRRG1wEMDiIYGX7IKrY1rFJlAax0vq_#:~:text=Udemy%20www,English))。講義は英語ですが、日本語字幕・吹き替え対応済みで学習しやすくなっています ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E5%9F%BA%E6%9C%ACudemy%E3%81%A7%E5%AE%8C%E7%B5%90%E3%81%97%E3%81%BE%E3%81%99%E3%80%82%E3%81%93%E3%81%A1%E3%82%89%E3%81%AE%E3%82%B3%E3%83%BC%E3%82%B9%E3%82%92%E8%B3%BC%E5%85%A5%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%A7%E7%84%A1%E6%96%99%E3%81%AEKodeKloud%E3%81%A8%E8%A8%80%E3%81%86%E3%82%B7%E3%83%9F%E3%83%A5%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E6%89%8B%E3%82%92%E5%8B%95%E3%81%8B%E3%81%97%E3%81%AA%E3%81%8C%E3%82%89%E3%80%81%E5%AD%A6%E3%81%B9%E3%81%BE%E3%81%99%E3%80%82%E5%85%88%E6%97%A5%E3%80%81%E5%AE%8C%E5%85%A8%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%8C%96%E3%81%97%E3%81%9F%20%E3%81%AE%E3%81%A7%E4%BB%8A%E3%81%AE%E4%BA%BA%E3%81%AF%E5%AD%A6%E3%81%B3%E3%82%84%E3%81%99%E3%81%84%E3%81%A7%E3%81%99%E3%80%82))。標準価格は約¥24,000ですがUdemyのセール時に**¥1,900〜¥2,300程度**で購入可能です ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E5%9F%BA%E6%9C%AC%E7%9A%84%E3%81%ABudemy%E3%82%92%E3%81%8A%E5%8B%A7%E3%82%81%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E5%AE%9A%E4%BE%A1%E3%81%8C24000%E5%86%86%E3%81%AA%E3%81%A9%E3%81%8B%E3%81%AA%E3%82%8A%E9%AB%98%E3%81%84%E3%81%AE%E3%81%A7%E3%80%81%E3%82%BB%E3%83%BC%E3%83%AB%E3%81%AE%E6%97%A5%E3%82%92%E7%8B%99%E3%81%A3%E3%81%A6%E8%B3%BC%E5%85%A5%E3%81%99%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%97%E3%81%BE%E3%81%97%E3%82%87%E3%81%86%E3%80%82%20%E3%81%84%E3%81%A4%E3%81%AE%E3%82%BB%E3%83%BC%E3%83%AB%E3%81%A7%E3%82%82%E8%89%AF%E3%81%84%E3%81%AE%E3%81%A7%E3%81%99%E3%81%8C%E3%80%81%E3%81%8A%E3%81%8A%E3%82%88%E3%81%9D1900))。このコース購入により**KodeKloud**という実践ラボ環境にも無料でアクセスでき、ブラウザ上で演習を繰り返せます（演習問題・模擬試験付き）。

- **公式Kubernetesドキュメント**（Kubernetes.io） ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=The%20test%20environment%20includes%20access,Pods%2C%20ConfigMaps%2C%20and%20troubleshooting%20services))  
  CKADは試験中に公式ドキュメント参照が許可されています。**公式ドキュメントそのものが最重要教材**です。試験範囲の各トピックについて、該当するドキュメントページ（例：ConfigMapの使い方、Deploymentのローリングアップデート方法など）を読み込みましょう。英語ですが日本語版も一部存在します。日頃から**サイト内検索**やページ内検索を駆使する練習をしておくと、本番で素早く必要情報を引けます ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=Also%20make%20sure%20you%20know,search%20provided%20by%20the%20browser))。特に参考になるページ:  
  - Kubernetes公式チートシート ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))（主要コマンドのまとめ）  
  - kubectlリファレンス ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))（オプション含め詳細）  
  - 各種リソースのAPIリファレンス（fieldsの構造を把握できる）  

- **Killer.sh CKAD模擬試験** ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))  
  CNCF公式が提供する模擬試験サービス。CKAD試験バウチャー購入時に**2回分無料**で付属します（単体購入も可で約30ドル/2回分） ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))。本番同様のUI・難易度で出題され、時間管理の練習に最適です。「killer.shは本番より難しめ」と言われますが、80%以上解ければ本番合格は堅いでしょう。受験直前の腕試しとして強くお勧めします。実施後は詳細な解説が得られるため、弱点発見にも役立ちます。

- **キルコーダ (Killercoda)** ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=3.%20dgkanatsios%2FCKAD))  
  ブラウザ上で無料利用できるKubernetes演習環境です。コマンドを自由に試せるサンドボックスや、CKAD向けのシナリオが提供されています。手元に環境構築できない場合や、手軽に色々な失敗を試したい場合に最適です。GUIのDashboard操作などは範囲外なので、本演習ではひたすらCLI操作に慣れるようにしましょう。Killercodaは**無料**です。

- **CKAD試験演習問題集（GitHubリポジトリ）** ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=,exercises))  
  有志がまとめたCKAD対策の演習問題集があります。特に有名なのはDimitrios氏の「CKAD Exercises」 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=,exercises))で、約50問程度の実践問題が公開されています。シナリオ形式で「〜を達成せよ」という問題文と解答があるので、自己学習に使えます。無料で誰でもアクセス可能です。自分で環境を用意して順番に解いていけば、弱点分野を洗い出すのに有用です。

- **Udemy: CKAD模擬試験コース（日本語解説付き）**  
  日本人講師によるCKAD向け問題演習コースもいくつかUdemyで提供されています。例：「CKAD模擬試験問題集【2024年版】」等は少数ながらレビューで高評価を得ています（※評価☆5.0だがレビュー数が少ない点に注意） ([認定Kubernetesアプリケーション開発者 (CKAD) 演習問題集 【2024 ...](https://www.udemy.com/course/ckad-questions/?srsltid=AfmBOooIURcr_BJLm7v0T5uqletNs842HL92tg053RX3jWPwn4HjXiAw#:~:text=%E8%AA%8D%E5%AE%9AKubernetes%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E9%96%8B%E7%99%BA%E8%80%85%20,0))。価格は同じくセール時¥2,000前後。英語教材に不安がある方や、日本語で解説を聞きながら問題演習したい方には有用です。ただし内容の最新性や網羅性は事前によく確認してください。

- **その他参考書籍・動画:** 書籍『Certified Kubernetes Application Developer (CKAD) Study Guide』（英語, O’Reilly）などテキストで体系的に学べる教材もあります。体系理解には役立ちますが、実技試験対策としては演習量を確保できるオンライン教材の方が効率的でしょう。また、合格者のブログ記事やYouTube解説動画（例：「How to Prepare and Crack CKAD in 2025」 ([How to Prepare and Crack CKAD exam in 2025 - Tips & Tricks](https://m.youtube.com/watch?v=6VrpdisVqAU#:~:text=How%20to%20Prepare%20and%20Crack,Go%20to))）もモチベーションアップに参考になります。

※費用は2025年4月時点の目安です。Udemyは頻繁にセールを行っているので、**セール期間に購入**するとお得です ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E5%9F%BA%E6%9C%AC%E7%9A%84%E3%81%ABudemy%E3%82%92%E3%81%8A%E5%8B%A7%E3%82%81%E3%81%97%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E5%AE%9A%E4%BE%A1%E3%81%8C24000%E5%86%86%E3%81%AA%E3%81%A9%E3%81%8B%E3%81%AA%E3%82%8A%E9%AB%98%E3%81%84%E3%81%AE%E3%81%A7%E3%80%81%E3%82%BB%E3%83%BC%E3%83%AB%E3%81%AE%E6%97%A5%E3%82%92%E7%8B%99%E3%81%A3%E3%81%A6%E8%B3%BC%E5%85%A5%E3%81%99%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%97%E3%81%BE%E3%81%97%E3%82%87%E3%81%86%E3%80%82%20%E3%81%84%E3%81%A4%E3%81%AE%E3%82%BB%E3%83%BC%E3%83%AB%E3%81%A7%E3%82%82%E8%89%AF%E3%81%84%E3%81%AE%E3%81%A7%E3%81%99%E3%81%8C%E3%80%81%E3%81%8A%E3%81%8A%E3%82%88%E3%81%9D1900))。公式試験の受験費用は$445（約5〜6万円）と高額なので、**一発合格**できるようこれら教材を最大限活用しましょう。

---

## 5. 出題テーマ別: ChatGPT活用「例題プロンプト」集

学習の仕上げや自己テストに、ChatGPTを活用してみましょう。各出題テーマごとに、ChatGPTに質問できる**例題プロンプト**を1～3個用意しました。ChatGPTにこれらを入力することで、模範解答や解説を得たり、対話形式で知識をチェックできます。疑似的な問題演習として活用してください（※実際の試験問題ではありませんが、類似のシナリオを想定しています）。

**① Pod設計 & マルチコンテナ関連:**
- **プロンプト例:** `「KubernetesでInitコンテナを使ってアプリ起動前に初期データを準備するにはどうすればいいですか？Initコンテナを含むPodのYAMLマニフェスト例を示してください。」`  
  *期待されるChatGPT回答:* Initコンテナの定義方法と、その具体例YAML（`initContainers`セクション付きPod定義）、およびInitコンテナの役割に関する解説。

- **プロンプト例:** `「Pod内にログ収集用のサイドカーコンテナを追加する方法を教えてください。メインコンテナのログをサイドカーで集約する設定のYAML例を説明付きでください。」`  
  *期待:* サイドカーコンテナの概念説明と、`shareProcessNamespace`やログ出力共有ディレクトリのマウント設定を含むPod YAML例。

**② アプリケーションのデプロイ & 管理:**
- **プロンプト例:** `「Rolling Update戦略でDeploymentをアップデートする手順を教えてください。kubectlコマンドと必要ならYAMLの変更点についても説明してください。」`  
  *期待:* `kubectl set image`でのイメージ更新法、`maxUnavailable`等の戦略パラメータ解説、ローリングアップデートの流れ説明。

- **プロンプト例:** `「KubernetesでCronJobを利用して毎日夜にバッチ処理を実行したいです。CronJobリソースのサンプルYAMLと設定項目（スケジュール表記や履歴保持など）の説明をしてください。」`  
  *期待:* CronJobの基本構造（`schedule: "0 0 * * *"`など）を示したYAML例と、主要フィールド（`jobTemplate`, `successfulJobsHistoryLimit`等）の意味解説。

**③ 可観測性 & トラブルシューティング:**
- **プロンプト例:** `「あるPodがCrashLoopBackOffになっています。どのように原因を調査し、解決すればよいでしょうか？考えられる原因の例も含めて教えてください。」`  
  *期待:* CrashLoopBackOff時の調査ステップ（ログ確認->設定ミス特定等）と典型的原因（イメージのCMD間違い、プローブ失敗など）および対処法の解説。

- **プロンプト例:** `「LivenessプローブとReadinessプローブの違いを教えてください。それぞれが失敗した場合のDeploymentの挙動も含めて説明してください。」`  
  *期待:* 両プローブの目的と違いの説明、Liveness失敗での再起動、Readiness失敗でServiceから外れる挙動の解説。

**④ 環境設定 (Config & Security):**
- **プロンプト例:** `「ConfigMapとSecretの違いは何ですか？それぞれをPodにマウントする方法（環境変数経由とボリューム経由）を具体例とともに教えてください。」`  
  *期待:* ConfigMapはプレーンテキスト、Secretは機密情報（Base64）であること、Podでの利用方法（env、volume）をYAML断片付きで解説。

- **プロンプト例:** `「Podを特定の非rootユーザ権限で実行するにはどう設定しますか？SecurityContextの設定例を示してください。」`  
  *期待:* PodまたはContainerの`securityContext`で`runAsUser`, `runAsGroup`, `fsGroup`を設定するYAML例と、それによりコンテナ内プロセスのUID/GIDがどうなるかの説明。

- **プロンプト例:** `「あるNamespace内のPod全てにデフォルトのリソース制限を適用したいです。どのリソースを使えばよいでしょうか？そのYaml例を示してください。」`  
  *期待:* Namespace単位で適用されるLimitRangeリソースの説明と、CPU/メモリのデフォルトrequests/limitsを指定したLimitRangeのYAML例。

**⑤ サービス & ネットワーク:**
- **プロンプト例:** `「ClusterIP, NodePort, LoadBalancer各Serviceの違いを説明してください。また、それぞれを作成するためのkubectlコマンド例を教えてください。」`  
  *期待:* 各タイプの概要とユースケース説明、`kubectl expose`や`kubectl create service`コマンドを使った具体的作成例。

- **プロンプト例:** `「Ingressリソースを使って`/frontend`はfrontサービスに、`/api`はapiサービスにルーティングする設定を行いたいです。IngressのYAML例をホスト名無しでいいので書いて説明してください。」`  
  *期待:* `paths`でパスプレフィックスごとにServiceを振り分けるIngress YAML例と、その主要フィールド（`pathType`, `serviceName`, `servicePort`等）の説明。

- **プロンプト例:** `「NetworkPolicyであるPodへのIngressトラフィックを特定の別Podからのものだけ許可するルールを作りたいです。どのようなYAMLになりますか？」`  
  *期待:* Podセレクタ同士を組み合わせたNetworkPolicyのYAML例（`podSelector`と`from`に別のpodSelectorを指定）とその解説。

*使い方:* 上記プロンプトをChatGPTに投げかけ、返ってきた解答を自分の答えと比較したり、不明点を追加で質問したりして理解を深めてください。ChatGPTは設定やコマンドの説明役、時にはクイズ出題役としても活用できます。ただしChatGPTの内容が必ず正確とは限らないため、**公式ドキュメントで裏付け確認**する癖付けも忘れずに。

---

## 6. 試験直前期の見直しポイントと本番Tips

最後に、ゴールデンウィーク明けから試験当日までの直前対策ポイントと、本番で実力を発揮するためのコツをまとめます。**5月前半（試験直前期）の過ごし方**と**実技試験本番のTips**に分けて確認しましょう。

### ● 直前期（試験1〜2週間前）の見直しポイント

- **弱点分野の重点補強:** 10日間の学習で各トピックを一通り経験したとはいえ、苦手意識の残る部分は直前期に集中して潰します。模擬試験や演習で間違えた箇所を洗い出し、もう一度同じシナリオを**公式ドキュメントを見ずに解けるか**練習しましょう ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=My%20exam%20was%20scheduled%20for,helping%20to%20clear%20up%20misunderstandings))。例えばIngressの設定ミスが多かったならIngressのYAMLを白紙から書く練習を繰り返す、といった具合です。

- **頻出タスクのおさらい:** CKADでよく出る典型タスクをリストアップし、自力で手順を言語化できるか確認します（実際に手を動かすのがベスト）。例として:
  - *「新しいNamespaceを作り、その中にDeploymentとServiceを作成する」*  
  - *「特定のPodのCPU使用率が高い時に調査する方法（トップコマンド代替など）」*  
  - *「Secretを使ってアプリのパスワード設定を注入する」*  
  など、一連の操作フローが頭に入っているかチェックします。言葉で説明できれば理解できている証拠です。

- **コマンドエイリアス/ショートカット確認:** 試験環境には`kubectl`が長いため**`k`エイリアス**が用意されていることがあります ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=You%20should%20also%20use%20imperative,less%20characters%20do%20add%20up))。`alias`の設定は当日確認するとして、自分でも`kubectl`を打つ代わりに`k`で操作する練習をしておくと良いでしょう。また、よく使うオプションはシェルの補完機能(Tab補完)を活用すると時短になります。試験前に主なコマンドの短縮形を整理しておきます。

- **公式ドキュメント参照練習の仕上げ:** 本番では制限時間内にドキュメントから答えを探す余裕はあまりありません。しかしゼロではなく、**どうしても思い出せない細かなオプション**（例: CronJobのスケジュール書式）などは素早く参照できると安心です。直前期に、公式サイト内検索のキーワード選定や、各トピックのドキュメント所在（どのセクションに記載があるか）を復習しておきましょう ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=Also%20make%20sure%20you%20know,search%20provided%20by%20the%20browser))。特にリソースの**マニフェスト構造**を確認できる`kubectl explain`コマンドも有効なので、使い方を再確認します。

- **模擬環境での再現練習:** 可能であれば試験直前にもう一度**killer.sh等で模擬試験**を実施し、前回からの向上を確認します ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=1,sh%E3%82%84%E3%81%A3%E3%81%A6%E3%80%9C%E3%81%AE%E6%B5%81%E3%82%8C%E3%81%AF%E5%90%8C%E3%81%98%E3%81%AA%E3%81%AE%E3%81%A7%E3%80%81%E3%81%9D%E3%82%8C%E3%81%A7%E3%81%84%E3%81%91%E3%82%8B%E3%81%8B%E3%81%A8%E6%80%9D%E3%81%84%E3%81%BE%E3%81%99%E3%80%82))。時間が無ければ、頭の中で模擬問題をイメージして解法をシミュレーションするのも有効です。とにかく**タイピングのスピードと正確性**が合否を左右するため、直前期も手を止めずキーボードに触れ続けることが大事です。

### ● CKAD本番当日のTips（システム操作・注意点など）

- **試験環境セットアップ確認:** 試験当日はLinux Foundationの専用環境にブラウザ経由で入り受験します。開始前にプロクターの指示に従い身分証提示やカメラ確認を行います。事前に周囲に参考資料等置いていないこと、スマホなど手元にないことを確認してください（発見されると失格になります）。また、**受験用PC以外のディスプレイは全てオフ**にする必要があります。

- **操作に慣れる:** 試験では**リモートデスクトップ上での操作**になります。自PCのキーボード配列やコピー&ペーストのキー操作が普段と異なる場合があるので注意しましょう（例：macOSでは`Cmd+V`ではなく`Ctrl+Shift+V`で貼り付け等）。事前の環境テストで確認したショートカットを本番でも活用します。**ペーストは特に時間短縮の鍵**なので、戸惑わないように ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E8%A9%A6%E9%A8%93%E5%86%85%E5%AE%B9%E3%81%8C%E6%95%B0%E5%9B%9E%E5%BF%83%E3%82%92%E6%8A%98%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E8%B8%8F%E3%82%93%E5%BC%B5%E3%82%8B%EF%BC%81%E5%86%85%E5%AE%B9%E5%89%B2%E6%84%9B%20%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E4%B8%8A%E3%81%AE%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%80%81%E3%82%BF%E3%83%BC%E3%83%9F%E3%83%8A%E3%83%AB%E9%96%93%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E7%B7%B4%E7%BF%92%E3%81%AF%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%20%E6%9C%AC%E7%95%AA%E8%A9%A6%E9%A8%93%E3%81%AE%E5%90%88%E5%90%A6%E3%81%AB%E9%96%A2%E3%82%8F%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))。

- **複数クラスタのコンテキスト切替:** CKADでは問題ごとに異なるKubernetesクラスターが用意されており、都度コンテキストを切り替える必要があります ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=higher%20weights%20before%20focusing%20on,paste%20it))。各設問文の冒頭に`kubectl config use-context ...`コマンドが提示されるので、**必ず問題に取り掛かる前に実行**してください ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=%2A%20CKAD%20exam%20provides%206,paste%20it))。うっかり前の問題のコンテキストのまま操作すると、正しいリソースに対して解答できず**得点されません** ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,If%20there%20is%20no))。

- **名前空間に注意:** 問題文で特定のNamespaceが指定されている場合、必ず`-n <NAMESPACE>`オプションを付けて操作するか、対象Namespaceに切り替えてください ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=be%20done%20in%20the%20same,with%20busybox%20then%20make%20sure))。Namespaceの指定漏れは初歩的ミスですが本番で焦ると起こりがちです。逆に指定が無い場合は`default` Namespaceで実施します。`kubectl config set-context --current --namespace=<NAME>`で都度Namespaceを設定してしまうのも一つの手です。

- **問題文のヒント活用:** 試験画面の問題文には「ℹ︎」アイコンの情報セクションがあり、**既に用意されているリソースやヒント**が書かれていることがあります ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,file%20and%20edit%20the%20same))。例えば「既にConfigMap Xが作成済み」などです。読まずにリソースを新規作成すると不要な作業をして時間ロスします。必ず問題を落ち着いて読み、ヒント情報も確認してから動き始めましょう。

- **時間配分と飛ばす勇気:** 2時間で全問解くには**1問あたり平均7～8分**程度の計算になります。ただし重い問題は15分以上かかるものもあるため、**配点と残り時間に応じて取捨選択**が重要です ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=The%20important%20thing%20to%20note,time%20in%20the%20first%20place))。各設問の重み付けは事前には表示されない可能性もありますが（※画面にWeightが出ないとの報告あり）、高難度で時間を食いそうなものは一旦飛ばして他を先に解くのが鉄則です ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=You%20need%2066,tasks%20related%20to%20the%20scenario))。部分点狙いで**一部だけでも手を付ける**価値はありますが、泥沼にはまらないよう見極めましょう。

- **解答の検証:** 解答した内容が正しく反映されているか、その場で検証できる場合は確認しましょう。例えば「Podを作成し◯◯できるようにせよ」という問題なら、`kubectl get pod`や`kubectl describe`で状態を確認し、要求通り動作しているかチェックします。時間に余裕があれば、`kubectl logs`等で想定する動きになっているか見ることで安心感も得られます。**ただし時間配分が最優先**なので、深追いは禁物です。

- **便利機能の活用:** 試験UIには未完了問題にフラグを立てたり、全体の残り時間を確認したりする機能があります。分からない問題はフラグを付けて飛ばし、後で一覧から戻れるようにします。時間ギリギリになったら、一旦すべてのコンソールを停止しフラグ付き問題をチェックし直す、といった動きも有効です。

- **トラブルへの対処:** 受験中に環境トラブル（画面フリーズ・ネット切断など）に遭遇した場合は慌てず対応しましょう。基本は**即座にプロクターにチャットで連絡**します。再接続が必要と言われたら指示に従います。時間ロスが大きい場合は後日救済措置を依頼できるケースもあるので、落ち着いて対処してください。

- **最後まで諦めない:** 部分点があるため、たとえ全問完了できなくても**途中まで書いたリソース**は提出しましょう ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=CKA%2CCKAD%2066%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20CKS%2067%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20%E5%90%84%E8%A9%A6%E9%A8%93%E3%81%AB%E3%81%AF%E9%87%8D%E3%81%BF%E4%BB%98%E3%81%8C%E3%81%82%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E9%85%8D%E7%82%B9%E3%81%8C%E5%A4%9A%E3%81%84%E3%82%82%E3%81%AE%E3%81%AF%E3%81%A7%E3%81%8D%E3%82%8C%E3%81%B0%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E3%80%82,%E5%B9%B8%E9%81%8B%E3%81%AA%E3%81%93%E3%81%A8%E3%81%AB%E3%80%81%E9%83%A8%E5%88%86%E7%82%B9%E3%81%8C%E3%81%82%E3%82%8B%E3%81%9F%E3%82%81%E3%80%81%E9%9B%A3%E3%81%97%E3%81%84%E3%81%A8%E6%84%9F%E3%81%98%E3%81%AA%E3%81%8C%E3%82%89%E3%82%82%E3%82%84%E3%82%8C%E3%82%8B%E3%81%A8%E3%81%93%E3%82%8D%E3%81%BE%E3%81%A7%E3%82%84%E3%82%8B%E3%81%A8%E3%80%81%E5%90%88%E6%A0%BC%E7%8E%87%E3%81%8C%E3%81%8B%E3%81%AA%E3%82%8A%E4%B8%8A%E6%98%87%E3%81%97%E3%81%BE%E3%81%99%E3%80%82))。例えばIngress設定でホスト名以外あっていれば部分点、ネットワークポリシーも半分正しければ点が入る可能性があります。時間いっぱいまで手を動かし、入力中でもタイムアップまで粘る姿勢で臨みます。

以上が、CKAD合格に向けた戦略ドキュメントとなります。  
ゴールデンウィーク中の集中トレーニング計画に沿って学習を進めれば、確実に実力と自信が身につくはずです。最後まで手を動かすことを重視し、本番では落ち着いて取り組んでください。健闘を祈ります！🚀

**参考資料:** 本ドキュメントは公式情報や合格者の知見に基づいていま ([Certified Kubernetes Application Developer (CKAD) | CNCF](https://www.cncf.io/certification/ckad/#:~:text=This%20exam%20curriculum%20includes%20these,their%20weights%20on%20the%20exam)) ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=CKAD%20Exam%20Preparation%20and%20Tips))】。各種Tipsは実際の受験報告を参照していま ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,If%20there%20is%20no)) ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E8%A9%A6%E9%A8%93%E5%86%85%E5%AE%B9%E3%81%8C%E6%95%B0%E5%9B%9E%E5%BF%83%E3%82%92%E6%8A%98%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E8%B8%8F%E3%82%93%E5%BC%B5%E3%82%8B%EF%BC%81%E5%86%85%E5%AE%B9%E5%89%B2%E6%84%9B%20%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E4%B8%8A%E3%81%AE%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%80%81%E3%82%BF%E3%83%BC%E3%83%9F%E3%83%8A%E3%83%AB%E9%96%93%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E7%B7%B4%E7%BF%92%E3%81%AF%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%20%E6%9C%AC%E7%95%AA%E8%A9%A6%E9%A8%93%E3%81%AE%E5%90%88%E5%90%A6%E3%81%AB%E9%96%A2%E3%82%8F%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))】。疑問点があれば公式ドキュメントに立ち返る習慣を持ち、正確な知識で試験に臨みましょう。健闘を祈ります！@@

**Sources:**

1. CNCF, *“CKAD Exam Details & Curriculum,”* 202 ([Certified Kubernetes Application Developer (CKAD) | CNCF](https://www.cncf.io/certification/ckad/#:~:text=This%20exam%20curriculum%20includes%20these,their%20weights%20on%20the%20exam)) ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,Configuration%20and%20Security%20%E2%80%93%2025))】  
2. Shabab Karim, *“Passing the CKAD Exam - 2024,”* LinkedIn, 202 ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=You%20need%2066,tasks%20related%20to%20the%20scenario)) ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,If%20there%20is%20no))】  
3. fruscianteee, *“短期間でCKA, CKAD, CKS三冠達成...攻略法,”* Qiita, 202 ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=CKA%2CCKAD%2066%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20CKS%2067%E3%82%B9%E3%82%B3%E3%82%A2%E4%BB%A5%E4%B8%8A%E3%81%A7%E5%90%88%E6%A0%BC%20%E5%90%84%E8%A9%A6%E9%A8%93%E3%81%AB%E3%81%AF%E9%87%8D%E3%81%BF%E4%BB%98%E3%81%8C%E3%81%82%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E9%85%8D%E7%82%B9%E3%81%8C%E5%A4%9A%E3%81%84%E3%82%82%E3%81%AE%E3%81%AF%E3%81%A7%E3%81%8D%E3%82%8C%E3%81%B0%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E3%80%82,%E5%B9%B8%E9%81%8B%E3%81%AA%E3%81%93%E3%81%A8%E3%81%AB%E3%80%81%E9%83%A8%E5%88%86%E7%82%B9%E3%81%8C%E3%81%82%E3%82%8B%E3%81%9F%E3%82%81%E3%80%81%E9%9B%A3%E3%81%97%E3%81%84%E3%81%A8%E6%84%9F%E3%81%98%E3%81%AA%E3%81%8C%E3%82%89%E3%82%82%E3%82%84%E3%82%8C%E3%82%8B%E3%81%A8%E3%81%93%E3%82%8D%E3%81%BE%E3%81%A7%E3%82%84%E3%82%8B%E3%81%A8%E3%80%81%E5%90%88%E6%A0%BC%E7%8E%87%E3%81%8C%E3%81%8B%E3%81%AA%E3%82%8A%E4%B8%8A%E6%98%87%E3%81%97%E3%81%BE%E3%81%99%E3%80%82)) ([[保存版]短期間でKubernetesのCKA、CKAD、CKSの三冠達成したので攻略法(勉強方法の解説とコツ)を共有 #初心者 - Qiita](https://qiita.com/fruscianteee/items/5963793b870835023d53#:~:text=%E8%A9%A6%E9%A8%93%E5%86%85%E5%AE%B9%E3%81%8C%E6%95%B0%E5%9B%9E%E5%BF%83%E3%82%92%E6%8A%98%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8C%E3%80%81%E8%B8%8F%E3%82%93%E5%BC%B5%E3%82%8B%EF%BC%81%E5%86%85%E5%AE%B9%E5%89%B2%E6%84%9B%20%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E4%B8%8A%E3%81%AE%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%80%81%E3%82%BF%E3%83%BC%E3%83%9F%E3%83%8A%E3%83%AB%E9%96%93%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88%E3%81%AE%E3%82%B3%E3%83%94%E3%83%9A%E3%81%AE%E7%B7%B4%E7%BF%92%E3%81%AF%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%E7%B5%B6%E5%AF%BE%E3%81%AB%E3%81%97%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%EF%BC%81%20%E6%9C%AC%E7%95%AA%E8%A9%A6%E9%A8%93%E3%81%AE%E5%90%88%E5%90%A6%E3%81%AB%E9%96%A2%E3%82%8F%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%BE%E3%81%99%E3%80%82))】  
4. tplisson, *“CKAD Study Notes – Curriculum (v1.20),”* GitHub Gist, 202 ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=Configuration%2018,ReadinessProbes%20%E2%80%A2%20Understand%20container%20logging)) ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=%E2%80%A2%20Understand%20debugging%20in%20Kubernetes,Demonstrate%20basic%20understanding%20of%20NetworkPolicies))】  
5. Jayendra Patil, *“CKAD Learning Path – Exam Tips,”* 202 ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,paste%20it)) ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=,file%20and%20edit%20the%20same))】  
6. Mauricio Quevedo, *“How I Passed the CKAD in 3 Weeks,”* Medium, 202 ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=Goal%3A%20Crossing%20the%20Finish%20Line)) ([How I Passed the CKAD in 3 Weeks. Introduction | by Mauricio Quevedo | Medium](https://medium.com/@mauricioqdevops/how-i-passed-the-ckad-in-3-weeks-357b363ff432#:~:text=By%20this%20point%2C%20I%20was,exercises))】  
7. Brandon Kang, *“How to prepare CKAD – Key Domains,”* Medium, 202 ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=,Service%20types%2C%20Ingress%2C%20NetworkPolicies)) ([How to prepare CKAD (Certified Kubernetes Application Developer)? | by Brandon Kang | Medium](https://medium.com/@sangjinn/how-to-prepare-ckad-certified-kubernetes-application-developer-21b3f431a2d9#:~:text=makes%20hands,comfortable%20with))】  
8. Udemy, *“CKAD Course by Mumshad Mannambeth,”* (accessed 2025 ([Kubernetes Certified Application Developer (CKAD) Training - Udemy](https://www.udemy.com/course/certified-kubernetes-application-developer/?srsltid=AfmBOoorjrNZAkrRCOGk77jvNfRRG1wEMDiIYGX7IKrY1rFJlAax0vq_#:~:text=Udemy%20www,English))】  
9. Kubernetes Official Documentation – *Tutorials & Reference ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=)) ([GitHub - tplisson/k8s-CKAD-study-notes: This is my study guide for the Certified Kubernetes Application Developer  (CKAD) exam.](https://github.com/tplisson/k8s-CKAD-study-notes#:~:text=))】  
10. CNCF, *“CKAD Candidate Handbook (Exam Guidelines),”* 202 ([Certified Kubernetes Application Developer CKAD Learning Path](https://jayendrapatil.com/certified-kubernetes-application-developer-ckad-learning-path/#:~:text=%2A%20CKAD%20exam%20provides%206,paste%20it)) ([Passing the CKAD Exam - 2024](https://www.linkedin.com/pulse/passing-ckad-exam-2024-shabab-karim-fqrbe#:~:text=,9%20them))】

