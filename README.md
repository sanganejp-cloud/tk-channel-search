# 📺 三兄弟ダディ TK チャンネル｜公開動画検索ページ

視聴者が「お金の悩み」を入力すると、該当する公開済み動画を検索できる静的サイトです。

## 公開 URL（例）

`https://sanganejp-cloud.github.io/tk-channel-search/`

## 構成

```
tk-channel-public/
├── index.html      検索ページ本体（Fuse.js でファジー検索）
├── videos.json    公開動画リスト（PC で生成 → ここに配置）
└── README.md       このファイル
```

## 初回セットアップ（1 回だけ）

### 1. GitHub アカウント作成（無料）

https://github.com/signup でアカウント作成。

### 2. リポジトリを作成

1. GitHub にログイン → 右上の「+」→「New repository」
2. **Repository name**: `tk-channel-search`（好きな名前で）
3. **Public**（無料の GitHub Pages を使うため）
4. 「Create repository」

### 3. ファイルをアップロード

このフォルダの 3 ファイル（`index.html` / `videos.json` / `README.md`）を、作成したリポジトリにアップロード。

**簡単な方法**：
- ブラウザで作成したリポジトリページを開く
- 「Add file」→「Upload files」
- 3 ファイルをドラッグ＆ドロップ
- 「Commit changes」

### 4. GitHub Pages を有効化

1. リポジトリ → 「Settings」（右上）
2. 左メニュー「Pages」
3. **Source**: 「Deploy from a branch」
4. **Branch**: `main` / `/ (root)` を選択して「Save」
5. 数分待つ
6. 同じページの上部に表示される URL がサイト URL

例：`https://sanganejp-cloud.github.io/tk-channel-search/`

### 5. （オプション）独自ドメイン設定

`tk-channel.com` のような独自ドメインを使いたい場合は、Pages の「Custom domain」欄に入力。詳しくは [GitHub Pages 公式ドキュメント](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site)。

---

## 動画リストの更新方法

新しい動画を投稿したら、`videos.json` を更新して GitHub に push します。

### 自動更新スクリプト（推奨）

PC の `03_制作スクリプト` フォルダで：

```bash
python dump_public_videos.py
```

すると `tk-channel-public/videos.json` が更新されます。

その後 GitHub に反映：

```bash
cd tk-channel-public
git add videos.json
git commit -m "新動画追加"
git push
```

→ GitHub Pages が自動再デプロイ（数分後にサイトに反映）

### 手動更新

1. PC の `videos.json` を上記スクリプトで生成
2. GitHub のリポジトリページで `videos.json` を編集 → 内容を貼り付け
3. 「Commit changes」

---

## 動画追加時の運用

```
新動画投稿
  ↓
Notion で YouTube/TikTok/Instagram URL を入力
  ↓
PC で `dump_public_videos.py` 実行
  ↓
`videos.json` 更新
  ↓
git push
  ↓
数分後、視聴者の検索ページに反映
```

---

## SEO 設定（オプション）

サイトを Google 検索に表示させるには：

1. [Google Search Console](https://search.google.com/search-console) にサイト登録
2. サイトマップ送信（`sitemap.xml`）
3. Google アナリティクス 4 を設定（アクセス解析）

希望があれば実装サポートします。

---

## トラブルシューティング

**Q. サイトが「404 Not Found」になる**
A. GitHub Pages の有効化に数分かかります。10 分待ってリロード。

**Q. 検索しても結果が出ない**
A. `videos.json` が空 or 配置されていない可能性。ブラウザで `https://sanganejp-cloud.github.io/tk-channel-search/videos.json` を直接開いて中身を確認。

**Q. 動画タイトルだけ表示されて URL リンクが出ない**
A. `videos.json` の `yt` / `tt` / `ig` フィールドが空。Notion で URL 入力 → `dump_public_videos.py` 再実行。

---

## カスタマイズ

- 色テーマ：`index.html` の `<style>` 内 `linear-gradient` を変更
- フォント：`font-family` を変更
- ヒーロー文言：`<h1>` と `.sub` を編集
- 例示チップ：`.examples` 内の `<div class="ex-chip">` を増減
