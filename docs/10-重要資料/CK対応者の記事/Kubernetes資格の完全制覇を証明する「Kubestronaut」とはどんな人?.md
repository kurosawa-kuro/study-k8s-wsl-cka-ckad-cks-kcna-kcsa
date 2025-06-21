Kubernetes資格の完全制覇を証明する「Kubestronaut」とはどんな人?
 2024年11月29日(金)
 松田 元輝 (まつだ げんき)



本記事では、Kubernetesの資格を全て取得すると得られる称号「Kubestronaut」について紹介します。

目次
1 はじめに
2 Kubestronautとは
3 Kubestronautを取得するメリット
4 各資格の概要と攻略法
4.1 Kubernetes and Cloud Native Associate (KCNA)
4.2 Kubernetes and Cloud Security Associate (KCSA)
4.3 Certified Kubernetes Administrator (CKA)
4.4 Certified Kubernetes Application Developer (CKAD)
4.5 Certified Kubernetes Security Specialist (CKS)
5 おわりに
はじめに
株式会社日立製作所の松田元輝です。この度「Kubestronaut」に認定されたので、Kubestronautとはどのようなものなのかを紹介していきます。

Kubestronautとは
Kubestronautは、2024年3月から開始された「Cloud Native Computing Foundation」 (以下、CNCF)のプログラムで、継続的に学習に励み、Kubernetesのスキルレベルを高めてきたコミュニティリーダーを表彰するものです。Kubestronautは、以下の5つのKubernetes関連認定資格すべてに合格した人に与えられます。

認定資格名	略称	概要
Kubernetes and Cloud Native Associate	KCNA	Kubernetesとクラウドネイティブエコシステムの基本的な知識があることを証明する認定資格
Kubernetes and Cloud Security Associate	KCSA	セキュリティに関する基礎知識を証明する認定資格
Certified Kubernetes Administrator	CKA	Kubernetesクラスター管理に必要なスキルと知識を証明する認定資格
Certified Kubernetes Application Developer	CKAD	Kubernetes上でクラウドネイティブアプリケーションを設計、構築、デプロイする能力を証明する認定資格
Certified Kubernetes Security Specialist	CKS	コンテナベースのアプリケーションやKubernetesクラスターのセキュリティを確保する能力を証明する認定資格
なお、5つの認定資格の有効期限は2年間で、Kubestronautに認定されるには5つすべての認定資格が有効な状態である必要があります。詳しくは公式ページをご覧ください。

Kubestronautを取得するメリット
Kubestronautにはさまざまな特典が付きます。まず、Kubestronautに認定されると、限定ジャケットとCredlyのバッジが授与されます。


Kubestronautに授与される限定ジャケットとCredlyバッヂ

また、Kubestronaut Programの公式ページに名前やプロフィールが掲載されます。私の場合はこのように紹介されています。

そして、Kubestronaut専用Slackチャンネル、メーリングリストを通じて、世界中のKubestronautとコミュニケーションを取ることができます。

さらに、CNCF関連の資格クーポンとイベントクーポンが受け取れます。対象とする5つの資格に対して毎年50%オフクーポンが配られ、譲渡可能です。私が受け取ったクーポンはどのCNCF資格にも使用でき、例えばPrometheus Certified Associateなどにも使えるものでした。CNCFイベント用には、年3回20%オフのクーポンが利用できます。

各資格の概要と攻略法
CNCFが提供するKubernetesの認定試験は2つの試験形式があります。1つは選択式で、KCNAとKCSAが該当します。もう1つはハンズオン形式で、実際にKubernetesのクラスターを触りながらワークロードのデプロイ、ネットワークの設定、クラスターの設定、トラブルシュートを行います。また、試験中、公式ドキュメントを見ることができます。CKA、CKAD、CKSがこのハンズオン形式に当たります。

また、私の独断と偏見による各資格の難易度を示します。

認定資格	難易度	感想
KCNA	★☆☆☆☆	簡単です
KCSA	★★☆☆☆	内容は簡単です。英語が難しいです
CKA	★★★★☆	基本的なことも多いので、普段Kubernetesを使っている人なら少し勉強すれば取れそうです
CKAD	★★★★☆
CKS	★★★★★★★	覚悟して挑みましょう
それでは、Kubestronautに必要な各資格について、それぞれ概要を説明していきます。

