# Claude Code 引き継ぎガイド（ローカル環境不要版）

## 概要

「Claude Code on the web」を使うことで、PCにファイルを置かずに
GitHubリポジトリ上で直接Claude Codeに作業させることができます。
ブラウザだけで完結します。

---

## 前提条件

- Claude Pro / Max / Team / Enterprise いずれかのプラン
- GitHub アカウント

---

## ステップ1：GitHubにリポジトリを作成し、ファイルをアップロード

### 1-1. リポジトリ作成

1. GitHub（github.com）にログイン
2. 右上の「+」→「New repository」
3. 以下を設定：
   - Repository name：`kujiramonaka-lp`（任意）
   - Public または Private：どちらでもOK
   - 「Add a README file」にチェックを入れる
4. 「Create repository」をクリック

### 1-2. フォルダ構成を作成してファイルをアップロード

GitHub上でファイルをアップロードします。

**画像のアップロード：**

1. リポジトリのページで「Add file」→「Upload files」
2. まず、アップロード画面のパス欄に `assets/images/` と入力
   （GitHubが自動でフォルダを作成します）
3. 以下の3ファイルをドラッグ＆ドロップ：
   - `Hero用_もしも猫展巾着サンプル.png` → アップロード後に `hero.png` にリネーム
   - `商品写真用_招き猫もなか4個入りサンプル.png` → `monaka.png` にリネーム
   - `商品写真用_もしも猫展巾着サンプル開き.png` → `kinchaku.png` にリネーム

※ GitHubのWebUIでは直接リネームしにくいので、
  最初からファイル名を変更してからアップロードするのが簡単です。

4. 「Commit changes」をクリック

**HTMLのアップロード：**

1. 再度「Add file」→「Upload files」
2. Claude.aiからダウンロードした `招き猫もなか_LP_v3.html` を
   `index.html` にリネームしてアップロード
3. 「Commit changes」をクリック

### 1-3. CLAUDE.md を作成

1. リポジトリのトップで「Add file」→「Create new file」
2. ファイル名に `CLAUDE.md` と入力
3. 以下の内容を貼り付け：

---

```markdown
# くじらもなか本舗 季節限定LP

## プロジェクト概要
仙台の老舗和菓子店「くじらもなか本舗」の季節限定商品用ランディングページ。
SNS（Instagram等）や広告からの流入を受け、HP内のカート機能へ誘導する導線設計。

## 現在の商品
- 商品名：招き猫もなか 猫展限定セット
- 価格：¥1,850（税込）
- 販売期間：2026年4月17日（金）〜 6月7日（日）
- コラボ：ミヤギテレビ主催「もしも猫展」（歌川国芳フィーチャー）
- セット内容：招き猫もなか + 猫展限定デザイン巾着袋（大きめ）
- 製造：くじらもなか本舗（保存料・着色料不使用）
- 購入リンク先：https://kujiramonaka.jp/products/season01

## 店舗情報
- 店名：くじらもなか本舗
- 住所：〒980-0821 宮城県仙台市青葉区春日町10-23 春山ビル1階 B号室
- TEL：022-261-4490
- 公式サイト：https://kujiramonaka.jp

## 技術仕様
- 単一HTMLファイル（index.html）
- 外部依存：Google Fonts（Noto Serif JP, Cormorant Garamond）
- 画像：assets/images/ ディレクトリに格納
- レスポンシブ対応済み（モバイルファースト）
- JavaScript：Intersection Observer によるスクロールアニメーション
- CSSのみでアニメーション（ライブラリ不使用）

## デザイン方針
- トーン：伝統的・老舗感 × プロフェッショナル・スタイリッシュ
- カラー：温かみのあるベージュ系背景、ダークブラウンの文字、赤茶（#8B3A2F）アクセント
- フォント：Noto Serif JP（本文）+ Cormorant Garamond（英字アクセント）
- レイアウト：1カラム縦スクロール「一直線スクロール型」

## ページ構成（上から順に）
1. Hero（全画面写真 + コピー + CTA）
2. 期間バー（販売期間の帯）
3. イントロ（コラボの紹介文）
4. 商品紹介（写真ギャラリー + 商品詳細 + 価格）
5. こだわり（素材・製法 3項目）
6. 販売情報（テーブル + CTA）
7. フッター（店舗情報 + SNSリンク）

## 導線設計
- SNS/広告 → LP（このページ）→ HPカート（kujiramonaka.jp）
- CTAボタン：Hero内 と 販売情報セクションの2箇所
- リンク先はすべて https://kujiramonaka.jp/products/season01

## 今後の運用
- 季節ごとに商品が変わるため、画像・テキスト・リンクを差し替えて再利用する設計
- Hero画像のインパクトを重視した構造

## コーディングルール
- HTMLはセマンティックに記述
- CSSはCSS変数（:root）で色・フォントを一元管理
- クラス名は短縮形を使用（.r = reveal, .v = visible など）
- 画像はbase64埋め込みではなく、assets/images/ からの相対パスで参照すること
```

---

4. 「Commit new file」をクリック

この時点で、リポジトリの中身は以下のようになっているはずです：

```
kujiramonaka-lp/
├── index.html
├── assets/
│   └── images/
│       ├── hero.png
│       ├── monaka.png
│       └── kinchaku.png
├── CLAUDE.md
└── README.md
```

---

## ステップ2：Claude Code on the web を起動

1. ブラウザで **claude.ai/code** にアクセス
2. 初回はGitHubアカウントの連携を求められるので、画面に従って認証
3. Claude GitHub App のインストール画面が出たら、
   先ほど作成したリポジトリにアクセスを許可
