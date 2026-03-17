---
name: research-figures
description: Generate publication-quality SVG research figures from natural language descriptions or model code. Use when user asks to draw, create, or visualize diagrams, architectures, flowcharts, comparisons, RL loops, math concepts, or system diagrams for papers or presentations.
---

# Research Figures

Generate zero-dependency, publication-quality SVG research figures. Supports both paper illustrations and slide-embedded diagrams.

## Trigger

Activate when the user:
- Asks to draw, create, or generate a research figure or diagram
- Provides model code and asks for an architecture visualization
- Mentions needing figures for a paper or presentation
- Says "画一个..." / "draw a..." / "visualize..." / "create a diagram of..."

---

## Phase 1: Understand the Request

### Step 1a: Receive Input

Accept one of two input types:
- **Natural language description** — e.g., "Draw an Actor-Critic architecture with shared encoder"
- **Model code** — e.g., PyTorch `nn.Module`, TensorFlow model, JAX code

### Step 1b: Identify Figure Type

Ask the user to confirm the figure type:

> "What type of figure is this?"
> - **Architecture** — Neural network structure, module connections (encoder-decoder, dual-network)
> - **Pipeline** — Training loop, data processing flow, method steps
> - **Comparison** — Side-by-side A vs B, before/after improvement
> - **RL Diagram** — Agent-environment loop, MDP state transitions
> - **Math Concept** — Loss landscape, probability distributions, geometric intuition
> - **System** — Multi-component architecture, deployment topology

### Step 1c: Extract Components

Parse the input and list all identified modules/components:

> "I identified these components from your description/code:
> 1. State Encoder (Linear: 128 → 256, ReLU)
> 2. Actor Network (Linear: 256 → 128 → action_dim)
> 3. Critic Network (Linear: 256 → 128 → 1)
> 4. Replay Buffer
> 5. Target Network
>
> Any missing or extra?"

**If input is code:** Parse the model definition to extract:
- Layer types and dimensions (Linear, Conv2d, LSTM, etc.)
- Forward pass data flow (which module feeds into which)
- Input/output shapes
- Named sub-modules and their roles

### Step 1d: Confirm Connections

Present the topology as a text-based graph:

> "Connections between components:
> - State → State Encoder
> - State Encoder → Actor Network → Action
> - State Encoder → Critic Network → Q Value
> - (State, Action, Reward, Next State) → Replay Buffer
> - Critic Network ··soft update··> Target Network
>
> Are the connections and arrow directions correct?"

### Step 1e: Confirm Emphasis

Ask what to highlight:

> "Any parts to emphasize?
> - Highlight a module (colored border/fill)
> - Special arrow style (dashed, bold, different color)
> - Group modules together (dashed border box with label)
> - Add annotations or callout boxes
> - Number steps in a sequence"

### Step 1f: Final Summary

Consolidate everything and get confirmation:

> "Final plan:
> - **Type**: Architecture
> - **Components**: 5 (as listed above)
> - **Connections**: as confirmed above
> - **Emphasis**: Actor/Critic fork highlighted, Target Network dashed connection
> - **Groups**: Encoder+Actor+Critic grouped as 'Online Network'
>
> Confirmed? I'll move to style selection."

---

## Phase 2: Confirm Style

### Step 2a: Color Scheme

> "Which color scheme?"
> - **Academic Default** — White bg, blue accent, clean for papers (recommended for publications)
> - **Light Academic** — Match academic-slides Light Academic theme
> - **Dark Slate** — Match academic-slides Dark Slate theme (dark bg, teal glow)
> - **Warm Ivory** — Match academic-slides Warm Ivory theme (cream bg, burgundy)
> - **Swiss Minimal** — Match academic-slides Swiss Minimal theme (B&W + red)
> - **MST Green** — Match academic-slides MST Green theme
> - **Custom** — Specify your own colors

Read `color-palettes.md` for the full palette definitions.

### Step 2b: Output Format

> "Where will this figure be used?"
> - **Slides** — Inline SVG, embedded directly in HTML presentation
> - **Paper** — Standalone `.svg` file for LaTeX/Word
> - **Both** — Generate both formats

### Step 2c: Layout

> "Layout preference?"
> - **Landscape** — Horizontal, suits slides and wide figures
> - **Portrait** — Vertical, suits paper single-column
> - **Auto** — I'll choose based on content

### Step 2d: Size

> "Figure size?"
> - **Full width** — Slides: 960×540, Paper: double-column width
> - **Half width** — Slides: 480×360 (for text+figure layout), Paper: single-column
> - **Custom** — Specify dimensions

