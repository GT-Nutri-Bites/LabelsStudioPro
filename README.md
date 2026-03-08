# 🏷 Label Studio Pro — Product Label Designer

[![Status](https://img.shields.io/badge/status-active-brightgreen)](#)
[![License](https://img.shields.io/badge/license-MIT-blue)](#)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](#)

A browser-based, single-page product label designer for creating, customising, and printing professional product labels on A4 self-adhesive sheets. No installation, no dependencies — just open and design.

![Label Studio Pro Screenshot](https://github.com/user-attachments/assets/3b5dcda4-3063-4fc0-8787-a3e04f376657)

---

## Table of Contents

- [Overview](#overview)
- [Getting Started](#getting-started)
- [Features & Functions](#features--functions)
  - [1. Brand Identity Configuration](#1-brand-identity-configuration)
  - [2. Product Information Entry](#2-product-information-entry)
  - [3. Dates & Traceability](#3-dates--traceability)
  - [4. Company Details](#4-company-details)
  - [5. Cutting Guidelines](#5-cutting-guidelines)
  - [6. Sheet Settings](#6-sheet-settings)
  - [7. Live Label Preview](#7-live-label-preview)
  - [8. A4 Sheet Preview](#8-a4-sheet-preview)
  - [9. Zoom Controls](#9-zoom-controls)
  - [10. Print Summary Modal](#10-print-summary-modal)
  - [11. Print Functionality](#11-print-functionality)
  - [12. Reset Form](#12-reset-form)
  - [13. Toast Notifications](#13-toast-notifications)
  - [14. Statistics Bar](#14-statistics-bar)
  - [15. Keyboard & Scroll Interactions](#15-keyboard--scroll-interactions)
- [JavaScript Functions Reference](#javascript-functions-reference)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Deployment](#deployment)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)

---

## Overview

**Label Studio Pro** is a fully client-side web application for designing product labels sized at **1.5″ × 1.0″** (38.1 mm × 25.4 mm), arranged on **A4 sheets** for printing. It provides a live preview, multiple colour themes, configurable cutting guides, and a print-optimised layout — all within a single HTML file.

**Key highlights:**

- Zero dependencies — works offline once loaded
- Live preview updates as you type
- 8 professional colour themes
- 5 cutting guide styles
- Print-ready A4 layout at 96 DPI
- XSS-safe input handling via HTML escaping

---

## Getting Started

### Prerequisites

- Any modern web browser (Chrome, Firefox, Edge, Safari)

### Quick Start

1. **Clone the repository:**

   ```bash
   git clone https://github.com/GT-Nutri-Bites/LabelsStudioPro.git
   cd LabelsStudioPro
   ```

2. **Open the application:**

   ```bash
   # Simply open the HTML file in your browser
   open index.html
   # or
   xdg-open index.html   # Linux
   start index.html       # Windows
   ```

   Alternatively, serve it with any static file server:

   ```bash
   python3 -m http.server 8080
   # Then visit http://localhost:8080
   ```

No build step, no package installation, and no configuration required.

---

## Features & Functions

### 1. Brand Identity Configuration

| Field | Details |
|-------|---------|
| **Business Name** | Text input, max 30 characters, required. Displayed in the label header bar. |
| **Label Colour Theme** | 8 preset colour themes (Navy, Forest, Merlot, Slate, Copper, Plum, Coal, Teal). Each theme sets the header background, accent colour, and accent background on the label. |

- Live character counter with colour-coded warnings (green → amber at 80% → red when exceeded)
- Theme selection updates all labels instantly via CSS custom properties

### 2. Product Information Entry

| Field | Details |
|-------|---------|
| **Product Name** | Text input, max 40 characters, required. Supports variant/size notation (e.g., `Premium Herbal Tea · 100g`). |

- Character counter with the same warning system as Business Name

### 3. Dates & Traceability

| Field | Details |
|-------|---------|
| **Manufacture Date** | Text input, format `DD-Mon-YYYY`. Displayed in teal on the label. |
| **Expiration Date** | Text input, format `DD-Mon-YYYY`. Displayed in red for high visibility. |
| **Batch / Lot Number** | Text input, required. Unique code for product traceability and recall management. |

### 4. Company Details

| Field | Details |
|-------|---------|
| **Company / Legal Name** | Text input for the registered business name. |
| **Address** | Textarea (multi-line). Newlines are converted to spaces for label fit. |
| **Contact Number** | Text input for telephone number. |
| **Website** | Text input, displayed in the label's dark accent bar. |

### 5. Cutting Guidelines

Five cutting guide styles for the A4 sheet:

| Style | Description | Best For |
|-------|-------------|----------|
| **Dashed Border** | Classic perforated-cut dashed outline | Manual scissors cutting |
| **Solid Lines** | Continuous solid border lines | Guillotine/straight-edge cutter |
| **Crop Marks** | Professional corner marks at each label corner | Professional print shops |
| **Dashed + Crop Marks** | Combination of dashed borders and corner marks | Maximum precision |
| **No Guide Lines** | Clean sheet with no visible guides | Pre-cut die-cut label sheets |

Additional options:
- **Light-colour guides** — reduces guide visibility for cleaner printed output (recommended)
- **Show cutting guide on single label preview** — overlays the selected cut style on the single label view

### 6. Sheet Settings

| Setting | Options | Details |
|---------|---------|---------|
| **Columns** | 3, 4, or 5 | Number of label columns per sheet |
| **Rows** | 6, 8, 10, or 11 | Number of label rows per sheet |
| **Number of Sheets** | 1–99 | Adjustable via +/− buttons; total labels auto-calculated |

- Label dimensions are fixed at **1.5″ × 1.0″**
- Grid dimensions auto-calculate to fit the A4 page (794 × 1123 px at 96 DPI)

### 7. Live Label Preview

- Real-time preview of a single label card at actual print size (1.5″ × 1.0″)
- Scalable from 50% to 500% zoom
- Displays specification chips showing current settings (size, paper, cut style, grid, theme)
- Label sections: Business Name header → Product Name → Dates → Batch → Website → Company Info → Contact

### 8. A4 Sheet Preview

- Full A4 page layout showing all labels in a grid
- Sheet header with metadata (grid dimensions, label count)
- Responsive grid that adjusts based on column/row settings
- Cutting guides rendered according to the selected style
- Each label on the sheet matches the single preview exactly

### 9. Zoom Controls

| Control | Action |
|---------|--------|
| **− / + buttons** | Decrease/increase zoom by 25% steps |
| **Slider** | Drag to set zoom from 50% to 500% |
| **Reset Zoom button** | Resets to 250% (default) |
| **Ctrl/Cmd + Scroll** | Mouse wheel zoom on the preview area |

### 10. Print Summary Modal

A modal dialog showing:
- **Labels per Sheet** — calculated from columns × rows
- **Sheets Required** — user-configured quantity
- **Total Labels** — per-sheet count × sheet quantity
- **Cutting Guide** — currently selected style

Includes a 4-step printing guide:
1. Set page scaling to 100% / Actual Size
2. Load A4 self-adhesive label sheets
3. Test print on plain paper first
4. Cut along guide lines with a straight-edge cutter

### 11. Print Functionality

- Automatically switches to the A4 Sheet view before printing
- Triggers the browser's native print dialog
- Print CSS hides all UI elements (sidebar, toolbar, stats bar)
- Sets exact A4 dimensions (210 mm × 297 mm) with proper margins
- Supports `print-color-adjust: exact` for accurate colour reproduction
- Uses `page-break-after: always` for multi-sheet support

### 12. Reset Form

- Restores all fields to default sample data
- Resets theme to Navy, cutting guide to Dashed Border, sheets to 1
- Triggers a toast notification confirming the reset

### 13. Toast Notifications

- Temporary message pop-ups in the bottom-right corner
- Three colour variants: default (teal), copper, and red
- Auto-dismiss after 2.8 seconds
- Smooth slide-up animation

### 14. Statistics Bar

A persistent footer bar displaying:
- Labels per sheet (with live pulse indicator)
- Number of sheets
- Total label count
- Active cutting guide style
- Technical specs (A4 · 1.5″×1″ · 96dpi)
- Quick access to Print Summary

### 15. Keyboard & Scroll Interactions

- **Ctrl/Cmd + Mouse Wheel** on the preview area zooms in/out by 25% steps
- All form inputs trigger live updates on every keystroke (`oninput` events)

---

## JavaScript Functions Reference

| Function | Purpose | Parameters |
|----------|---------|------------|
| `g(id)` | Get DOM element by ID | `id` — element ID string |
| `v(id)` | Get input value by element ID (returns `''` if missing) | `id` — element ID string |
| `esc(s)` | HTML-escape a string (XSS prevention) | `s` — raw string |
| `toast(msg, type, dur)` | Show a toast notification | `msg` — message text, `type` — `'default'`/`'copper'`/`'red'`, `dur` — duration in ms (default: 2800) |
| `buildSwatches()` | Build colour theme picker UI from `THEMES` array | — |
| `applyTheme(idx)` | Apply a colour theme by index | `idx` — theme index (0–7) |
| `labelHTML()` | Generate the inner HTML for a single label card | — (reads form values) |
| `updateSingle()` | Re-render the single label preview | — |
| `updateA4()` | Re-render the A4 sheet grid with all labels | — |
| `charCounts()` | Update character count indicators for Business Name and Product Name | — |
| `update()` | Master update — calls `charCounts()`, `updateSingle()`, `updateA4()` | — |
| `setZoom(z)` | Set preview zoom level (clamped 50–500) | `z` — zoom percentage |
| `adjZoom(d)` | Adjust zoom by a delta value | `d` — delta (e.g., +25 or −25) |
| `switchTab(id, el)` | Switch between Single/A4 preview tabs | `id` — `'single'`/`'sheet'`, `el` — clicked tab element |
| `setCut(el)` | Set cutting guide style | `el` — clicked cutting option element |
| `adjSheets(d)` | Adjust sheet quantity (clamped 1–99) | `d` — delta (+1 or −1) |
| `openModal()` | Open print summary modal | — |
| `closeModal()` | Close print summary modal | — |
| `doPrint()` | Switch to A4 view and trigger browser print | — |
| `resetForm()` | Reset all form fields to default sample data | — |

**Global Variables:**

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `zoom` | Number | `250` | Current zoom percentage |
| `cutClass` | String | `'cut-dashed'` | CSS class for active cutting style |
| `cutLabel` | String | `'Dashed Border'` | Display name of active cutting style |
| `sheetsCount` | Number | `1` | Number of sheets to print |
| `activeTheme` | Number | `0` | Index of the currently active theme |
| `THEMES` | Array | 8 items | Colour theme definitions (name, primary, accent, accentL) |

---

## Technology Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| **Markup** | HTML5 | Semantic elements, forms, meta viewport |
| **Styling** | CSS3 | Custom properties, Flexbox, Grid, animations, `@media print` |
| **Logic** | Vanilla JavaScript (ES6+) | No frameworks or libraries |
| **Fonts** | Google Fonts | Playfair Display, IBM Plex Sans, IBM Plex Mono |
| **Icons** | Unicode Emoji | No icon library dependency |

---

## Project Structure

```
LabelsStudioPro/
├── index.html          # Complete application (HTML + CSS + JS)
└── README.md           # This documentation file
```

The entire application is contained in a single `index.html` file (~56 KB, ~1356 lines):
- **Lines 1–731:** `<head>` with embedded CSS (~900 lines covering reset, layout, components, print styles, animations)
- **Lines 732–1120:** `<body>` HTML markup (topbar, sidebar form, preview panels, modal, toast)
- **Lines 1125–1354:** `<script>` with all JavaScript logic (17 functions, 5 global variables)

---

## Deployment

Label Studio Pro works with any static file hosting. No build step required.

**Options:**
- **GitHub Pages** — push to `main` branch and enable Pages in repository settings
- **Netlify / Vercel** — connect the repository for automatic deployment
- **Any web server** — copy `index.html` to the server's document root
- **Local** — open `index.html` directly in any modern browser

---

## Future Enhancements

### Short-term Improvements

- [ ] **Custom colour picker** — allow users to define custom theme colours beyond the 8 presets using a colour picker input
- [ ] **Image/logo upload** — support uploading a brand logo to display on each label
- [ ] **QR code generation** — auto-generate QR codes from the website URL or batch code for traceability
- [ ] **Barcode support** — generate and embed barcodes (Code128, EAN-13) on labels
- [ ] **Save/load configurations** — persist label configurations to `localStorage` or export/import as JSON files
- [ ] **Undo/redo** — implement undo/redo history for form changes
- [ ] **Dark mode** — add a dark mode toggle for the application UI

### Medium-term Features

- [ ] **Multiple label templates** — offer different label layouts (horizontal, vertical, circular, custom shapes)
- [ ] **Custom label dimensions** — allow user-defined label sizes beyond 1.5″ × 1.0″
- [ ] **Multi-product sheets** — support mixing different products on a single sheet
- [ ] **PDF export** — generate print-ready PDF files directly (using libraries like jsPDF or html2pdf)
- [ ] **Drag-and-drop label editor** — allow repositioning label fields via drag and drop
- [ ] **Font customisation** — let users choose from additional fonts for label text
- [ ] **Ingredient list field** — add a dedicated field for nutritional or ingredient information
- [ ] **Responsive mobile layout** — optimise the sidebar and preview panels for mobile and tablet screens

### Long-term Vision

- [ ] **Backend integration** — connect to a backend for user accounts, saved templates, and team collaboration
- [ ] **Batch import** — import product data from CSV/Excel to generate labels for multiple products at once
- [ ] **Multi-language support** — internationalise the UI and support multilingual label content
- [ ] **Accessibility improvements** — full ARIA labelling, keyboard navigation for all interactive elements, screen reader support
- [ ] **PWA support** — convert to a Progressive Web App for offline use and home screen installation
- [ ] **Template marketplace** — community-contributed label templates that users can browse and use
- [ ] **Print service integration** — connect with commercial label printing services for direct ordering
- [ ] **Version history** — track changes to label designs with version control and rollback

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add my feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

<p align="center">
  Made with ❤️ by <strong>GT-Nutri-Bites</strong>
</p>
