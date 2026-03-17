# SVG Conventions

## Viewport Sizes

| Use Case | viewBox | Notes |
|----------|---------|-------|
| Slides full-width | `0 0 960 540` | 16:9, for full-screen figures |
| Slides half-width | `0 0 480 360` | For left-text-right-figure layouts |
| Paper single-column | `0 0 480 600` | Portrait, fits one column |
| Paper double-column | `0 0 960 400` | Landscape, spans two columns |

## Fonts

Use Google Fonts family names in `font-family` attributes:
- **Labels/titles**: `Source Serif 4, Georgia, serif` — for figure titles, section labels
- **Body text**: `Inter, -apple-system, sans-serif` — for module names, annotations
- **Values/code**: `JetBrains Mono, monospace` — for dimensions, parameter values, code snippets

When embedded in HTML slides, fonts inherit from the page. For standalone SVG files, include a comment noting required fonts.

## Text Sizing

| Element | Font Size | Weight |
|---------|----------|--------|
| Figure title | 16px | 700 |
| Section label | 14px | 600 |
| Module name | 12px | 500 |
| Annotation | 10px | 400 |
| Dimension/value | 10px | 400 (mono) |
| Caption | 9px | 400 (italic) |

## Spacing

- Figure padding: minimum 20px from viewBox edges
- Module gap: 16px between adjacent modules
- Arrow clearance: 8px from module border to arrow start/end
- Text padding inside modules: 8px horizontal, 6px vertical
- Group padding: 12px inside group borders

## Shapes

### Modules (processing blocks)
- Rectangle with `rx="6"` rounded corners
- Border: 1.5px solid
- Fill: soft color from palette
- Min size: 60x40

### Group boxes (logical grouping)
- Rectangle with `rx="10"` rounded corners
- Border: 2px dashed
- Fill: none or very faint bg
- Label at top-left or top-center

### Data/IO nodes
- Rounded rectangle `rx="12"` or pill shape for inputs/outputs
- Cylinder shape (two ellipses + rect) for databases/storage

### Decision nodes
- Diamond shape for conditionals
- Keep text short (Yes/No on outgoing arrows)

## Arrows and Connections

### Standard arrow marker definition (include in every SVG):
```xml
<defs>
    <!-- Solid arrow -->
    <marker id="arrow" viewBox="0 0 10 10" refX="9" refY="5"
            markerWidth="6" markerHeight="6" orient="auto-start-reverse">
        <path d="M 0 0 L 10 5 L 0 10 z" fill="#4A5568"/>
    </marker>
    <!-- Hollow arrow (for inheritance/interface) -->
    <marker id="arrow-hollow" viewBox="0 0 10 10" refX="9" refY="5"
            markerWidth="6" markerHeight="6" orient="auto-start-reverse">
        <path d="M 0 0 L 10 5 L 0 10 z" fill="white" stroke="#4A5568" stroke-width="1"/>
    </marker>
</defs>
```

### Connection types

| Type | Style | Use |
|------|-------|-----|
| Data flow | Solid line + arrow | Primary connections |
| Optional/conditional | Dashed line + arrow | Skip connections, optional paths |
| Soft update/sync | Dotted line + arrow | Target network update, async sync |
| Bidirectional | Line + arrows on both ends | Agent-Environment interaction |
| Grouping | No arrow, dashed border | Logical grouping |

### Line weights
- Primary connections: 1.5px
- Secondary/annotation: 1px
- Group borders: 2px dashed
- Emphasis connections: 2px solid

## Colors

Colors are defined in `color-palettes.md`. Key rules:
- Arrow color: use palette's secondary text color (not black)
- Module border: slightly darker than fill
- Text on colored fills: ensure WCAG AA contrast (4.5:1 minimum)
- Maximum 5 distinct fill colors per figure

## Shadows (optional)

For slides (depth effect):
```xml
<filter id="shadow" x="-5%" y="-5%" width="110%" height="110%">
    <feDropShadow dx="0" dy="2" stdDeviation="3" flood-opacity="0.08"/>
</filter>
```
Apply with `filter="url(#shadow)"` on module rectangles.

For papers: no shadows (clean print style).

## Annotations

- Dimension labels on arrows: centered on line, small bg rect for readability
  ```xml
  <text x="250" y="148" text-anchor="middle" font-family="JetBrains Mono" font-size="10" fill="#4A5568">
      <tspan style="background:white">[B, 256]</tspan>
  </text>
  ```
- Callout boxes: rounded rect with pointer triangle for explaining specific parts
- Numbering: circled numbers (like outline-list) for step sequences

## Code Structure

- Indent with 4 spaces
- Group related elements with comments: `<!-- Section: Encoder -->`
- Order: defs -> background -> main elements (left-to-right or top-to-bottom) -> arrows -> annotations -> caption
- Each logical group wrapped in `<g>` with descriptive id: `<g id="encoder-stack">`

## Accessibility

- Every interactive/meaningful shape should have a `<title>` child element
- Use `role="img"` and `aria-label` on the root `<svg>` element
- Maintain logical reading order in source (matches visual flow)
- Never rely on color alone — add text labels or patterns

## Embedding Modes

### Inline in HTML slides
```html
<svg viewBox="0 0 960 540" xmlns="http://www.w3.org/2000/svg"
     style="max-width:100%; max-height:min(58vh,520px); border-radius:6px;
            border:1px solid var(--border); box-shadow:0 2px 12px rgba(0,0,0,0.06);
            background:var(--bg-accent);">
    <!-- figure content -->
</svg>
```
- Use CSS variables from slides theme when available
- Set max-height relative to viewport

### Standalone SVG file
```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg viewBox="0 0 960 540" xmlns="http://www.w3.org/2000/svg"
     role="img" aria-label="Figure description">
    <!-- figure content -->
</svg>
```
- Include font comment at top
- Self-contained (no external dependencies)