Kubernetes and Cloud Native Associate (KCNA)
KCNAは、Kubernetesとクラウドネイティブエコシステムの基本的な知識があることを証明する資格です。

Kubernetesのアーキテクチャー、Kubernetesのリソース、ネットワーク、ストレージ、モニタリングなどが問われます。また、CI/CDやGitOpsなどKubernetes周辺のエコシステムについても問われます。

【公式ページ】Kubernetes and Cloud Native Associate (KCNA)

アソシエイト資格ということもあり、難易度は低いと感じました。私は他の資格を全て取った後に受けたので、特に対策しませんでした。

Kubernetes and Cloud Security Associate (KCSA)
KCSAは、Kubernetesのセキュリティに関する基礎知識を証明する資格です。

kube-api serverやRBAC、kubelet、コンテナランタイム、サービスメッシュなど、Kubernetesとその周辺に関わるセキュリティの知識はもちろんのこと、STRIDEモデルなどセキュリティ一般に関わる知識も問われます。

【公式ページ】Kubernetes and Cloud Security Associate (KCSA)

2024年9月現在、KCSAは英語での受験しかできません。また、前述のKCNAと比べると難しいのですが、やはりアソシエイト資格なので、英語ということを除けば、あまり難しくはありませんでした。私はUdemyで購入した模試を2回分解いて挑みました。

Certified Kubernetes Administrator (CKA)
CKAはKubernetesクラスター管理に必要なスキルと知識を証明する資格です。

Kubernetesクラスターの構築、トラブルシューティングなどのクラスターの管理タスクと、DeploymentやServiceなどの基本的なKubernetesのリソース操作を問われます。

【公式ページ】Certified Kubernetes Administrator (CKA)

私はKodeKloudのCKA対策とCKAを購入すると付いてくるKiller Shellの模試で勉強しました。基本的な操作はともかく、Kubernetesクラスターの管理はある程度の勉強が必要でした。

Certified Kubernetes Application Developer (CKAD)
CKADは、Kubernetes上でクラウドネイティブアプリケーションを設計、構築、デプロイする能力を証明する資格です。

Kubernetesでのアプリケーション開発に特化した知識が問われます。そのため、コンテナのビルド、Deploymentのアップデートストラテジー、CronJob、サイドカーパターンなど、アプリケーション開発に必要な内容が多くなります。

【公式ページ】Certified Kubernetes Application Developer (CKAD)

有志の方々が作成したCKAD-exercisesという問題集とCKADを買うと付いてくるKiller Shellの模試で勉強しました。Deploymentのアップデートストラテジーの設定や、CronJobのスケジューリングの設定など細かい内容も聞かれるので、試験前に今一度見直しておくと良いでしょう。

Certified Kubernetes Security Specialist (CKS)
CKSは、コンテナベースのアプリケーションやKubernetesクラスターのセキュリティを確保する能力を証明する資格です。

Kubernetesクラスターのセキュリティ、Dockerfileやマニフェストのセキュアな書き方、サプライチェーンセキュリティ、システムモニタリングなど、KubernetesそのものやKubernetesで運用するアプリケーションのセキュリティについて問われます。CKAの上位資格だけあって、監査ログの設定やFalcoの設定など、かなり細かいところまで問われます。

【公式ページ】Certified Kubernetes Security Specialist (CKS)

私は、KodeKloudのCKS対策とCKSを購入すると付いてくるKiller Shellの模試を解いて挑みました。1か月勉強しましたが、73点(合格は67点)とギリギリのスコアでした。CKSだけ段違いに難しいので、しっかり勉強時間を確保することをお勧めします。

おわりに
本記事では、Kubernetesの資格を全て取得すると得られる称号「Kubestronaut」について紹介しました。

資格勉強は大変でしたが、勉強を通して新しい知識を得ることができたり、今まで知らなかったKubernetesの機能に気付いたりすることができました。また、Kubestronaut関連でCNCJから声がかかり、OSS Summit JapanのCo-Locatedイベントで登壇する機会もいただけました。

皆さんも、ぜひチャレンジしてみてください。特にCKA、CKAD、CKSはハンズオン形式なので、勉強した知識を実務にも生かしやすく、試験自体も面白いですよ。