# Data Sources & Provenance

Full documentation of every dataset used in this project.

---

## 1. Lighting Global PAYGo Market Attractiveness Index

| Field | Detail |
|---|---|
| **Publisher** | Lighting Global / World Bank Group |
| **Version** | 2023 edition (24-country index) |
| **URL** | https://www.lightingglobal.org/work-with-us/paygo-mai |
| **Licence** | Free download, registration required |
| **Used in** | Module 1 — Notebooks 02, 03 |
| **Local path** | `data/raw/lighting_global_mai/` |
| **Notes** | Composite index across: market size, financial infrastructure, regulatory environment, mobile money, off-grid supply, consumer awareness. East Africa four (KE, TZ, UG, ET) are included in the 24-country set. |

---

## 2. World Bank Global Findex 2021

| Field | Detail |
|---|---|
| **Publisher** | World Bank |
| **URL** | https://datacatalog.worldbank.org |
| **Indicators used** | FX.OWN.TOTL.ZS (account ownership), EG.CFT.ACCS.ZS (clean fuel access), SP.URB.TOTL.IN.ZS (urban population %) |
| **Licence** | CC BY 4.0 |
| **Used in** | Module 1 — Notebook 01, 02 |
| **Access method** | World Bank Data API (automated in Notebook 01) |

---

## 3. GSMA Mobile Money Dataset

| Field | Detail |
|---|---|
| **Publisher** | GSMA |
| **URL** | https://www.gsma.com/solutions-and-impact/connectivity-programmes/mobile-for-development/fintech/mobile-money |
| **Variables** | Mobile money account penetration, transaction volumes by country |
| **Licence** | Free download |
| **Used in** | Module 1 — Notebook 02 |
| **Local path** | `data/raw/gsma/` |

---

## 4. DHS Program — Household Survey Microdata

| Field | Detail |
|---|---|
| **Publisher** | ICF / USAID-funded DHS Program |
| **Countries** | Kenya (KEHR8AFL), Uganda (UGHR7BFL), Tanzania (TZHR7AFL), Ethiopia (ETHR8AFL) |
| **URL** | https://dhsprogram.com/data/ |
| **Licence** | Free, requires DHS account registration and project approval |
| **Used in** | Module 1 (sub-national segmentation), Module 2 (wealth, urban/rural features) |
| **Local path** | `data/raw/dhs/{KE,UG,TZ,ET}/` |
| **Key variables** | Household wealth index, cooking fuel type, urban/rural classification, gender of household head |

---

## 5. Meta / Facebook Relative Wealth Index

| Field | Detail |
|---|---|
| **Publisher** | Meta (Facebook) Connectivity Lab, via Humanitarian Data Exchange |
| **URL** | https://data.humdata.org/dataset/relative-wealth-index |
| **Resolution** | ~2.4 km grid cells |
| **Licence** | CC BY 4.0 |
| **Used in** | Module 1 (sub-national heat map), Module 2 (wealth proxy feature) |
| **Local path** | `data/raw/rwi/` |
| **Files** | `ken_relative_wealth_index.csv`, `uga_relative_wealth_index.csv`, `tza_relative_wealth_index.csv`, `eth_relative_wealth_index.csv` |

---

## 6. FinAccess Kenya 2021

| Field | Detail |
|---|---|
| **Publisher** | Kenya National Bureau of Statistics (KNBS) / FSD Kenya |
| **URL** | https://www.knbs.or.ke |
| **Licence** | Free download |
| **Used in** | Module 2 (mobile money usage frequency feature) |
| **Local path** | `data/raw/finaccess/` |

---

## 7. GOGLA PAYGo PERFORM Benchmarks

| Field | Detail |
|---|---|
| **Publisher** | GOGLA (Global Off-Grid Lighting Association) |
| **URL** | https://www.gogla.org |
| **Format** | Published PDF reports (2022, 2023 editions) |
| **Licence** | Free, publicly available |
| **Used in** | Modules 2 & 3 — simulation calibration |
| **Local path** | `data/raw/gogla_benchmarks.json` (manually encoded) |
| **Key figures encoded** | Sector avg repayment rate (72%), downpayment threshold effects, lockout trigger logic |

---

## ⚠️ Simulated Customer Data

| Dataset | Path | Description |
|---|---|---|
| `credit_risk_customers.csv` | `data/simulated/` | 12,000 synthetic customers generated in Notebook 04 using GOGLA benchmark distributions |
| `churn_customer_ledger.csv` | `data/simulated/` | 8,000 synthetic payment event records generated in Notebook 05 |

All simulated data is clearly labelled throughout the codebase. Findings derived from simulated data are illustrative of known sector patterns, not empirical results from a live portfolio.
