# SC3008_Kickstarter_Research_Project
NLP + LLM pipeline to score ESG authenticity in Kickstarter crowdfunding campaigns. Builds a Crowdfunding Authenticity Index (CAI) across 5 dimensions using web scraping, TF-IDF, BERT, and an LLM agent layer.

# Crowdfunding Authenticity Index (CAI)
### SC3008 — NLP & LLM Pipeline for ESG Authenticity in Kickstarter Campaigns

This project builds a **Crowdfunding Authenticity Index** that scores Kickstarter campaigns on how genuinely aligned they are with Environmental, Social, and Governance (ESG) principles. It combines web scraping, NLP feature extraction, and an LLM agent orchestration layer to produce a composite authenticity score for each campaign.

---

## Overview

Crowdfunding platforms like Kickstarter are increasingly used to fund ESG-oriented products. But how authentic are those claims? This project operationalises "authenticity" across five theoretically-grounded dimensions and scores campaigns from the full Kickstarter historical dataset.

**Final deliverable:** Research report + reproducible Python pipeline.

---

## CAI Framework

The index is computed as a weighted sum of five dimensions:

| Dimension | Weight | Key Signals |
|---|---|---|
| Behavioural Transparency | 0.25 | Update frequency, ESG disclosure, creator reply rate |
| Cognitive Credibility | 0.25 | Claim specificity, concreteness, third-party certifications |
| Affective Sincerity | 0.20 | Emotional language, personal storytelling, altruistic framing |
| Social Validation | 0.15 | Backer count, comment sentiment, ESG discussion density |
| Institutional Legitimacy | 0.15 | Credentials, creator track record, category alignment |

All indicators are normalised to [0, 1] before aggregation. Weights are validated via exploratory factor analysis (EFA/PCA).

---

## Pipeline

```
Raw Kickstarter CSVs 
        ↓
Date conversion + deduplication
        ↓
Web scraper → campaign story, FAQ, comments, updates
        ↓
ESG labelling (keyword dictionary, TF-IDF)
        ↓
NLP feature extraction (LIWC, BERT, sentiment, regex)
        ↓
CAI scoring (normalise → weighted sum)
        ↓
LLM agent layer (orchestration + natural language summaries)
        ↓
Analysis + report
```

---

## Repository Structure

```
├── data/
│   ├── raw/                  # Original Kickstarter CSVs
│   └── processed/            # Cleaned, merged, deduplicated master CSV
├── scraper/
│   └── kickstarter_scraper.py   # Story, FAQ, comments scraper
├── notebooks/
│   ├── 01_kickstarter_convertdates.ipynb   # Date conversion + merge
│   ├── 02_esg_labelling.ipynb              # ESG keyword scoring
│   ├── 03_nlp_features.ipynb               # NLP feature extraction
│   ├── 04_cai_scoring.ipynb                # CAI index computation
│   └── 05_analysis.ipynb                   # EFA, topic modelling, results
├── agents/
│   └── cai_agent.py          # LLM agent wrapper (orchestrates pipeline tools)
├── reports/
│   └── final_report.pdf
└── requirements.txt
```

---

## Tech Stack

- **Data**: pandas, glob, openpyxl
- **Scraping**: Scrapy / requests + BeautifulSoup
- **NLP**: spaCy, NLTK, scikit-learn (TF-IDF), HuggingFace Transformers (BERT)
- **Sentiment & LIWC**: VADER, LIWC dictionaries
- **Topic modelling**: Gensim (LDA)
- **Validation**: pingouin (EFA), scikit-learn (PCA)
- **LLM agents**: LangChain + OpenAI / Anthropic API
- **Visualisation**: matplotlib, seaborn

---

## Data Sources

- **Kickstarter historical dataset** — scraped snapshots from Web Archive (2014–present), 84 CSV files merged into a single master dataset
- **Campaign pages** — story text, FAQ, backer comments, and creator updates scraped directly from Kickstarter
- **ESG keyword dictionary** — based on Baier et al. (2020)

---

## Status

| Phase | Status |
|---|---|
| Date conversion + dedup | ✅ Done |
| Full scraping pipeline | 🔄 In progress |
| ESG labelling | ⬜ Upcoming |
| NLP feature extraction | ⬜ Upcoming |
| CAI scoring | ⬜ Upcoming |
| LLM agent layer | ⬜ Upcoming |
| Report | ⬜ Upcoming |

---

## References

- Baier, D., Berens, G., & Li, J. (2020). ESG keyword dictionaries.
- CAI framework grounded in Tier 1 (conceptual) and Tier 2 (empirical) authenticity literature.
