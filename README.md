# TFS Dashboard

A single-file, zero-dependency web dashboard for Azure DevOps / TFS that tracks **AI adoption**, **sprint progress**, **completed work**, and **work item timelines** — all from the browser using the TFS REST API.

![Version](https://img.shields.io/badge/version-3.2.1-blue) ![License](https://img.shields.io/badge/license-Proprietary-red) ![Zero Dependencies](https://img.shields.io/badge/dependencies-0-green)

---

## Features

### 🤖 AI Adoption Tracker
- Measures AI vs manual task distribution across assignees
- AI efficiency calculation: `(estimate - completed) / estimate × 100`
- Configurable efficiency target (default 40%) — estimates include extra buffer for AI tasks
- Color-coded ratings: Excellent (≥60%), Good (≥target), Moderate, Below target
- Per-assignee breakdown with bar charts and sortable tables
- L1 task exclusion from AI efficiency metrics
- Custom TFS field detection for task execution type

### ⏱ Sprint Tracker
- Real-time sprint data from TFS iteration API
- Per-assignee task grid with configurable columns (drag, reorder, resize, show/hide)
- Daily hours breakdown with capacity tracking and team days off
- AI efficiency panel with below-target task alerts and suggested adjustments
- Hour Update popup: view/edit hours per assignee with daily suggestions
  - State-priority sorting: Active → Resolved → Closed → New → Proposed
  - ALM daily rate support, AI target-aware suggestions
  - Proposed/New tasks shown but excluded from suggestions
  - Live calculation of new completed/remaining values
  - Direct save to TFS via PATCH API
- Animated expand/collapse for assignee cards and popup open/close
- Sprint progress bar, capacity stats, and summary cards
- Efficiency panel: Avg AI Efficiency, Avg Manual Efficiency, AI vs Manual comparison

### ⚡ Completed Work
- Load completed tasks by iteration with requirement grouping
- Tree view: Requirements → child Tasks with hours breakdown
- Filter by iteration, assignee, area path
- Export to CSV / copy to clipboard

### 📋 Work Item Timeline
- Search and visualize work items across sprints
- Sortable, filterable grid with custom column support
- Work item type badges (Task, Bug, Requirement, etc.)
- Link to TFS work item detail pages

---

## Quick Start

1. Open `TFS Dashboard - AI Adoption, Sprint Tracker & Completed Work.html` in a browser
2. Enter your TFS/Azure DevOps server URL (e.g., `https://tfs.example.com/tfs/Collection`)
3. Enter your Personal Access Token (PAT)
4. Select project and team, then start using any tab

> **No server, no build step, no dependencies.** Just one HTML file.

---

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| ALM Daily Rate | 0.25h/day | Hours per day for ALM-tagged tasks |
| AI Efficiency Target | 40% | Target efficiency % — estimates include this as extra buffer |
| PAT | — | TFS Personal Access Token (stored in browser session only) |

---

## AI Efficiency — How It Works

Estimates for AI-assisted tasks are planned with an extra buffer (configurable, default 40%). The efficiency metric measures how much of the estimate was saved:

```
Efficiency = (Original Estimate - Completed Hours) / Original Estimate × 100
```

**Example:** A task estimated at 10h (includes 40% buffer, base effort ~7.1h):
- Completed in 6h → Efficiency = 40% → On target
- Completed in 4h → Efficiency = 60% → Excellent
- Completed in 7h → Efficiency = 30% → Below target (warning shown)

| Rating | Threshold |
|--------|-----------|
| 🚀 Excellent | ≥ 60% |
| ⚡ Good | ≥ Target % |
| 📊 Moderate | < Target % (no warning) |
| ⚠️ Below target | < Target % and over allowed hours |

---

## Tech Stack

- **Pure HTML/CSS/JavaScript** — single file, no framework, no build
- **TFS REST API** (v2.0–v5.0) for data fetching
- **Zero external dependencies** — no CDN, no npm, no libraries
- Dark theme with CSS custom properties
- Responsive layout with animated transitions

---

## Browser Support

Modern browsers with ES6+ support:
- Chrome 60+
- Firefox 60+
- Edge 79+
- Safari 12+

---

## API Compatibility

| TFS / Azure DevOps Version | Supported |
|----------------------------|-----------|
| Azure DevOps Services | ✅ |
| Azure DevOps Server 2020+ | ✅ |
| TFS 2018+ | ✅ |
| TFS 2017 | ⚠️ Partial |

---

## Security

- PAT is stored in browser memory only (not persisted to disk)
- All API calls use Basic Auth over HTTPS
- No data is sent to any third-party service
- Cache-control headers prevent stale content

---

## License

Proprietary. Copyright © 2026 CDP. All rights reserved.
