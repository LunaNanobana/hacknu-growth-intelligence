# 📊 Growth Intelligence Pipeline — HackNU 2026
<img width="1904" height="791" alt="image" src="https://github.com/user-attachments/assets/2ad80d79-980f-4bf7-b074-5402f8a03be5" />



An automated competitive intelligence system that reverse-engineers Claude's viral growth patterns from Reddit and Hacker News, then displays findings on a live auto-refreshing dashboard.

---

## What It Does

1. **Scrapes** public Reddit & Hacker News posts (~9,200 total) using PRAW and the Algolia API
2. **Classifies** content automatically using LDA topic modelling (10 clusters) — no manual labelling
3. **Scores** each post with VADER sentiment analysis (compound score −1 to +1) and a custom virality metric
4. **Visualises** growth timelines, viral rate matrices, and complaint signals on a live HTML dashboard

---

## Key Findings

| Content Category | Viral Rate | Avg Sentiment |
|---|---|---|
| Research & Analysis | **16.0%** | +0.31 |
| Comparison posts | 13.0% | +0.23 |
| Coding & Dev | 8.7% | +0.21 |
| Rate-limit complaints | 8.0% | −0.08 |

- Code content scores **3.5× higher** than question posts
- A single viral tip/hack post scored 6,910 — more than the next 10 posts combined
- Post volume spiked **10× in 6 weeks** following the Claude Sonnet 4.6 release

---

## Tech Stack

`Python` · `PRAW` · `Algolia API` · `pandas` · `VADER` · `scikit-learn (LDA)` · `matplotlib` · `Flask`

---

## Project Structure

```
hacknu-growth/
├── reddit_scraper.py        # PRAW scraper — collects Reddit posts
├── reddit_scraper2.py       # Fallback scraper using public JSON endpoint
├── analysis.py              # Virality scoring + sentiment pipeline
├── deep_analysis_fixed.py   # LDA topic modelling + full enrichment
├── charts.py                # Chart generation (4 output charts)
├── build_dashboard.py       # Builds the live HTML dashboard
├── generate_report.py       # Generates markdown report from data
├── architecture.py          # Pipeline architecture diagram
├── server.py                # Flask server to serve the dashboard
├── dashboard.html           # Auto-refreshing analytics dashboard
├── reddit_data.csv          # Raw scraped dataset
├── counter_playbook.md      # Growth strategy derived from findings
└── architecture.png         # System architecture diagram
```

---

## Setup & Run

```bash
# 1. Clone
git clone https://github.com/YOUR_USERNAME/hacknu-growth-intelligence.git
cd hacknu-growth-intelligence

# 2. Install dependencies
pip install praw pandas vaderSentiment scikit-learn matplotlib flask requests

# 3. Scrape data
python reddit_scraper.py

# 4. Run analysis
python analysis.py
python deep_analysis_fixed.py

# 5. Generate charts
python charts.py

# 6. Launch dashboard
python server.py
# Open http://localhost:5000
```

> **Note:** Reddit scraper uses the public JSON endpoint — no API key needed. HN data uses the free Algolia search API.

---

## Dashboard Preview

The dashboard shows:
- Monthly post volume timeline with model release markers
- Viral rate bubble chart (sentiment × virality × volume)
- Reddit title formula analysis
- Rate-limit complaint trend over time

---

## Assumptions & Tradeoffs

- Used Reddit public JSON endpoint instead of the official API due to CAPTCHA constraints during the hackathon
- Focused on Reddit + HN only — highest signal platforms for technical discourse
- VADER has ~12% noise rate on sarcastic/technical posts (validated by spot-check of 50 posts)
- Virality proxy: `upvotes + (comments × 2)` — doesn't capture external shares, so true virality is likely underestimated

---

*Built at HackNU 2026 in 24 hours.*
