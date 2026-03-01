# CLAUDE.md — Levara Sauna Site

## Project Overview

This is a **static HTML documentation site** for the Levara Pool-View Dual Sauna Suite — a luxury 3-room sauna project (two saunas + vestibule/cool-down area with pool views). The site serves as both a public-facing landing page and a comprehensive technical reference for contractors, designers, and stakeholders.

**Key facts:**
- Suite dimensions: W 2.95m × L 4.62m × H 3.50m (envelope 5.7m × 4.0m)
- Total capacity: 10 people (8 comfortable)
- All costs in Thai Baht (฿); metric units throughout
- Bilingual: English + Thai (full localization)

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | HTML5 (semantic) |
| Styling | Inline CSS in `<style>` tags — CSS Custom Properties, Grid, Flexbox |
| JavaScript | None (purely static pages) |
| Fonts | Google Fonts API: Cormorant Garamond, Outfit, Noto Sans Thai |
| Build tools | None — no bundler, preprocessor, or task runner |
| Documentation | Markdown files |
| Drawings | SVG (vector), PDF, JPG/PNG (raster) |

**No package.json, no npm dependencies, no build step.** Files are served as-is by any static web server.

## Repository Structure

```
levara-sauna-site/
├── CLAUDE.md                          # This file
├── README.md                          # Project readme
│
├── index.html                         # English landing page (main site)
├── index-th.html                      # Thai landing page
├── docs.html                          # English documentation portal
├── docs-th.html                       # Thai documentation portal
│
├── pool-view-dual-sauna-suite-design-specs.md   # Master design specification
├── acceptance-criteria.md             # Testable performance targets
├── deliverables-checklist.md          # Contractor deliverables tracker
│
├── calculations/                      # Engineering calculations
│   ├── heater-sizing.md               # Thermal load & heater kW sizing
│   └── glass-cost-comparison.md       # Glazing cost analysis (Thailand market)
│
├── drawings/                          # Technical drawings
│   ├── floor-plan-draft.svg           # SVG floor plan
│   ├── interior-elevation-draft.svg   # SVG interior elevation
│   ├── isometric-concept.svg          # SVG isometric view
│   ├── section-AA-draft.svg           # SVG cross-section
│   ├── sauna v4.pdf                   # Room Planner v4 detailed floor plan
│   ├── Room - Full report.pdf         # Full room specifications report
│   └── steam-room.pdf                 # Steam room design
│
├── floor-plans/                       # Images & renders
│   ├── sauna3.jpg                     # Elevation render
│   ├── sauna4.jpg                     # Top-down view
│   ├── sauna5.jpg                     # 3D floor plan render (current)
│   ├── steam-room-1.jpg              # Steam room render
│   ├── exhaust.png                    # Ventilation placement diagram
│   └── IMG_0267.jpg                   # Figma render
│
├── schedules/                         # Construction schedules (Markdown)
│   ├── room-schedule.md               # Room dimensions & areas
│   ├── material-schedule.md           # Materials with quantities
│   ├── equipment-schedule.md          # Heaters, controls, lighting, ventilation
│   ├── finish-schedule.md             # Surface finishes by room
│   └── door-schedule.md              # Door specifications
│
└── specifications/                    # Detailed technical specs (Markdown + PDF)
    ├── hinoki-wood-spec.md            # Japanese cypress wood selection
    ├── wall-assembly-spec.md          # Layer-by-layer wall construction
    ├── ventilation-spec.md            # Air supply/exhaust requirements
    ├── electrical-spec.md             # Power, controls, safety systems
    ├── door-spec.md                   # Sauna door construction & hardware
    ├── floor-spec.md                  # Floor assembly and duckboards
    ├── window-spec.md                 # Pool-view glazing specification
    ├── sauna-materials-spec.md        # Materials with supplier links (EN)
    ├── sauna-materials-spec.pdf       # Materials spec PDF (EN)
    ├── sauna-materials-spec-th.md     # Materials with Thai suppliers
    ├── sauna-materials-spec-th-v2.md  # Updated Thai materials spec v2
    └── sauna-materials-spec-th-v2.pdf # Thai materials spec v2 PDF
```

## HTML Pages

### Architecture

