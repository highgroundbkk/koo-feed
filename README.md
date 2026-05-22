# 📡 KOO SUPERDEV — Signal Feed

Public signal dashboard for the KOO SUPERDEV ecosystem.  
Curated AI/devtools trends, updated **daily at 15:00 Bangkok time** by autonomous bots.

## 🌐 Live Site

→ **[https://highgroundbkk.github.io/koo-feed/](https://highgroundbkk.github.io/koo-feed/)**

| Page | Description |
|------|-------------|
| [📡 Signal](signal.md) | AI/devtools ecosystem dispatches — HN picks + GitHub trending |
| [📰 Feed](feed.md) | System activity log — bot runs, deploys, syncs |
| [📓 Journal](obra-superpowers.md) | Architecture decisions and development notes |

## 🤖 How It Works

A GitHub Actions workflow runs daily at **08:00 UTC (15:00 Bangkok)**:

1. **HN Signal Bot** — fetches top Hacker News stories, filters by AI/devtools keywords (score ≥ 40), deduplicates via `.hn-seen`, appends to `signal.md`
2. **GitHub Trending Bot** — fetches recently created repos by stars, appends top picks to `signal.md`
3. **Feed Logger** — logs each bot run with timestamp and entry count to `feed.md`

No LLM usage. No external services. Runs free on GitHub Actions.

## 📁 Repository Structure

```
koo-feed/
├── index.html              # Dashboard homepage
├── signal.html             # Signal dispatches page
├── feed.html               # Activity feed page
├── journal.html            # Development journal page
├── signal.md               # Signal data (updated daily by bot)
├── feed.md                 # Activity log (updated daily by bot)
├── obra-superpowers.md     # Development journal
├── .hn-seen                # Tracks seen HN story IDs (dedup)
└── .github/workflows/
    └── daily-signal.yml    # Daily automation workflow
```

## 🏗️ Architecture

This repo is the **public read surface** of the KOO SUPERDEV system:

- **koo-feed** (this repo) — public blog, curated markdown, zero secrets, served via GitHub Pages
- **gstack-private** (private) — private vault, all bots, 42 shell commands, full config backup

## 🔧 Ecosystem Monitoring

Signal categories tracked:

| Tag | Description |
|-----|-------------|
| `HN` | Hacker News community picks (score ≥ 40) |
| `RELEASE` | GitHub trending repos |
| `AI` | AI model and agent releases |
| `TOOL` | Developer tools |
| `BLOG` | Notable articles |

## ⚙️ Automation Schedule

| Workflow | Schedule | What it does |
|----------|----------|--------------|
| `daily-signal.yml` | Daily 08:00 UTC | Fetch HN + GitHub trending → update `signal.md` + `feed.md` |

Trigger manually: **Actions → Daily Signal Update → Run workflow**
