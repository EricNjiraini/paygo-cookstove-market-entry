# Data Dictionary

Field definitions for all processed and simulated datasets.

---

## `data/processed/country_comparison.csv`

| Field | Type | Description |
|---|---|---|
| `iso` | str | ISO 3166-1 alpha-2 country code |
| `country` | str | Country name |
| `financial_account_pct` | float | % of adults (15+) with a formal financial account (Findex 2021) |
| `bank_branches_per_100k` | float | Bank branches per 100,000 adults (World Bank) |
| `mobile_subs_per_100` | float | Mobile cellular subscriptions per 100 people |
| `clean_fuel_access_pct` | float | % of population using clean fuels for cooking (World Bank EG.CFT.ACCS.ZS) |
| `urban_pop_pct` | float | Urban population as % of total (World Bank) |
| `clean_cooking_deficit_pct` | float | Derived: 100 - clean_fuel_access_pct |
| `mai_composite` | int | Lighting Global PAYGo MAI composite score (0–100) |
| `mai_market_size` | int | LG MAI sub-dimension: market size |
| `mai_fin_infra` | int | LG MAI sub-dimension: financial infrastructure |
| `mai_mobile_money` | int | LG MAI sub-dimension: mobile money |
| `mai_regulatory` | int | LG MAI sub-dimension: regulatory environment |

---

## `data/simulated/credit_risk_customers.csv`

| Field | Type | Description |
|---|---|---|
| `customer_id` | str | Synthetic customer identifier (CUS000001 format) |
| `downpayment_pct` | float | Initial payment as a fraction of total device cost (0–0.35) |
| `contract_months` | int | Contract duration in months (12, 18, 24, 30, or 36) |
| `is_urban` | int | 1 = urban registration, 0 = rural |
| `gender_female_hh` | int | 1 = female-headed household, 0 = male-headed |
| `age_head` | int | Age of household head in years |
| `wealth_index` | float | Standardised wealth index (proxy from Meta RWI; mean=0, sd=1) |
| `mobile_money_freq` | int | Mobile money usage frequency: 0=none, 1=monthly, 2=weekly, 3=daily |
| `prior_credit` | int | 1 = prior formal credit history, 0 = none |
| `household_size` | int | Number of household members |
| `defaulted` | int | **Target variable**: 1 = defaulted on instalments, 0 = repaid |

---

## `data/simulated/churn_customer_ledger.csv`

| Field | Type | Description |
|---|---|---|
| `customer_id` | str | Synthetic customer identifier |
| `duration_days` | int | Observed days active (either to churn event or to end of contract) |
| `churned` | int | **Survival event**: 1 = churned before contract end, 0 = censored (completed or still active) |
| `downpayment_pct` | float | Initial payment fraction (same definition as credit risk dataset) |
| `contract_months` | int | Contract duration in months |
| `is_urban` | int | 1 = urban, 0 = rural |
| `wealth_index` | float | Standardised wealth index |
| `mobile_money_freq` | int | Mobile money usage frequency (0–3) |
| `days_since_last_pmt` | int | Days since most recent payment at time of snapshot |
| `payment_regularity` | float | Standard deviation of inter-payment intervals (higher = more irregular) |
| `pmt_vs_schedule` | float | Ratio of actual cumulative payments to expected schedule (1.0 = on track) |
| `days_locked` | int | Cumulative days product was locked due to missed payments |
| `churn_risk_score` | float | Predicted probability of churning within 30 days (output of Module 3 model) |
| `risk_band` | str | Categorical risk band: Low / Medium / High / Critical |

---

## `data/raw/gogla_benchmarks.json`

| Field | Description |
|---|---|
| `sector_avg_repayment_rate` | Sector average: fraction of financed amount recovered (0.72 = 72%) |
| `sector_default_rate` | Implied default rate = 1 - repayment rate (0.28) |
| `best_quartile_repayment` | Top performing firms: 90% repayment rate |
| `worst_quartile_repayment` | Bottom performing firms: 58% repayment rate |
| `downpayment_threshold_high` | Threshold above which repayment significantly improves (10%) |
| `downpayment_threshold_low` | Threshold below which repayment is worst (5%) |
| `typical_contract_months_range` | Typical contract duration range [12, 36] months |
| `lockout_trigger_days` | Consecutive missed days before product lockout (3 days) |
