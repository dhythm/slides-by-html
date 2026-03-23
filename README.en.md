English | [日本語](README.md)

# slides-by-html

A repository that generates professional presentation slides simply by prompting a coding agent (Claude Code, Codex, etc.).

It comes with a rich set of layout patterns and a unified design system that agents reference when creating slides.

![](assets/thumbnail.png)

### Sample Slide

![Sample slide](assets/sample-slide.gif)

## Features

- Generate slides just by instructing a coding agent
- Rich layout patterns (data visualization, comparison, timeline, org chart, etc.)
- Unified color system and typography
- Custom theme support (corporate colors, background templates)
- Browser-based presentations with Reveal.js
- PDF export via DeckTape

## Tech Stack

| Category     | Tool                                                |
| ------------ | --------------------------------------------------- |
| Presentation | [Reveal.js](https://revealjs.com/) v5               |
| Styling      | [Tailwind CSS](https://tailwindcss.com/) (CDN)      |
| Icons        | [Lucide](https://lucide.dev/) (CDN)                 |
| PDF Export   | [DeckTape](https://github.com/astefanutti/decktape) |

## Directory Structure

```
.
├── css/
│   ├── theme-light.css          # Color system & theme definitions
│   └── custom/                  # Custom themes (corporate colors, etc.)
│       └── your-company.css
├── images/
│   └── templates/               # Background template images
├── layouts/
│   └── layout-patterns.html     # 68 layout patterns
├── slides/                      # Generated slides
├── .claude/
│   └── skills/
│       └── create-slide/        # Slide generation skill
│           └── SKILL.md
├── CLAUDE.md
└── AGENTS.md
```

## Usage

### Creating Slides

Open this repository in Claude Code and use the `/create-slide` command or give instructions in natural language.

#### Prompt Examples

**Simple instruction:**

```
/create-slide Internal proposal for DX initiatives
```

**Detailed instruction:**

```
Create an investor pitch deck for a new SaaS product.
Please use the following structure:

1. Cover (Product name: DataFlow)
2. Problem statement — Enterprise data silo issues
3. Solution overview — 3-column layout for key features
4. Market size — TAM/SAM/SOM breakdown
5. Competitive analysis — Harvey ball feature comparison
6. Business model — 3-tier pricing plan comparison
7. KPI dashboard — 4 key metrics
8. Roadmap — 3-phase development plan
9. Team introduction — 4 executives
10. CTA — Contact & next steps
```

**With theme specification:**

```
Create a Q3 sales report slide deck.
I'd like bar charts for quarterly revenue trends,
a funnel for the sales pipeline, and before/after
comparisons for operational improvements.
```

**Using with other agents (Codex, etc.):**

```
Refer to layouts/layout-patterns.html and css/theme-light.css
in this repository to create an internal report slide on AI adoption
results as slides/ai-report.html. Use Reveal.js + Tailwind CSS +
Lucide icons, and do not use emoji.
```

### Browser Preview

Generated slides can be opened directly in a browser.

```bash
open slides/my-presentation.html
```

### PDF Export

#### Ask the coding agent

After creating slides, you can request PDF export directly.

```
Convert slides/my-presentation.html to PDF
```

```
Export the created slides to PDF using npx decktape.
Use 1920x1080 size and save to output/my-presentation.pdf.
```

The agent will automatically handle everything from starting a local server to running DeckTape.

#### npx (for developers)

You can run it directly with npx in environments with Node.js installed.

```bash
# Start a local server (in a separate terminal)
npx serve .

# Export to PDF
npx decktape reveal http://localhost:3000/slides/my-presentation.html output.pdf
```

**With options:**

```bash
# Specify slide size and page transition interval
npx decktape reveal \
  --size 1920x1080 \
  --pause 1000 \
  http://localhost:3000/slides/my-presentation.html \
  output.pdf
```

## Color System

Color palette defined in `css/theme-light.css`:

| Purpose        | Variable               | Tailwind Class                   |
| -------------- | ---------------------- | -------------------------------- |
| Primary        | `--color-primary`      | `text-primary`, `bg-primary`     |
| Secondary      | `--color-secondary`    | `text-secondary`, `bg-secondary` |
| Accent         | `--color-accent`       | `text-accent`, `bg-accent`       |
| Strong text    | `--color-text-strong`  | `text-text-strong`               |
| Body text      | `--color-text`         | `text-text-base`                 |
| Muted text     | `--color-text-muted`   | `text-text-muted`                |
| Background     | `--color-neutral-1~5`  | `bg-neutral-1` ~ `bg-neutral-5`  |

## Custom Themes

Customize colors and background templates to match your corporate branding.

### Setup

1. Copy and rename `css/custom/example-corporate.css`
2. Edit color variables (primary, secondary, accent)
3. Place background images in `images/templates/` (1920x1080px, PNG recommended)
4. Link the custom CSS in your slide HTML

```html
<link rel="stylesheet" href="../css/theme-light.css">
<link rel="stylesheet" href="../css/custom/your-company.css">
```

> **Note**: Files starting with `example-` are samples included in the repository.
> Use different names for your own themes and images (e.g., `my-company.css`).

### Background Template Patterns

| Slide Type | Specification | Purpose |
|------------|---------------|---------|
| Cover slide | `<section data-state="cover">` | Background for title slides |
| Normal slide | `<section>` | Background for content slides |
| Gradient | `<section data-state="hero-gradient">` | No background image, gradient only |

### Prompt Example

```
Create a company introduction slide deck using
css/custom/example-corporate.css as the theme.
```

## Layout Patterns

Patterns included in `layouts/layout-patterns.html`:

| Category               | Key Patterns                                          |
| ---------------------- | ----------------------------------------------------- |
| Structure & Opening    | Cover, hero cover, agenda, section divider             |
| Introduction           | Company intro, product/service intro                   |
| Basic Text Layouts     | 2-column, 3-column, heading + subtitle, quote, FAQ     |
| Comparison & Analysis  | Side-by-side, SWOT, Venn diagram, problem-cause-action |
| Flow & Timeline        | Steps, chevron, timeline, roadmap                      |
| Data & Analytics       | KPI, bar chart, line chart, donut chart, Gantt chart   |
| Image & Product        | Full-screen image, screenshot + annotations            |
| People & Organization  | Team intro, org chart, testimonials                    |
| Closing & Supplemental | Summary, CTA, Thank You, references                   |
| Decorative Components  | Panel design, cards, tags, badges                      |

## License

[MIT](LICENSE)
