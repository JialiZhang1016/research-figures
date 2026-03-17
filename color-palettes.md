# Color Palettes

## Usage Rules

- Maximum 5 distinct fill colors per figure
- Text on colored fills must pass WCAG AA contrast (4.5:1 minimum)
- Never rely on color alone — always include text labels or patterns
- Arrow/line color: use secondary text color from palette
- Module borders: 15-20% darker than fill color

## Academic Default

The standard palette for papers and general use. Clean, professional, colorblind-friendly.

```
Background:      #FFFFFF
Primary text:    #1A2332
Secondary text:  #4A5568
Muted text:      #8896A6
Accent:          #0066CC
Accent light:    #E8F0FE
Border:          #E2E8F0
Shadow:          rgba(0,0,0,0.06)
```

### Module fills (for differentiating components)

| Name | Fill | Border | Use for |
|------|------|--------|---------|
| Blue | #E8F0FE | #0066CC | Primary modules, encoder |
| Green | #D1FAE5 | #009E73 | Success states, decoder, output |
| Amber | #FEF3C7 | #E69F00 | Warnings, special components |
| Rose | #FEE2E2 | #D55E00 | Error states, loss, negative |
| Purple | #EDE9FE | #7C3AED | Attention, special mechanisms |

### Semantic colors

```
Success/positive: #009E73 (colorblind-friendly green)
Warning/neutral:  #E69F00 (colorblind-friendly amber)
Danger/negative:  #D55E00 (colorblind-friendly vermillion)
Info:             #0066CC (blue)
```

## Light Academic

Linked to academic-slides Light Academic template.

```
Background:      #FAFBFC
Primary text:    #1A2332
Secondary text:  #4A5568
Muted text:      #8896A6
Accent:          #0066CC
Accent light:    #E8F0FE
Border:          #E2E8F0
Shadow:          rgba(0,0,0,0.06)
```

Module fills: same as Academic Default.

## Dark Slate

Linked to academic-slides Dark Slate template. For dark-background slides.

```
Background:      #0F172A
Primary text:    #F8FAFC
Secondary text:  #94A3B8
Muted text:      #64748B
Accent:          #06B6D4
Accent light:    rgba(6, 182, 212, 0.1)
Border:          #334155
Shadow:          rgba(0, 0, 0, 0.3)
```

### Module fills (dark mode)

| Name | Fill | Border | Use for |
|------|------|--------|---------|
| Cyan | rgba(6,182,212,0.15) | #06B6D4 | Primary modules |
| Emerald | rgba(52,211,153,0.15) | #34D399 | Success, output |
| Amber | rgba(251,191,36,0.15) | #FBBF24 | Warnings, special |
| Orange | rgba(251,146,60,0.15) | #FB923C | Error, loss |
| Violet | rgba(167,139,250,0.15) | #A78BFA | Attention, mechanisms |

## Warm Ivory

Linked to academic-slides Warm Ivory template.

```
Background:      #FFF8F0
Primary text:    #2D1B0E
Secondary text:  #5C4033
Muted text:      #9C8578
Accent:          #8B2252
Accent light:    #FDE8EF
Border:          #E8D5C4
Shadow:          rgba(45, 27, 14, 0.06)
```

### Module fills

| Name | Fill | Border | Use for |
|------|------|--------|---------|
| Rose | #FDE8EF | #8B2252 | Primary modules |
| Sage | #E8F0E8 | #2D6A4F | Success, output |
| Cream | #FFF5EB | #B45309 | Warnings, special |
| Blush | #FEE2E2 | #9F1239 | Error, loss |
| Lavender | #F3E8FF | #7C3AED | Attention, mechanisms |

## Swiss Minimal

Linked to academic-slides Swiss Minimal template. Extreme minimalism.

```
Background:      #FFFFFF
Primary text:    #111111
Secondary text:  #555555
Muted text:      #999999
Accent:          #E50000
Accent light:    #F5F5F5
Border:          #E0E0E0
Shadow:          transparent
```

### Module fills

| Name | Fill | Border | Use for |
|------|------|--------|---------|
| Light gray | #F5F5F5 | #E0E0E0 | All modules (minimal) |
| White | #FFFFFF | #111111 | Emphasis modules |

Note: Swiss Minimal uses minimal color. Differentiate modules by border weight, labels, and position rather than fill colors. Use accent red sparingly for emphasis only.

## MST Green

Linked to academic-slides MST Green template. Missouri S&T brand.

```
Background:      #FFFFFF
Primary text:    #1A2B23
Secondary text:  #3D5347
Muted text:      #7A8F83
Accent:          #154734
Accent light:    #E6F0EC
Accent secondary:#BFD730 (gold)
Border:          #D4E0DA
Shadow:          rgba(21, 71, 52, 0.06)
```

### Module fills

| Name | Fill | Border | Use for |
|------|------|--------|---------|
| Green | #E6F0EC | #154734 | Primary modules |
| Gold | #F5F3E0 | #BFD730 | Highlighted/special |
| Sage | #F0F5F3 | #3D5347 | Secondary modules |
| Cream | #FFF8F0 | #BF8B2E | Warnings |
| Rose | #FEE2E2 | #C53030 | Error, loss |

## Mapping Theme Colors to Figure Elements

When generating a figure with a theme-linked palette:

| Figure element | Maps to |
|---------------|---------|
| SVG background | Background |
| Module text | Primary text |
| Arrow labels | Secondary text |
| Annotations | Muted text |
| Primary modules | Accent light fill + Accent border |
| Arrow/line color | Secondary text |
| Emphasis border | Accent |
| Group box border | Border (dashed) |
| Highlight box | Accent light bg + Accent border |
