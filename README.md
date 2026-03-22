# slides-by-html

コーディングエージェント（Claude Code, Codex など）にプロンプトを投げるだけで、プロフェッショナルなプレゼンテーションスライドを生成できるリポジトリです。

多彩なレイアウトパターンと統一されたデザインシステムを備えており、エージェントはこれらを参照してスライドを作成します。

## 特徴

- コーディングエージェントへの指示だけでスライド生成
- 多彩なレイアウトパターン（データ可視化、比較、タイムライン、組織図など）
- 統一されたカラーシステムとタイポグラフィ
- Reveal.js によるブラウザ上でのプレゼンテーション
- DeckTape による PDF 出力

## 技術スタック

| カテゴリ           | ツール                                              |
| ------------------ | --------------------------------------------------- |
| プレゼンテーション | [Reveal.js](https://revealjs.com/) v5               |
| スタイリング       | [Tailwind CSS](https://tailwindcss.com/)（CDN）     |
| アイコン           | [Lucide](https://lucide.dev/)（CDN）                |
| PDF出力            | [DeckTape](https://github.com/astefanutti/decktape) |

## ディレクトリ構成

```
.
├── css/
│   └── theme-light.css          # カラーシステム・テーマ定義
├── layouts/
│   └── layout-patterns.html     # 68種のレイアウトパターン集
├── slides/                      # 生成されたスライド
├── .claude/
│   └── skills/
│       └── create-slide/        # スライド生成スキル
│           └── SKILL.md
├── CLAUDE.md
└── AGENTS.md
```

## 使い方

### スライドの作成

Claude Code でこのリポジトリを開き、`/create-slide` コマンドまたは自然言語で指示します。

#### プロンプト例

**シンプルな指示：**

```
/create-slide DX推進の社内提案資料
```

**詳細な指示：**

```
新規SaaSプロダクトの投資家向けピッチデッキを作成してください。
以下の構成でお願いします：

1. 表紙（プロダクト名: DataFlow）
2. 課題提起 — 企業のデータサイロ問題
3. ソリューション概要 — 3カラムで主要機能を紹介
4. 市場規模 — TAM/SAM/SOMの説明
5. 競合比較 — ハーベイボールで機能比較
6. ビジネスモデル — 3案比較の料金プラン
7. KPIダッシュボード — 主要指標4つ
8. ロードマップ — 3フェーズの開発計画
9. チーム紹介 — 経営陣4名
10. CTA — 問い合わせ・次のアクション
```

**テーマを指定した指示：**

```
Q3の営業報告スライドを作成してください。
棒グラフで四半期売上推移、ファネルで営業パイプライン、
Before/Afterで業務改善効果を見せたいです。
```

**Codex など他のエージェントでの利用：**

```
このリポジトリの layouts/layout-patterns.html と css/theme-light.css を
参照して、AI導入効果の社内報告スライドを slides/ai-report.html として
作成してください。Reveal.js + Tailwind CSS + Lucide アイコンを使用し、
絵文字は使わないでください。
```

### ブラウザでプレビュー

生成されたスライドはブラウザで直接開けます。

```bash
open slides/my-presentation.html
```

### PDF 出力

#### コーディングエージェントに依頼

スライド作成後、そのまま PDF 出力も依頼できます。

```
slides/my-presentation.html をPDFに変換してください
```

```
作成したスライドを npx decktape で PDF 出力してください。
サイズは 1920x1080 で、output/my-presentation.pdf に保存してください。
```

エージェントがローカルサーバーの起動から DeckTape の実行まで自動で行います。

#### npx（エンジニア向け）

Node.js がインストールされている環境では npx で直接実行できます。

```bash
# ローカルサーバーを起動（別ターミナル）
npx serve .

# PDF出力
npx decktape reveal http://localhost:3000/slides/my-presentation.html output.pdf
```

**オプション指定：**

```bash
# スライドサイズとページ送り間隔を指定
npx decktape reveal \
  --size 1920x1080 \
  --pause 1000 \
  http://localhost:3000/slides/my-presentation.html \
  output.pdf
```

## カラーシステム

`css/theme-light.css` で定義されたカラーパレット：

| 用途         | 変数名                 | Tailwind クラス                  |
| ------------ | ---------------------- | -------------------------------- |
| メインカラー | `--color-primary`      | `text-primary`, `bg-primary`     |
| サブカラー   | `--color-secondary`    | `text-secondary`, `bg-secondary` |
| アクセント   | `--color-accent`       | `text-accent`, `bg-accent`       |
| 強調テキスト | `--color-text-strong`  | `text-text-strong`               |
| 本文テキスト | `--color-text`         | `text-text-base`                 |
| 補助テキスト | `--color-text-muted`   | `text-text-muted`                |
| 背景/区切り  | `--color-neutral-1〜5` | `bg-neutral-1` 〜 `bg-neutral-5` |

## レイアウトパターン一覧

`layouts/layout-patterns.html` に収録されたパターン：

| カテゴリ             | 主なパターン                                     |
| -------------------- | ------------------------------------------------ |
| 構成・導入系         | 表紙、ヒーロー表紙、アジェンダ、セクション扉     |
| 紹介系               | 会社紹介、製品・サービス紹介                     |
| 基本文字レイアウト   | 2カラム、3カラム、大見出し+補足、引用、FAQ       |
| 比較・整理系         | 左右比較、SWOT、ベン図、課題→原因→打ち手         |
| 流れ・時間軸系       | ステップ、シェブロン、タイムライン、ロードマップ |
| データ・分析系       | KPI、棒グラフ、折れ線、ドーナツ、ガントチャート  |
| 画像・プロダクト系   | 全画面画像、スクリーンショット+注釈              |
| 人・組織・信頼形成系 | チーム紹介、組織図、顧客の声                     |
| 締め・補足系         | まとめ、CTA、Thank You、参考文献                 |
| 装飾コンポーネント   | パネルデザイン、カード・タグ・バッジ             |
