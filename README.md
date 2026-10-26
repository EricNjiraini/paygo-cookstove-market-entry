# PayGo Clean Cookstove — Market Entry Analysis
**Kenya · Uganda · Tanzania · Ethiopia**

> An end-to-end portfolio project replicating the analytical workflow of a BI Manager at a PayGo energy company (e.g. M-KOPA, BURN, Sun King). Three interconnected modules — market sizing, credit risk scoring, and churn prediction — converging on a single market-entry recommendation.

---

## Project Narrative

You are the data analyst for a hypothetical PayGo cookstove company evaluating:

1. **Which country and sub-national zone** to enter first
2. **Who to extend credit to** at point of onboarding
3. **Who is likely to churn** and when — so field agents can intervene early

This mirrors real internal analytics at companies operating across East Africa's ~$1B PayGo clean energy market.

---

## Repository Structure

```
paygo-cookstove-market-entry/
├── notebooks/
│   ├── 01_data_collection.ipynb          # API pulls, DHS download, data audit
│   ├── 02_country_comparison.ipynb       # Module 1: macro market dimensions
│   ├── 03_market_entry_scorecard.ipynb   # Module 1: country ranking + heat map
│   ├── 04_credit_risk_model.ipynb        # Module 2: default probability model
│   ├── 05_churn_prediction.ipynb         # Module 3: survival + 30-day classifier
│   └── 06_integrated_dashboard.ipynb     # Ties all three modules together
├── data/
│   ├── raw/                              # Downloaded source files (gitignored if large)
│   ├── processed/                        # Cleaned, merged datasets
│   └── simulated/                        # Synthetic customer ledger (see disclaimer)
├── outputs/
│   ├── figures/                          # All charts and maps
│   ├── models/                           # Serialised .pkl model files
│   └── tables/                           # Scorecard CSVs, ranking outputs
├── docs/
│   ├── data_sources.md                   # Full provenance for every dataset
│   ├── methodology.md                    # Analytical decisions + assumptions
│   └── data_dictionary.md               # Field definitions across all datasets
└── README.md
```

---

## Modules

### Module 1 — Market Sizing & Entry Prioritisation
**Question:** Which country and sub-national zones offer the best PayGo opportunity right now?

Segments the addressable market using the Clean Cooking Alliance framework:
- **Early adopters** — high consumption power, electricity access, quality housing
- **Fast followers** — banked, credit-accessible households
- **Secondary followers** — limited financial inclusion

Country comparison dimensions: clean cooking access deficit, mobile money penetration, PayGo market maturity (Lighting Global MAI), financial inclusion (Findex 2021), urban/rural split, regulatory environment.

Output: Weighted scorecard ranking + sub-national opportunity heat maps for all four countries.

---

### Module 2 — Credit Risk Scoring
**Question:** Given a new customer's profile at sign-up, what is their probability of defaulting?

Binary classification (default / non-default) using onboarding features only.

Key benchmark from GOGLA: The sector average repayment rate is **72%** — $28 of every $100 financed is not recovered. Cohorts with downpayment > 10% show significantly better repayment; < 5% downpayment cohorts show the worst performance.

Models compared: Logistic Regression → Random Forest → XGBoost. Evaluated on AUC-ROC and precision-recall. Feature importance chart surfaces the main default drivers.

---

### Module 3 — Churn Prediction & Retention
**Question:** Among active customers, who is about to stop paying — and when?

A customer is considered churned when they stop paying for consecutive days (forcing product lockout) or abandon the product entirely.

Approach: Survival analysis (time-to-churn) + 30-day binary classifier. Output is a daily risk score per customer for field agent or call centre action.

---

## Data Sources

| Dataset | Source | Free? |
|---|---|---|
| Lighting Global PAYGo Market Attractiveness Index | lightingglobal.org | ✅ |
| World Bank Global Findex 2021 | datacatalog.worldbank.org | ✅ |
| GSMA Mobile Money dataset | gsma.com | ✅ |
| DHS data — KE, UG, TZ, ET | dhsprogram.com | ✅ (registration) |
| GOGLA PAYGo PERFORM benchmarks | gogla.org | ✅ (published reports) |
| Facebook / Meta Relative Wealth Index | data.humdata.org | ✅ |
| FinAccess Kenya 2021 household survey | knbs.or.ke | ✅ |

---

## ⚠️ Disclaimer: Simulated Transaction Data

No public PayGo customer transaction dataset exists — real companies treat this as a core commercial asset. The customer payment ledger used in Modules 2 and 3 is **synthetically generated** using GOGLA benchmark distributions (repayment rates, default rates, contract lengths by segment). All simulated data is clearly labelled. Findings are illustrative, not drawn from a live portfolio.

---

## Skills Demonstrated

| Skill | Where |
|---|---|
| Geospatial analysis & choropleth mapping | Notebooks 02–03 |
| Feature engineering from survey microdata | Notebooks 02, 04 |
| Binary classification (LR / RF / XGBoost) | Notebook 04 |
| Survival analysis (Kaplan-Meier, Cox PH) | Notebook 05 |
| Model evaluation (AUC-ROC, precision-recall) | Notebooks 04–05 |
| Dashboard design | Notebook 06 |

---

## Relevance

Market intelligence, credit modelling and customer analytics are the three analytical questions behind most growth decisions in PayGo energy. This project works through all three with public data and a simulated customer ledger, and brings them together in one market-entry recommendation.

---

## Setup

```bash
git clone https://github.com/EricNjiraini/paygo-cookstove-market-entry.git
cd paygo-cookstove-market-entry
pip install -r requirements.txt
jupyter lab
```

Start with `notebooks/01_data_collection.ipynb`.
