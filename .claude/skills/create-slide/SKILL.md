---
name: create-slide
description: Create a Reveal.js presentation slide deck from user requirements. Reads layout pattern references and generates complete HTML files with proper styling, Tailwind CSS, and Lucide icons.
argument-hint: [topic or outline]
---

# Create Slide

You are a presentation slide builder. Generate a complete Reveal.js HTML slide deck based on the user's topic or outline provided in `$ARGUMENTS`.

## Step 1: Read references

Before writing any code, read the following files to understand the project's conventions:

1. **Layout patterns reference**: `layouts/layout-patterns.html` — contains 68 slide layout examples organized by category. Read specific sections relevant to the user's request rather than the entire file.
2. **Theme CSS**: `css/theme-light.css` — the color system and component styles.

## Step 2: Plan the slide structure

Based on the user's input, plan which layout patterns to use for each slide. Choose the most appropriate layout for the content:

### Available layout categories and when to use them

| Category | Patterns | Use for |
|----------|----------|---------|
| 構成・導入系 | 表紙, ヒーロー表紙, アジェンダ, セクション扉, エグゼクティブサマリー, 1メッセージ | Opening, navigation, section breaks |
| 紹介系 | 会社紹介, 製品・サービス紹介 | Company/product overviews |
| 基本文字レイアウト | タイトル+本文, 2カラム均等/6:4/4:6, 3カラム, 大見出し+補足, 引用, FAQ | General content, text-heavy slides |
| 比較・整理系 | 左右比較, 3案比較, Pros/Cons, Before/After, 2x2マトリクス, SWOT, ベン図, 課題→原因→打ち手 | Comparisons, analysis, decision support |
| 流れ・時間軸系 | ステップ型(横/縦), シェブロン, タイムライン(横/縦), ロードマップ, チェックリスト | Processes, timelines, progress |
| データ・分析系 | KPIダッシュボード, 棒グラフ(縦/横/積み上げ/100%), 折れ線, ドーナツ, 表, ファネル, ウォーターフォール, 散布図, ガントチャート, グラフ+表複合, ハーベイボール, 推移チャート | Data visualization, metrics |
| 画像・プロダクト系 | 全画面画像, 画像+テキスト(左/右), 複数画像(2枚/グリッド), 背景画像(右側), スクリーンショット+注釈 | Visual content, product demos |
| 人・組織・信頼形成系 | チーム紹介, 組織図, 顧客の声, ロゴ実績, パートナー | Team, social proof, credibility |
| 締め・補足系 | まとめ, CTA, Thank You, 連絡先, Appendix表紙, 参考文献 | Closing, next steps, references |

## Step 3: Generate the HTML file

Create the HTML file in the `slides/` directory. Use the filename format: `slides/<topic-slug>.html`

### HTML boilerplate

Every slide deck MUST use this exact boilerplate:

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <title>SLIDE_TITLE</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/reveal.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/theme/white.css">
  <link rel="stylesheet" href="../css/theme-light.css">
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: { DEFAULT: 'var(--color-primary)', light: 'var(--color-primary-light)', dark: 'var(--color-primary-dark)' },
            secondary: { DEFAULT: 'var(--color-secondary)', light: 'var(--color-secondary-light)' },
            accent: { DEFAULT: 'var(--color-accent)', light: 'var(--color-accent-light)' },
            'text-strong': 'var(--color-text-strong)',
            'text-base': 'var(--color-text)',
            'text-muted': 'var(--color-text-muted)',
            'neutral-1': 'var(--color-neutral-1)',
            'neutral-2': 'var(--color-neutral-2)',
            'neutral-3': 'var(--color-neutral-3)',
            'neutral-4': 'var(--color-neutral-4)',
            'neutral-5': 'var(--color-neutral-5)',
            success: { DEFAULT: 'var(--color-success)', light: 'var(--color-success-light)' },
            danger: { DEFAULT: 'var(--color-danger)', light: 'var(--color-danger-light)' },
          }
        }
      }
    }
  </script>
</head>
<body>
  <div class="reveal">
    <div class="slides">
      <!-- SLIDES GO HERE -->
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5/dist/reveal.js"></script>
  <script>
    Reveal.initialize({
      width: 1920,
      height: 1080,
      margin: 0,
      hash: true,
      slideNumber: true,
      controls: true,
      progress: true,
    });
    lucide.createIcons();
  </script>
</body>
</html>
```

### Slide structure

Each `<section>` represents one slide. Follow these conventions:

```html
<section>
  <h2>Slide Title</h2>
  <div class="slide-body">
    <!-- Content using Tailwind utility classes -->
  </div>
</section>
```

### Mandatory rules

1. **Color system**: Use ONLY the defined color variables via Tailwind classes: `text-primary`, `bg-primary-light`, `text-text-muted`, `bg-neutral-1`, etc. NEVER use raw hex colors or Tailwind's default color palette (e.g., no `bg-blue-500`).
2. **Icons**: Use Lucide icons via `<i data-lucide="icon-name" class="w-5 h-5"></i>`. NEVER use emoji.
3. **Typography**: Use the existing heading hierarchy (h1-h4) and text sizing from `theme-light.css`.
4. **Layout**: Use CSS Grid (`grid grid-cols-*`) and Flexbox (`flex`) for layouts. Match patterns from the reference file.
5. **Aspect ratio**: Slides are 1920x1080 (16:9). Design content to fill the space appropriately.
6. **Language**: Generate slide content in Japanese unless the user explicitly requests another language.
7. **Images**: Use `.img-placeholder` class for image placeholders with descriptive text inside.
8. **Inline styles**: Only use `style=""` for things Tailwind cannot express (e.g., `grid-template-columns: 6fr 4fr`, `conic-gradient`, specific `height` values for chart bars).
9. **File location**: Save to `slides/` directory. Create the directory if it doesn't exist.
10. **Light mode**: All slides use light mode (white background). No dark backgrounds except for specific design elements like gradient hero slides.
11. **No `!important`**: NEVER use `!important` in CSS. Solve specificity issues by using more specific selectors instead.
12. **Vertical centering**: Slide content below the h2 title is vertically centered via `.slide-body` (which has `flex: 1; justify-content: center`). The h2 stays at the top. Always wrap main content in `<div class="slide-body">`.
13. **Reveal.js config**: Always set `center: false` in `Reveal.initialize()` — vertical centering is handled by CSS, not by Reveal.js.

### Typical slide deck structure

A well-structured presentation usually follows this order:
1. Cover slide (表紙 or ヒーロー表紙)
2. Agenda (アジェンダ) — if 5+ slides
3. Content slides (use section dividers for distinct topics)
4. Summary (まとめ)
5. CTA or Thank You (closing)

## Step 4: Verify

After creating the file, confirm:
- The file is saved in `slides/` directory
- All CSS paths use `../css/` prefix (relative to slides/)
- No emoji characters exist in the output
- No raw Tailwind colors (blue-500, gray-200, etc.) — only the custom color system
- `lucide.createIcons()` is called after `Reveal.initialize()`