All four HTML pages follow the same pattern:
- Single-file HTML5 with all CSS inlined in a `<style>` block (1500+ lines)
- No external stylesheets or JavaScript files
- CSS Custom Properties for consistent theming
- Responsive design with a mobile breakpoint at `max-width: 768px`
- Images reference local files in `floor-plans/` and `drawings/`
- Images use `onerror="this.style.display='none'"` as a fallback

### CSS Design System

```css
/* Color palette (defined in :root) */
--bg-dark: #1a1512;         /* Primary dark background */
--bg-warm: #2d2420;         /* Warm secondary background */
--accent-copper: #c17f59;   /* Copper accent */
--accent-gold: #d4a574;     /* Gold accent */
--text-light: #f5f0eb;      /* Light text */
--text-muted: #a89a8c;      /* Muted text */
--hinoki: #deb887;          /* Hinoki wood tone */
--hinoki-dark: #c9a86c;     /* Dark hinoki */
```

### Typography

- **Headings:** `Cormorant Garamond` (serif) — weights 300, 400, 500, 600
- **Body:** `Outfit` (sans-serif) — weights 300, 400, 500
- **Thai text:** `Noto Sans Thai` — weights 300, 400, 500 (line-height: 1.8)

### Language Toggle

English and Thai pages are separate HTML files linked via a language toggle button in the navigation. The toggle links between:
- `index.html` ↔ `index-th.html`
- `docs.html` ↔ `docs-th.html`

## Content Conventions

### Units & Formatting

- **Dimensions:** Metric (meters, cm, mm) — e.g., "2.62 × 3.00 × 3.00m"
- **Currency:** Thai Baht (฿) — e.g., "฿94,099"
- **Temperature:** Celsius — e.g., "85°C"
- **Power:** kW — e.g., "8-10 kW"
- **Area:** m² — e.g., "15.81 m²"
- **Volume:** m³ — e.g., "9.87 m³"

### Markdown Files

- Use hierarchical headings (H1 → H3)
- Tables for structured data (dimensions, costs, comparisons)
- Cross-reference other documents via relative links
- Version tracking in filenames (v2, v4 suffixes)

## Development Workflow

### Serving Locally

No build step required. Open `index.html` directly in a browser, or use any static file server:

```bash
# Python
python3 -m http.server 8000

# Node.js (npx)
npx serve .
```

### Making Changes

1. **HTML pages:** Edit inline CSS/HTML directly in the HTML files. Keep styling consistent across all four pages (index.html, index-th.html, docs.html, docs-th.html).
2. **Specifications/schedules:** Edit the relevant Markdown file. If the change affects docs.html/docs-th.html links, update those too.
3. **Images/drawings:** Add to `floor-plans/` or `drawings/` and reference from HTML.
4. **Thai content:** Any English content change should have a corresponding Thai update in the `-th` variant files.

### Key Editing Rules

- When modifying CSS variables or the design system, update **all four HTML files** to keep them in sync.
- When adding new specification or schedule documents, also add a link card in `docs.html` and `docs-th.html`.
- When updating room dimensions, costs, or specifications, check for consistency across: the master spec (`pool-view-dual-sauna-suite-design-specs.md`), the relevant schedule, the relevant specification file, and the HTML pages.
- SVG drawings in `drawings/` are lightweight vector files; prefer SVG for new technical drawings.
- PDFs are stored alongside their Markdown source when both exist (e.g., `sauna-materials-spec.md` + `sauna-materials-spec.pdf`).

## Important Design Decisions

- **Window placement:** The pool-view window is in the vestibule (not inside hot saunas) to avoid heat loss and condensation.
- **Dropped ceilings:** Sauna ceilings are dropped to 2.2–2.3m (from 3.5m room height) for heater efficiency.
- **Doors:** All 3 doors swing outward (safety requirement). No locks — magnetic catches only.
- **Hinoki wood:** Japanese cypress (Chamaecyparis obtusa) selected for antimicrobial properties. No varnish or sealant inside sauna zones.
- **Heaters:** Solzaima Radiator units (฿94,099 each, 3 total). Electric sauna targets 85°C; IR sauna targets 55°C.
- **Floor-level glazing:** 10 m² total, laminated insulated glass, walk-on rated (2.5 kN/m²). Air-filled IGU recommended over argon for tropical climate.

## Git Conventions

- Commit messages are descriptive, starting with an action verb: "Add", "Update", "Fix"
- The default branch on the remote is `main`
- No CI/CD pipeline or automated testing configured
- No `.gitignore` — binary assets (PDFs, images) are tracked directly in the repository
