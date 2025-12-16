# Personal Daily Weather Brief (Go)

A lightweight Go CLI that fetches **tomorrow’s forecast** for a city and generates a **practical daily weather brief** for planning (commute + what to carry/wear).  
Designed as an “AI Essentials for everyday work” capstone: **data → interpretation → actionable summary**.

## What this project does (and does not do)
- ✅ Summarizes an **existing forecast** into an actionable brief.
- ✅ Provides **rule-based recommendations** (reliable by default).
- ✅ Optionally uses an LLM to **polish tone** while keeping facts locked to input.
- ❌ Does **not** attempt true meteorological prediction.

---

## Features
- City-based forecast retrieval via **Open-Meteo** (no API key required)
- Clean bullet-style brief (terminal output)
- Markdown export to `brief.md`
- Offline demo mode (`--mock`)
- Optional CSV logging for visualizations (`--csv`)
- Optional LLM enhancement (OpenAI-compatible) with safe fallback

---

## Quick start
```bash
go mod tidy
go run ./cmd/brief --city "Nairobi"
```

This prints the brief and writes `brief.md` in the current directory.

---

## Usage

### Basic
```bash
go run ./cmd/brief --city "Nairobi"
```

### With preferences
```bash
go run ./cmd/brief --city "Nairobi" --commute motorbike --sensitivity normal --tone friendly
```

### Offline demo mode
```bash
go run ./cmd/brief --city "Nairobi" --mock
```

### Choose output file
```bash
go run ./cmd/brief --city "Nairobi" --out mybrief.md
```

### Log results to CSV (for charts/visualization)
```bash
go run ./cmd/brief --city "Nairobi" --csv
```

By default, this appends to `runs.csv` in the current directory.

---

## Visualization (Charts / Results)
You have two simple options:

### A) Google Sheets (no coding)
1. Run several times (different cities or different days):
   ```bash
   go run ./cmd/brief --city "Nairobi" --csv
   go run ./cmd/brief --city "Mombasa" --csv
   ```
2. Import `runs.csv` into Google Sheets (File → Import).
3. Insert a chart:
   - X-axis: `date`
   - Series: `temp_max_c` and/or `rain_probability_pct`

See: `docs/visualization.md`

### B) Local Python plot (quick and clean)
After collecting a few rows in `runs.csv`:
```bash
python3 scripts/plot_runs.py runs.csv
```

This creates PNG charts in `charts/` (e.g., temperature and rain probability).

---

## Optional: LLM enhancement (tone polish)
The tool works without an LLM.

To enable an OpenAI-compatible endpoint:
```bash
export BRIEF_USE_LLM=1
export BRIEF_LLM_PROVIDER=openai_compatible
export BRIEF_LLM_API_KEY="YOUR_KEY"
export BRIEF_LLM_BASE_URL="https://api.openai.com/v1"
export BRIEF_LLM_MODEL="gpt-4o-mini"
```

If LLM config is missing/invalid, the app **falls back** to rule-only output.

---

## Repository structure
```
weather-brief/
  cmd/brief/                 # CLI entrypoint
  internal/weather/          # weather providers (Open-Meteo + mock)
  internal/brief/            # brief generation rules + optional enhancer + CSV logger
  internal/llm/              # minimal OpenAI-compatible client (optional)
  docs/visualization.md      # visualization guide (Sheets + Python)
  scripts/plot_runs.py       # local plotting script for runs.csv
  TOOLKIT.md                 # toolkit document (course submission)
  README.md
  go.mod
  LICENSE
```

---

## License
MIT — see `LICENSE`.