4. リポジトリ選択画面で `kujiramonaka-lp` を選択

---

## ステップ3：Claude Code にタスクを依頼

以下のプロンプトを順番に投げてください。
各タスクが完了するとClaude Codeが自動でブランチを作成し、
PRを作れる状態になります。

---

### タスク①：base64画像を外部ファイル参照に変換

```
index.html の画像を base64 埋め込みから外部ファイル参照に変換してください。

現在の状態：
- .hero-img の CSS background に base64 PNG が埋め込まれている
- <img> タグの src にも base64 PNG が埋め込まれている

変換後のパス：
- Hero背景 → background: url('assets/images/hero.png') center/cover no-repeat;
- 招き猫もなか写真の img → src="assets/images/monaka.png"
- 巾着袋（開いた状態）の img → src="assets/images/kinchaku.png"
- 巾着袋（使用イメージ）の img → src="assets/images/hero.png"

画像ファイルは assets/images/ に配置済みです。
base64データをすべて削除してファイルサイズを軽量化してください。
```

---

### タスク②：OGPタグの追加（SNSシェア対策）

```
index.html の <head> 内に OGP タグを追加してください。
Instagram や X でシェアされた際にプレビュー画像が表示されるようにします。

設定内容：
- og:title → 招き猫もなか 猫展限定セット｜くじらもなか本舗
- og:description → 歌川国芳「もしも猫展」コラボ限定。仙台の老舗くじらもなか本舗が手がける招き猫もなか＋限定巾着セット。4/17〜6/7期間限定販売。
- og:image → assets/images/monaka.png（デプロイ後に絶対URLに要変更、コメントで明記）
- og:type → website
- og:url → （TODO: 本番URL決定後に設定、とコメントで明記）
- twitter:card → summary_large_image
- twitter:title, twitter:description, twitter:image も同様に設定
```

---

### タスク③：本番デプロイ（GitHub Pages が最も簡単）

```
このリポジトリを GitHub Pages で公開する設定をしてください。

要件：
- 独自ドメインは不要（github.io のサブドメインでOK）
- main ブランチの / (root) を公開ソースにする
- 公開後のURLが確定したら、index.html 内の OGP タグの
  og:url と og:image を絶対URLに更新する

手順がある場合はステップごとに教えてください。
```

※ GitHub Pages の設定自体はリポジトリの Settings > Pages から
手動で行う必要がある場合があります。
Claude Code が手順を案内してくれます。

---

### タスク④（今後用）：季節商品の差し替えテンプレート

次の季節に商品を差し替える際は、以下のプロンプトの空欄を埋めて投げるだけです：

```
季節限定LPの商品を差し替えます。以下の情報で index.html を更新してください。

■ 新商品情報
- 商品名：
- 価格：
- 販売期間：
- コラボ/テーマ：
- セット内容：
- 購入リンク：
- 商品説明：

■ 画像
- assets/images/ に新しい画像を配置済み
- Hero画像のファイル名：
- 商品写真のファイル名：

■ 更新対象
- ページタイトル（<title>タグ）
- meta description
- OGPタグ（og:title, og:description, og:image）
- Hero セクションのテキストとCTA
- 商品セクションの写真・テキスト・価格
- 販売情報テーブル
- CLAUDE.md の商品情報セクション
```

---

## ステップ4：PRをレビューしてマージ

Claude Code on the web は作業が完了すると、
変更内容の差分（diff）を画面上で確認できます。

1. 変更内容を diff ビューで確認
2. 問題があればコメントで修正を依頼（Claude が自動で対応）
3. 問題なければ「Create PR」でプルリクエストを作成
4. GitHub上でPRをマージ

---

## 全体の流れまとめ

```
┌─────────────────────────────────────────────────┐
│  ステップ1：GitHub にリポジトリを作成            │
│  　・README付きで新規作成                        │
│  　・画像3枚を assets/images/ にアップロード     │
│  　・index.html をアップロード                   │
│  　・CLAUDE.md を作成                            │
├─────────────────────────────────────────────────┤
│  ステップ2：claude.ai/code にアクセス            │
│  　・GitHub連携 → リポジトリ選択                 │
├─────────────────────────────────────────────────┤
│  ステップ3：タスクを依頼                         │
│  　①  base64 → 画像ファイル参照に変換           │
│  　②  OGPタグ追加                               │
│  　③  GitHub Pages デプロイ設定                  │
├─────────────────────────────────────────────────┤
│  ステップ4：PR をレビュー → マージ               │
│  　・diff確認 → Create PR → Merge               │
└─────────────────────────────────────────────────┘
```

---

## 補足

### ローカルのClaude Code（ターミナル版）との違い

| | Claude Code on the web | Claude Code（ターミナル） |
|---|---|---|
| 環境 | ブラウザだけでOK | PCにインストールが必要 |
| ファイル | GitHub上で完結 | ローカルにクローンが必要 |
| 結果 | 自動でブランチ作成・PR | ローカルで変更後、手動push |
| 向いている作業 | 定型タスク、並列作業 | 対話的な試行錯誤、未コミットの作業 |

### 注意点

- Claude Code on the web はリポジトリを仮想環境にクローンして作業します。
  あなたのPCのファイルには一切触れません。
- 作業結果は新しいブランチにpushされ、PRとして提案されます。
  main ブランチに直接変更が入ることはありません（マージするまで安全）。
- ネットワークアクセスはデフォルトで制限されていますが、
  Google Fonts の読み込み等に必要な場合は設定で許可できます。
