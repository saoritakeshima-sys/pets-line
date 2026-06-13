# PETS LINE

ペットシッター検索・依頼プラットフォームの静的HTMLアプリです。  
**React / Next.js 不要。** HTMLファイル2枚だけで動きます。

---

## ファイル構成

```
pets-line/
├── index.html      # お客様向け：シッター検索・依頼フォーム
├── sitter.html     # シッター向け：管理ダッシュボード
├── vercel.json     # Vercel デプロイ設定
└── README.md
```

---

## ローカルでの起動方法

### 方法①　ファイルをダブルクリック（最速）
`index.html` または `sitter.html` をブラウザで直接開くだけで動きます。  
> ⚠️ AIチャット機能（Anthropic API呼び出し）はブラウザのCORS制限で動かない場合があります。その場合は方法②を使ってください。

### 方法②　ローカルサーバーを立てる（推奨）

**Node.js がある場合：**
```bash
cd pets-line
npx serve .
# → http://localhost:3000 で起動
```

**Python がある場合：**
```bash
cd pets-line
python3 -m http.server 8080
# → http://localhost:8080 で起動
```

**VS Code がある場合：**  
Live Server 拡張を使うと `index.html` を右クリック → "Open with Live Server" で起動できます。

---

## Vercel でのデプロイ手順

### ① Vercel CLIを使う方法

```bash
# Vercel CLI をインストール（初回のみ）
npm install -g vercel

# プロジェクトフォルダに移動
cd pets-line

# デプロイ
vercel

# 本番公開
vercel --prod
```

初回は対話式で設定します：
- `Set up and deploy?` → **Y**
- `Which scope?` → 自分のアカウントを選択
- `Link to existing project?` → **N**（新規の場合）
- `What's your project's name?` → `pets-line`（任意）
- `In which directory is your code located?` → `.`（そのまま Enter）
- `Override settings?` → **N**

### ② GitHub連携でデプロイする方法（自動デプロイ）

1. GitHubにリポジトリを作成
2. `pets-line` フォルダをプッシュ
   ```bash
   git init
   git add .
   git commit -m "initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_NAME/pets-line.git
   git push -u origin main
   ```
3. [vercel.com](https://vercel.com) → `Add New Project` → GitHubリポジトリを選択
4. 設定はすべてデフォルトのまま → `Deploy`

以降は `main` ブランチにプッシュするたびに自動で再デプロイされます。

---

## ビルドコマンド

このプロジェクトは**静的HTMLのみ**のため、ビルド工程は不要です。

Vercel の設定画面では以下のように設定してください：

| 項目 | 設定値 |
|------|--------|
| Framework Preset | `Other` |
| Build Command | （空欄のまま） |
| Output Directory | `.`（ルートディレクトリ） |
| Install Command | （空欄のまま） |

---

## 公開後のURL

| 画面 | URL |
|------|-----|
| お客様向け（シッター検索） | `https://YOUR-PROJECT.vercel.app/` |
| シッター向け（管理画面） | `https://YOUR-PROJECT.vercel.app/sitter` |

---

## 公開前チェック項目

### 機能チェック
- [ ] `index.html`：シッターカードをクリックして詳細ページに遷移できる
- [ ] `index.html`：フィルターチップで絞り込みが動く
- [ ] `index.html`：依頼フォームをステップ1→2→3まで進められる
- [ ] `index.html`：AIチェック（ステップ3）でAnthropicのAPIが呼ばれ返答が返る
- [ ] `sitter.html`：サイドバーの各メニューをクリックしてページが切り替わる
- [ ] `sitter.html`：「メッセージ」画面でスレッドを開き返信できる
- [ ] `sitter.html`：「✨ AI下書き」ボタンでAI返信文が生成される
- [ ] `sitter.html`：「売上・収益」画面で棒グラフが描画される
- [ ] `sitter.html`：口コミの「AI返信文を生成」が動く

### モバイルチェック（スマートフォン実機 or Chrome DevTools）
- [ ] `index.html`：シッター一覧が縦1列で表示される（480px以下）
- [ ] `index.html`：検索バーが縦積みになる
- [ ] `index.html`：依頼フォームのボタンが横並びにならず押せる
- [ ] `sitter.html`：ハンバーガーメニュー（☰）が表示される
- [ ] `sitter.html`：☰ をタップするとサイドバーが開閉する
- [ ] `sitter.html`：「メッセージ」でスレッドをタップすると全画面チャットが開く
- [ ] `sitter.html`：「← スレッド一覧に戻る」で戻れる

### 表示チェック
- [ ] iOSのSafariで崩れがない（特にフォント・ボタン）
- [ ] 文字が小さすぎず読める（最小12px以上）
- [ ] タップ領域が十分に広い（44px以上推奨）

### API・セキュリティ
- [ ] Anthropic APIキーがHTMLにハードコードされていない（このアプリはAPIキーなしでもUIは動作します）
- [ ] 本番運用の際は `/api` プロキシ経由でAPIキーをサーバー側に隠すこと

---

## 注意事項

- このアプリはフロントエンドのみのデモです。データは保存されません（リロードでリセット）
- AI機能（返信生成・見積もりチェック）はAnthropicのAPIを使用します
- 本番運用する場合は、APIキーをVercel環境変数で管理し、サーバーレス関数経由で呼び出す構成に変更してください