After all 4 choices, proceed to generation.

---

## Phase 3: Generate

### Before generating, read these reference files:
- `svg-conventions.md` — Code standards, fonts, spacing, arrow definitions
- `color-palettes.md` — Color values for chosen scheme
- Browse `templates/` — Find the closest matching template for layout inspiration

### SVG Generation Rules

1. **Self-contained** — No external dependencies. All styles inline.
2. **Proper viewBox** — Use dimensions from Step 2d
3. **Fonts** — Use Google Font family names: Inter for body, Source Serif 4 for titles, JetBrains Mono for values
4. **Rounded corners** — `rx="6"` for modules, `rx="10"` for groups
5. **Arrows** — Include `<defs>` with arrow markers. Use secondary text color, not black.
6. **Colors** — Apply module fills from chosen palette. Max 5 distinct fills.
7. **Accessibility** — `role="img"`, `aria-label` on root SVG. Meaningful `<title>` on shapes.
8. **Code structure** — Indent 4 spaces, `<!-- Section -->` comments, logical `<g>` groups
9. **Contrast** — Text on fills must pass WCAG AA (4.5:1)
10. **No scrolling** — Everything must fit within the viewBox

### Output based on format choice:

**For slides (inline SVG):**
```html
<svg viewBox="0 0 960 540" xmlns="http://www.w3.org/2000/svg"
     style="max-width:100%; max-height:min(58vh,520px); border-radius:6px;
            border:1px solid var(--border); box-shadow:0 2px 12px rgba(0,0,0,0.06);
            background:var(--bg-accent);">
    <!-- figure content -->
</svg>
```

**For paper (standalone file):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg viewBox="0 0 960 540" xmlns="http://www.w3.org/2000/svg"
     role="img" aria-label="Figure description">
    <!-- Requires: Inter, Source Serif 4, JetBrains Mono from Google Fonts -->
    <!-- figure content -->
</svg>
```

---

## Phase 4: Iterate

1. **Preview** — Save the SVG and open in browser with `open filename.svg`
2. **Ask for feedback** — "How does this look? Anything to adjust?"
3. **Common adjustments:**
   - Move/resize modules
   - Change arrow routing
   - Add/remove labels
   - Adjust spacing
   - Change colors
4. **Apply changes** and preview again
5. **Repeat** until the user is satisfied

---

## Code Analysis Mode

When the user provides model code instead of a description:

### PyTorch
```python
class MyModel(nn.Module):
    def __init__(self):
        self.encoder = nn.Sequential(...)
        self.head = nn.Linear(...)
```

Parse:
- `__init__`: Extract all `nn.*` layers and sub-modules
- `forward`: Trace data flow, identify skip connections, branches, concatenations
- Named children: Use variable names as module labels
- Dimensions: Extract from layer parameters (in_features, out_features, etc.)

### TensorFlow/Keras
- Parse `tf.keras.Sequential` or functional API
- Extract layer types, shapes from `model.summary()` style info

### JAX/Flax
- Parse `nn.Module` subclasses and `__call__` method

After parsing, proceed to Step 1c (present extracted components for confirmation).

---

## Reference Templates

Available in `templates/` directory for layout inspiration:

| Template | Type | Description |
|----------|------|-------------|
| `arch-encoder-decoder.svg` | Architecture | Encoder → Latent → Decoder with skip connections |
| `arch-dual-network.svg` | Architecture | Shared encoder → Actor/Critic branches |
| `pipe-training-loop.svg` | Pipeline | Circular 5-step training flow |
| `pipe-data-pipeline.svg` | Pipeline | Linear data processing with train/val split |
| `comp-side-by-side.svg` | Comparison | Two approaches with pros/cons |
| `comp-before-after.svg` | Comparison | Baseline → improvement with metrics |
| `rl-agent-env.svg` | RL | Agent-Environment interaction loop |
| `rl-mdp.svg` | RL | State transition diagram with rewards |
| `math-optimization.svg` | Math | Gradient descent on contour plot |
| `math-distribution.svg` | Math | Overlapping class distributions |
| `sys-multi-component.svg` | System | Three-layer microservice architecture |
| `sys-deploy.svg` | System | Cloud deployment topology |

---

## Supporting Files

| File | Purpose | When to Read |
|------|---------|-------------|
| `svg-conventions.md` | SVG code standards, fonts, spacing, arrows | Phase 3 (before generating) |
| `color-palettes.md` | All color schemes with hex values | Phase 2 (style selection) and Phase 3 |
| `templates/*.svg` | Reference layouts for each figure type | Phase 3 (layout inspiration) |
