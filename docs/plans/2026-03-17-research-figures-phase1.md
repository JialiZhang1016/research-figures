# Research Figures Skill — Phase 1 Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Create a Claude Code skill that generates publication-quality SVG research figures from natural language descriptions or model code.

**Architecture:** A SKILL.md-driven skill with reference SVG templates, color palette definitions, and SVG conventions. AI reads these files at invocation time and generates figures following the defined standards and interactive workflow.

**Tech Stack:** SVG, Markdown, Claude Code skill system

---

### Task 1: Initialize GitHub repo

**Files:**
- Create: `README.md`
- Create: `LICENSE`

**Step 1: Create repo on GitHub**

Run: `cd ~/Documents/github/research-figures && git init`

**Step 2: Create LICENSE (MIT)**

Copy MIT license with author "Jiali Zhang".

**Step 3: Create minimal README.md**

```markdown
# Research Figures

A Claude Code skill for generating publication-quality SVG research figures.

Fork-free, zero-dependency. Describe what you need → get a vector diagram.

## Status

Phase 1 (SVG figures) — in development.

## License

MIT
```

**Step 4: Initial commit**

```bash
git add README.md LICENSE
git commit -m "chore: init project"
```

**Step 5: Create remote and push**

```bash
gh repo create JialiZhang1016/research-figures --public --source=. --push
```

---

### Task 2: SVG conventions file

**Files:**
- Create: `svg-conventions.md`

Defines the code standards every generated SVG must follow. This is the "style guide" that AI references when generating.

**Content to include:**

- **Viewport**: default `viewBox` sizes per use case (slides full-width: 960×540, slides half: 480×360, paper single-column: 480×600, paper double-column: 960×400)
- **Fonts**: use Google Fonts family names in `font-family` attributes. Default: Inter for body, Source Serif 4 for labels, JetBrains Mono for code/values
- **Spacing**: minimum padding 20px, module gap 16px, arrow clearance 8px
- **Arrows**: standard `<marker>` definitions for solid, dashed, bidirectional arrows
- **Corners**: `rx="6"` for modules, `rx="10"` for group boxes
- **Text sizing**: title 16px, module label 12px, annotation 10px, caption 9px
- **Line weights**: module border 1.5px, arrows 1.5px, group border 2px dashed, subtle connections 1px
- **Shadow**: optional `filter` for depth, default off for paper, on for slides
- **Accessibility**: every shape needs descriptive text, logical reading order
- **Code structure**: indent with 4 spaces, group related elements with comments `<!-- Section Name -->`

**Step 1: Write `svg-conventions.md`**

**Step 2: Commit**

```bash
git add svg-conventions.md
git commit -m "docs: add SVG code conventions"
```

---

### Task 3: Color palettes file

**Files:**
- Create: `color-palettes.md`

Defines all available color schemes.

**Content to include:**

**Academic Default palette:**
- bg: #FFFFFF
- primary text: #1A2332
- secondary text: #4A5568
- muted: #8896A6
- accent: #0066CC
- accent-light: #E8F0FE
- success: #009E73
- warning: #E69F00
- danger: #D55E00
- module fills: 4-5 distinct soft colors for differentiating components
- border: #E2E8F0

**5 theme-linked palettes** (reference academic-slides templates):
- Light Academic, Dark Slate, Warm Ivory, Swiss Minimal, MST Green
- For each: extract bg, text, accent, module fill colors from their CSS `:root` variables
- Include guidance on how to map theme colors to figure elements

**Usage rules:**
- Maximum 5 distinct fill colors per figure
- High contrast: text on fill must pass WCAG AA
- Color-blind friendly: never rely on color alone, use patterns/labels too

**Step 1: Write `color-palettes.md`**

**Step 2: Commit**

```bash
git add color-palettes.md
git commit -m "docs: add color palette definitions"
```

---

### Task 4: Architecture templates (2 SVGs)

**Files:**
- Create: `templates/arch-encoder-decoder.svg`
- Create: `templates/arch-dual-network.svg`

**Template 1: Encoder-Decoder**
- Classic left-to-right: Input → Encoder (stacked layers) → Latent → Decoder (stacked layers) → Output
- Show skip connections with curved dashed lines
- Dimension annotations on arrows

**Template 2: Dual Network**
- Shared bottom module → fork into two parallel branches → separate outputs
- Typical for Actor-Critic, Siamese networks
- Show parameter sharing with grouped dashed border

Both templates use `academic-default` palette, `viewBox="0 0 960 540"` (slides full-width).

**Step 1: Create `templates/` directory and write both SVGs**

**Step 2: Open in browser to verify they render correctly**

**Step 3: Commit**

```bash
git add templates/
git commit -m "feat: add architecture reference templates"
```

---

### Task 5: Pipeline templates (2 SVGs)

**Files:**
- Create: `templates/pipe-training-loop.svg`
- Create: `templates/pipe-data-pipeline.svg`

