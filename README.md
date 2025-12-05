# US Patent Data by Metropolitan Area (2015)

## Overview

This project visualizes US patent activity across metropolitan statistical areas (MSAs/CBSAs) using data from the US Patent and Trademark Office (USPTO). It combines USPTO patent counts with US Census geographic data to create interactive maps and charts showing innovation hubs across America.

The final output is a clean, analysis-ready CSV file (`datawrapper_cleaned.csv`) that powers Datawrapper visualizations showing the top 5 patent-producing metros in simplified, user-friendly labels.

## What This Project Does

1. **Scrapes patent data** from the USPTO CBSA table for 2015
2. **Cleans and normalizes** metro area names to match Census gazetteer standards
3. **Matches geographic IDs** (CBSA codes) for each metropolitan area
4. **Highlights the top 5** innovation centers with simplified labels
5. **Produces a final CSV** ready for visualization tools like Datawrapper

**Key Data Sources:**
- USPTO: Patent counts by CBSA (all CBSAs in US)
- US Census Bureau: `2023_Gaz_cbsa_national.txt` (geographic reference data)

## Project Structure

```
.
├── index.ipynb                           # Main processing notebook
├── 2023_Gaz_cbsa_national.txt          # Census gazetteer data (geography reference)
├── datawrapper_cleaned.csv             # Output: final clean dataset for visualization
├── requirements.txt                     # Python dependencies
└── .github/workflows/ci.yml            # Automated execution on GitHub push
```

## Quick Start

### 1. Clone and Set Up

```bash
git clone <repo-url>
cd maps
source .venv/bin/activate
pip install -r requirements.txt
```

### 2. Run the Notebook

**Option A: Interactive (Recommended)**
- Open `index.ipynb` in VS Code or Jupyter Lab
- Run cells top-to-bottom
- See outputs and debug interactively

**Option B: Automated**
```bash
python -m nbconvert --to notebook --execute index.ipynb --inplace
```

### 3. Output

After execution, `datawrapper_cleaned.csv` will contain:
- `cbsa` — CBSA geographic identifier (5-digit code)
- `msa_name` — Metropolitan area name
- `patent_count` — Number of patents (2015)
- `top5_label` — Simplified name if metro is in top 5, blank otherwise

## Top 5 Metro Areas by Patents (2015)

The final dataset highlights these innovation leaders:
- San Jose, CA (Silicon Valley)
- San Francisco, CA (Bay Area)
- Seattle, WA
- Minneapolis–St. Paul, MN–WI
- Dallas–Fort Worth, TX

## How the Cleaning Works

### Data Pipeline Steps

1. **Patent scrape** — Extract USPTO CBSA table for 2015
2. **Name cleanup** — Normalize whitespace, dashes, and special characters
3. **Gazetteer matching** — Join patents to Census geographic codes using:
   - Exact name matching (first pass)
   - Fuzzy matching at 92% similarity (second pass)
4. **Deduplication** — Remove or combine duplicate entries
5. **Top-5 labeling** — Mark the highest patent-count metros with clean, user-friendly names
6. **Final filtering** — Remove unmatchable CBSAs with red-flag codes

### Why This Matters

The notebook keeps all intermediate data **in-memory** and writes only the final clean CSV, avoiding hundreds of temporary files and keeping the repository clean and fast.

## Using the Output

The `datawrapper_cleaned.csv` is designed for:
- **Datawrapper** interactive maps and charts
- **Tableau** dashboards
- **Excel/Google Sheets** pivot tables and filters
- Any visualization tool that accepts CSV input

## Development & CI

A GitHub Actions workflow automatically:
- Installs dependencies
- Executes the notebook
- Uploads the clean CSV as an artifact for download

See `.github/workflows/ci.yml` for details.

## Project Structure & Dependencies

**Python Packages (see `requirements.txt`):**
- `pandas` — Data manipulation
- `requests` — Web scraping
- `beautifulsoup4` — HTML parsing
- `nbconvert` — Notebook execution
- Jupyter tools for notebook support

**Data Files:**
- `.venv/` — Virtual environment (ignored; not committed)
- `*.csv` — Intermediate files (ignored; recreated on each run)
- `datawrapper_cleaned.csv` — Final output (safe to commit or upload separately)

## Notes for Users

- **Running locally?** Make sure you have Python 3.13+ and activate the `.venv` before running
- **No internet connection?** The notebook requires internet to scrape USPTO data
- **Want to customize?** Edit the `scrape_uspto_cbsa_patents()` function to change years (2000–2015) or the top_5 mapping to use different labels
- **Reproducibility:** All dependencies are pinned in `requirements.txt` for consistent results across machines

