以下は **「man / --help だけを頼りに」** 問題を解くときの“思考パス”と、実際に打つコマンド例です。  
（スクショにある **/opt/course/11/image** の Dockerfile を修正 → Docker & Podman でビルド／プッシュ → Podman で起動 → ログをファイルに保存 というタスク）

---

## 0 . 事前準備

```bash
ssh ckad9043                  # 問題に書かれているノードへ
sudo -i                       # 以降 root 前提
cd /opt/course/11/image
```

---

## 1 . Dockerfile を修正

### help の使い方

```bash
docker build --help | less    # -t/--tag が何かを確認
```

### 作業

```bash
vi Dockerfile
# 既存の ENV 行を以下に置き換え
ENV SUN_CIPHER_ID=5b9c1065-e39d-4a43-a04a-e59bcea3e03f
:wq
```

---

## 2 . Docker でビルド → プッシュ

```bash
# --help で -t と context (=最後の .) の位置を確認
docker build -t registry.killer.sh:5000/sun-cipher:v1-docker .
docker push  registry.killer.sh:5000/sun-cipher:v1-docker
```

> ヒント検索例
> 
> ```bash
> docker --help | grep build
> docker build --help | grep '\-t,'
> docker push --help    # オプション不要なことを確認
> ```

---

## 3 . Podman でビルド → プッシュ

```bash
podman build -t registry.killer.sh:5000/sun-cipher:v1-podman .
podman push  registry.killer.sh:5000/sun-cipher:v1-podman
```

> **man podman-build** でオプションが Docker と互換であることを確認できます。

---

## 4 . Podman でコンテナを detatch 起動

### help の確認

```bash
podman run --help | less      # -d / --name の位置を確認
```

### 実行

```bash
podman run -d --name sun-cipher registry.killer.sh:5000/sun-cipher:v1-podman
```

---

## 5 . ログをファイルへ出力

```bash
mkdir -p /opt/course/11/logs
podman logs sun-cipher > /opt/course/11/logs/sun-cipher
```

> `podman logs --help` で **NAME** を渡す形式と  
> `> file` リダイレクトが使えることを確認。

---

## 6 . 動作チェック

```bash
podman ps                    # コンテナが Up しているか
ls -l /opt/course/11/logs
head /opt/course/11/logs/sun-cipher
```

---

### まとめ：man / --help を駆使する“型”

1. **コマンドの存在確認**
    
    ```bash
    docker --help | grep build
    ```
    
2. **サブコマンド個別のオプション調査**
    
    ```bash
    docker build --help | grep '\-t'
    man podman-run            # :/^-d で検索
    ```
    
3. **試し打ち & 失敗→オプション再確認**
    
4. **成功したら一連をスクリプト感覚で実行**
    

この流れを覚えておけば、外部ドキュメントがなくてもコンテナ系タスクを確実に解けます。 CKAD 本番でも同じ手順で進めてください。Good luck!