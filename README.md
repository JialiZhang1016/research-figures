# Research Figures

A Claude Code skill for generating publication-quality SVG research figures from natural language descriptions or model code.

Zero-dependency. Describe what you need → get a vector diagram for your paper or slides.

## Quick Start

```bash
# Install as Claude Code skill
git clone https://github.com/JialiZhang1016/research-figures.git ~/.claude/skills/research-figures
```

Then in Claude Code, describe what you need:
- "Draw an Actor-Critic architecture with shared encoder"
- "Visualize this PyTorch model" (paste code)
- "Create a before/after comparison diagram"

## Supported Figure Types

| Type | Templates | Use for |
|------|-----------|---------|
| **Architecture** | encoder-decoder, dual-network | Neural network structures, module connections |
| **Pipeline** | training-loop, data-pipeline | Training flows, data processing steps |
| **Comparison** | side-by-side, before-after | A vs B, method improvements |
| **RL Diagram** | agent-env, mdp | Agent-environment loops, state transitions |
| **Math Concept** | optimization, distribution | Loss landscapes, probability distributions |
| **System** | multi-component, deploy | Microservices, deployment topologies |

## Color Schemes

- **Academic Default** — Clean white bg, blue accent (for papers)
- **Light Academic / Dark Slate / Warm Ivory / Swiss Minimal / MST Green** — Match [academic-slides](https://github.com/JialiZhang1016/academic-slides) themes

## Output Formats

- **Inline SVG** — Embed directly in HTML slides
- **Standalone .svg** — For LaTeX, Word, or any document
- **Both** — Generate both formats simultaneously

## Input Modes

- **Natural language** — Describe the figure you want
- **Code analysis** — Provide PyTorch/TensorFlow/JAX model code, auto-extract architecture

## Project Structure

```
research-figures/
├── SKILL.md              # Main skill file (interactive workflow)
├── svg-conventions.md    # SVG code standards
├── color-palettes.md     # Color schemes (academic + theme-linked)
├── templates/            # 12 reference SVG templates
│   ├── arch-*.svg        # Architecture templates
│   ├── pipe-*.svg        # Pipeline templates
│   ├── comp-*.svg        # Comparison templates
│   ├── rl-*.svg          # RL diagram templates
│   ├── math-*.svg        # Math concept templates
│   └── sys-*.svg         # System diagram templates
└── README.md
```

## Roadmap

- [x] **Phase 1** — SVG figures (architecture, pipeline, comparison, RL, math, system)
- [ ] **Phase 2** — matplotlib integration (training curves, bar charts, ablation plots)

## License

MIT
