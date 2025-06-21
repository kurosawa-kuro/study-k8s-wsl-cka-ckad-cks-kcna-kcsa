思考時間: 6 秒

### CKAD‑JP に直結する Udemy コース優先度リスト

（※リスト内＝すでに購入済みコースからピックアップ）

| 優先     | コースタイトル                                                                             | 位置づけ / 目的                                                   | おすすめの使い方                                   |
| ------ | ----------------------------------------------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------ |
| **★1** | **認定Kubernetesアプリケーション開発者 (CKAD) 演習問題集【2024年版】**（NZ Cloud）                          | **本命の日本語演習コース**・出題範囲を日本語で網羅・模擬問題 → 解説 YAML 付き               | 本番 2 週間前から **毎晩 1 セクション** → スコア 80 % 越えを目標 |
| **★2** | **Kubernetes Operator 入門**（Masato Naka）                                             | Pod/Deployment/ConfigMap/Probes など **CKAD ドメイン基礎** を丁寧に解説   | 1.5× 再生で **ブロックごとに写経** → alias に登録         |
| **★3** | **Kubernetes for Beginners: Google Cloud, AWS & Azure [2020]**（in28Minutes）         | Imperative コマンド練習に最適（`kubectl create … --dry-run` のフォームが多い） | 1 章＝40 分想定で **平日夕方に 1 章ずつ**                |
| 4      | **Learn DevOps: The Complete Kubernetes Course**（Edward Viaene）                     | Service/Ingress/Volumes/Helm 章が CKAD 出題範囲と深く重なる             | 必要章だけピンポイント再生（目次クリック）                      |
| 5      | **Certified Kubernetes Administrator (CKA) with Practice Tests**（KodeKloud/Mumshad） | CKAD より広いが **Troubleshoot / NetworkPolicy** 章のハンズオンが強い      | 模擬問題パートを “CKAD 予行演習” として利用                 |
| 6      | **Docker + Kubernetes で構築する Webアプリケーション 実践講座**（津郷 先生）                               | 日本語で Deployment→Service→Ingress 一連をハンズオン                    | 完全未経験章があれば補完教材として                          |
| 7      | **米DevOpsエンジニア監修！Kubernetesの登竜門CKAD模擬試験問題とハンズオン解答集**                                | 模擬試験 2 セット相当                                                | 直前期に “時間制限 2 h” で通し演習                      |
|        |                                                                                     |                                                             |                                            |

> **CKAD‑JP だけ狙うなら★1〜3で 80 % 以上カバー**  
> ★4〜★7 は弱点補強 or 追加ハンズオンとして使えば OK。

---

## 具体的な活用フロー（50 h プランに当てはめ）

|フェーズ|時間|コース & 章|目的|
|---|---|---|---|
|**Week 1 (基礎固め)**|18 h|★2 全章 & ★3 主要章|Pod/Container/Config/Probe/Service 基礎を手打ちで暗記|
|**Week 1 末〜Week 2 前半**|12 h|★1 模擬問題 Part 1‑3|日本語で CKAD 出題パターン把握|
|**Week 2 後半**|8 h|★4 Helm/Ingress/Volumes 章 + ★5 Troubleshoot 章|苦手分野を補強|
|**直前 3 日**|8 h|★1 模擬 Part 4‑5 + ★7 1 回通し|時間配分とコマンド速度を最適化|
|**前日**|4 h|★1/7 の間違えた問題だけ再演習|取りこぼしゼロへ|

---

### 4 h 勉強ブロック例（平日）

1. **50 分** — ★2 または ★3 で動画視聴＋写経
    
2. **80 分** — 同章ハンズオン：`kubectl create … --dry-run -o yaml` → 修正 → `apply`
    
3. **20 分** — スライド/公式 docs を “日本語→英語” 対訳検索
    
4. **30 分** — ★1 演習問題 3 問
    
5. **40 分** — ハンズオンで詰まったコマンドを alias / cheatsheet 更新
    
6. **20 分** — 休憩＆ Slack に自分用メモ投稿（アウトプット）
    

---

## 補足 Tips

- **英語コースは 1.5×～1.75× 再生**＋日本語字幕 ON で時短
    
- 各コースの **k8s manifest は GitHub に置く** → 反復練習がしやすい
    
- 模擬試験は **VS Code＋tmux＋alias** 本番設定で行い、時間配分に慣れる
    
- ★5（KodeKloud CKA）は **`troubleshoot`、`network-policy`、`rbac`** 章だけ摘み食いで十分
    

---

> **結論：**  
> CKAD‑JP 合格までに“必修”なのは ★1‑3。  
> 残りのコースは **苦手分野用のサブ教材 or CKA への布石** として活用すればコスパ最強です。  
> これで動画迷子にならず一直線に CKAD‑JP 行けますよ💪