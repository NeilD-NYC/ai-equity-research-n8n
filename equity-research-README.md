# Weekly AI Equity Research Report Generator

> **Automated n8n workflow that transforms financial statements and news into institutional-quality equity research reports — powered by GPT-4.1, delivered as PDF every Monday morning.**

[![n8n](https://img.shields.io/badge/n8n-workflow-FF6D5A?style=flat)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/GPT--4.1--mini-powered-412991?style=flat&logo=openai&logoColor=white)](https://openai.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## What Is This?

A fully automated weekly workflow that generates structured equity research reports for any list of public companies. Every Monday at 8AM it pulls 5 years of financial data, fetches recent market news, computes key financial signals, runs dual AI analysis pipelines, and delivers a formatted PDF research report to your inbox.

Built by a former institutional allocator with 20+ years of buy-side experience — the analytical framework mirrors the actual equity screening and risk assessment methodology used at multi-billion-dollar investment offices.

---

## Pipeline Architecture

```
[Monday 8AM Trigger]
        │
        ▼
[Google Sheets] ← company watchlist with enabled/disabled toggle
        │
        ▼
[Filter: enabled only] → [Iterate per company]
        │
        ├──► Fetch Income Statement  (FMP API, 5 years)
        ├──► Fetch Balance Sheet     (FMP API, 5 years)
        ├──► Fetch Cash Flow         (FMP API, 5 years)
        └──► Fetch Market News       (NewsAPI, 10 articles)
                │
                ▼
        [Normalize all data]
                │
                ▼
        [Compute Financial Signals]
        ├── Revenue growth (5Y CAGR)
        ├── Operating margin
        ├── Debt-to-equity ratio
        ├── Free cash flow margin
        └── Capital allocation (buybacks)
                │
          ┌─────┴─────┐
          ▼           ▼
    [SWOT Agent]  [Risk & Growth Agent]
    GPT-4.1-mini  GPT-4.1-mini
          │           │
          └─────┬─────┘
                ▼
        [Build HTML Report]
                │
                ▼
        [Render to PDF]
                │
                ▼
        ┌───────┴───────┐
        ▼               ▼
[Log to Sheets]  [Email PDF link]
```

---

## Report Output

Each generated report includes:

- **Company Symbol & Header**
- **Strengths** — data-grounded competitive and financial advantages
- **Weaknesses** — margin pressure, leverage, cash flow concerns
- **Opportunities** — growth vectors from news and financial trends
- **Threats** — macro, competitive, and regulatory risks
- **Key Risks** — specific business and financial risk factors
- **Growth Outlook (12–24 months)** — forward-looking narrative grounded in financials

AI is strictly instructed to base all output on provided data only — no invented facts, no hallucination.

---

## Prerequisites

| Service | Purpose |
|---------|---------|
| [n8n](https://n8n.io/) | Workflow orchestration (self-hosted or cloud) |
| [Financial Modeling Prep](https://financialmodelingprep.com/) | Income statement, balance sheet, cash flow data |
| [NewsAPI](https://newsapi.org/) | Recent market news per ticker |
| [OpenAI](https://openai.com/) | GPT-4.1-mini for SWOT + risk analysis |
| [HTML/CSS to PDF](https://htmlcsstopdf.com/) | Report PDF rendering |
| Google Sheets | Company watchlist + report log |
| Gmail | Report delivery |

---

## Setup

1. Import `equity_research_workflow.json` into your n8n instance
2. Configure credentials for each service
3. Create a Google Sheet with columns: `ticker`, `enabled` (TRUE/FALSE)
4. Replace all `YOUR_*_API_KEY` placeholders with your actual keys
5. Update `your_email@example.com` in the Send Email node
6. Activate the workflow — it will trigger every Monday at 8AM

**Google Sheet structure:**
| ticker | enabled |
|--------|---------|
| AAPL   | TRUE    |
| MSFT   | TRUE    |
| TSLA   | FALSE   |

---

## Customization

- **Add companies:** Add rows to your Google Sheet — no workflow changes needed
- **Change schedule:** Edit the Weekly Equity Research Trigger node
- **Swap AI model:** Change `gpt-4.1-mini` to `gpt-4.1` for deeper analysis
- **Extend report:** Add valuation multiples, peer comparison, or price target sections

---

## Related Projects

| Project | Description |
|---------|-------------|
| [altbots-tearsheet](https://github.com/NeilD-NYC/altbots-tearsheet) | AI pipeline for alternative investment manager tearsheets |
| [Alice-ai-agent](https://github.com/NeilD-NYC/Alice-ai-agent) | Personal AI chief-of-staff via Telegram |
| [AltBots Platform](https://altbots.io) | Full institutional research platform |

---

## Background

**Neil Datta** — Founder, AltBots / NKD Advisory LLC

Former MD & Global Head of Risk & Diligence at Optima/Forbes Family Trust ($24B MFO). 2,000+ manager reviews. 500+ investments closed. $9B+ deployed across alternative asset classes. Building AI automation for institutional finance since 2022.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-in%2Fneildatta-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/neildatta)

---

## License

MIT — see [LICENSE](./LICENSE)