**Template 1: Training Loop**
- Circular flow: Sample Batch → Forward Pass → Compute Loss → Backward Pass → Update Weights → (loop arrow back)
- Epoch/step counter annotation
- Loss value callout box

**Template 2: Data Pipeline**
- Linear left-to-right: Raw Data → Preprocess → Feature Extract → Train/Val Split → Model → Evaluate
- Branching at split point
- Data shape annotations on arrows (e.g., "[B, 128]")

**Step 1: Write both SVGs**

**Step 2: Verify in browser**

**Step 3: Commit**

```bash
git add templates/
git commit -m "feat: add pipeline reference templates"
```

---

### Task 6: Comparison and RL templates (4 SVGs)

**Files:**
- Create: `templates/comp-side-by-side.svg`
- Create: `templates/comp-before-after.svg`
- Create: `templates/rl-agent-env.svg`
- Create: `templates/rl-mdp.svg`

**comp-side-by-side**: Two columns with matching components, visual diff highlights (like RNN vs Transformer example)

**comp-before-after**: Left "before" (grayed/red) → arrow → right "after" (colored/green), showing improvement

**rl-agent-env**: Classic RL loop — Agent ↔ Environment with State, Action, Reward arrows, dashed line separating agent/env

**rl-mdp**: State transition diagram — circles for states, arrows for actions, rewards on edges, terminal state highlighted

**Step 1: Write all 4 SVGs**

**Step 2: Verify in browser**

**Step 3: Commit**

```bash
git add templates/
git commit -m "feat: add comparison and RL reference templates"
```

---

### Task 7: Math and System templates (4 SVGs)

**Files:**
- Create: `templates/math-optimization.svg`
- Create: `templates/math-distribution.svg`
- Create: `templates/sys-multi-component.svg`
- Create: `templates/sys-deploy.svg`

**math-optimization**: 2D loss landscape contour with gradient descent path, annotated minimum point

**math-distribution**: Overlapping bell curves or bar distributions, labeled with μ and σ

**sys-multi-component**: Multiple service boxes with API arrows, database cylinder, message queue

**sys-deploy**: Client → Load Balancer → Server instances → Database, with cloud boundary box

**Step 1: Write all 4 SVGs**

**Step 2: Verify in browser**

**Step 3: Commit**

```bash
git add templates/
git commit -m "feat: add math and system reference templates"
```

---

### Task 8: SKILL.md — the main skill file

**Files:**
- Create: `SKILL.md`

This is the core file that AI reads when the skill is invoked. It defines the full interactive workflow.

**Content structure:**

```markdown
---
name: research-figures
description: Generate publication-quality SVG research figures from descriptions or code. Use when user asks to draw/create diagrams, architecture figures, flowcharts, or any visual for papers/slides.
---

# Research Figures

## Trigger
- User asks to draw, create, or generate a research figure/diagram
- User provides model code and asks for an architecture visualization
- User mentions needing figures for a paper or presentation

## Phase 1: Understand the Request (interactive)
[Full Step 1 workflow: receive → identify type → extract components → confirm connections → confirm emphasis → summarize]

## Phase 2: Confirm Style (interactive)
[Full Step 2 workflow: color scheme → output format → layout → size]

## Phase 3: Generate
[SVG generation rules, reference conventions and templates]

## Phase 4: Iterate
[Preview → feedback → modify loop]

## Code Analysis Mode
[How to parse PyTorch nn.Module, TensorFlow, JAX code into component lists]

## Reference Files
- Read svg-conventions.md for code standards
- Read color-palettes.md for color schemes
- Browse templates/ for layout inspiration
```

**Step 1: Write SKILL.md with complete workflow**

**Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: add main SKILL.md with interactive workflow"
```

---

### Task 9: Update README and finalize

**Files:**
- Modify: `README.md`

**Step 1: Rewrite README with full documentation**

Include:
- Project description and credits
- Quick Start (clone to `~/.claude/skills/research-figures/`)
- Supported figure types with template previews
- Color schemes
- Usage examples
- Phase 2 roadmap mention

**Step 2: Commit and push**

```bash
git add README.md
git commit -m "docs: complete README with usage guide"
git push origin main
```

---

### Task 10: Install as Claude Code skill

**Step 1: Clone to skills directory**

```bash
git clone https://github.com/JialiZhang1016/research-figures.git ~/.claude/skills/research-figures
```

**Step 2: Verify skill appears in available skills list**

Start a new Claude Code session and check that `research-figures` shows up.

---

## Task Dependency Order

```
Task 1 (init repo)
  → Task 2 (SVG conventions)
  → Task 3 (color palettes)
  → Tasks 4, 5, 6, 7 (templates — can run in parallel)
  → Task 8 (SKILL.md — needs conventions + palettes + templates done)
  → Task 9 (README)
  → Task 10 (install)
```
