# Discord Widget (Static Profile System)

GitHub Pages + Discord Internal API を使った静的プロフィールウィジェット。

サーバー不要でプロフィールカードを構築する仕組み。

---

# 🧭 Step 1: Repository Setup

## 1. GitHubリポジトリ作成
- 任意の名前でリポジトリ作成
- Publicに設定

## 2. GitHub Pages有効化
- Settings → Pages
- Branch: `main`
- `/ (root)` を選択

---

# 🖼 Step 2: Assets準備

## 1. 画像配置

```

/images
├─ tutu-mlnpn.png
├─ twitter.png
├─ github.png
├─ operators.png
└─ mbti.png

```

## 2. 公開URL確認

GitHub Pagesで以下形式になる：

```

https://<username>.github.io/<repo>/images/xxx.png

````

---

# 📦 Step 3: Widget JSON作成

## 1. 基本構造

```json
{
  "username": "your-name",
  "data": {
    "dynamic": [
      {
        "type": 3,
        "name": "Image",
        "value": {
          "url": "IMAGE_URL"
        }
      }
    ]
  }
}
````

---

## 2. 実際の例

```json
{
  "username": "tutu-mlnpn",
  "data": {
    "dynamic": [
      {
        "type": 3,
        "name": "Image",
        "value": {
          "url": "https://tutu-mlnpn.github.io/discord-widget/images/tutu-mlnpn.png"
        }
      },
      {
        "type": 1,
        "name": "Text",
        "value": "tutu22 / ツツ"
      },
      {
        "type": 1,
        "name": "Subtitle",
        "value": "Melon Pan / Cats / Music / Anime / Liminal Spaces"
      }
    ]
  }
}
```

---

# 🔐 Step 4: Discord Application作成

## 1. Developer Portal

* [https://discord.com/developers/applications](https://discord.com/developers/applications)

## 2. Application作成

* New Application

## 3. Bot作成

* Botタブ → Add Bot

## 4. 必要情報取得

* Application ID
* User ID
* Bot Token

---

# 🚀 Step 5: Widget登録（PATCH）

## 1. 実行コマンド

```bash
curl -X PATCH \
"https://discord.com/api/v9/applications/APP_ID/users/USER_ID/identities/0/profile" \
-H "Content-Type: application/json" \
-H "Authorization: Bot YOUR_BOT_TOKEN" \
-d 'JSON_STRING'
```

---

## 2. 置換箇所

```
APP_ID        → Application ID
USER_ID       → Discord User ID
BOT_TOKEN     → Bot Token
JSON_STRING   → JSON.stringifyしたWidgetデータ
```

---

## 3. 成功例

```
HTTP/2 204 No Content
```

→ 成功（何も返らないのが正常）

---

# 🔁 Step 6: 更新方法

## 1. 画像変更

* /images 更新
* GitHub push

## 2. テキスト変更

* widget.json編集
* JSON再生成

## 3. Discord反映

* 再度PATCH実行

---

# 👀 Step 7: 表示確認

## 1. リロード

* Discord再起動 or Cmd + R

## 2. プロフィール確認

* Widgetが追加されているか確認

---

# ⚙️ System Behavior

* データはDiscord側に保存される
* GitHub Pagesは画像ホスティングのみ
* 完全サーバーレス構成

---

# ⚠️ 注意事項

* Bot Tokenは絶対に公開しない
* internal APIは仕様変更される可能性あり
* widget.jsonはローカル管理推奨

---

# 📌 Architecture

```
GitHub Pages
    ↓
画像ホスティング

Widget JSON
    ↓
Discord PATCH API

Discord Profile
    ↓
Widget表示
```

---

# 🧠 Summary

* 静的サイトだけで構築可能
* サーバー不要
* Discordプロフィールを拡張
* GitHub + Discord APIで完結