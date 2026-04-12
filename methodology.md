# Methodology Notes

Analytical decisions, assumptions, and design choices for each module.

---

## Module 1 — Market Sizing & Entry Prioritisation

### Customer Segmentation Framework
Follows the Clean Cooking Alliance (2022) segmentation:
- **Early adopters**: Electricity access, quality housing, high consumption. Targeted first.
- **Fast followers**: Bank account, formal employment or consistent income, can access credit products.
- **Secondary followers**: Limited financial inclusion; require different product design (e.g. agent-mediated payments, shorter contract windows).

### Country Scoring Weights
| Dimension | Weight | Rationale |
|---|---|---|
| Clean cooking access deficit | 25% | Quantifies the size of the addressable problem |
| Mobile money penetration | 25% | Essential for PayGo payment collection infrastructure |
| Financial inclusion | 20% | Determines credit product accessibility |
| LG MAI composite | 20% | Sector-specific maturity, regulation, and competitive landscape |
| Urban population share | 10% | Distribution, after-sales, and agent network logistics |

Weights are intentionally biased toward payment infrastructure (mobile money + financial inclusion = 45%) reflecting the operational reality that PayGo products are commercially unviable without reliable payment rails.

### Sub-National Heat Map
The Meta Relative Wealth Index (RWI) is used as a proxy for household ability to make the initial downpayment. RWI is spatially joined to admin-level shapefiles from GADM. County-level mean RWI is visualised as a choropleth map. This is a necessary simplification — a live deployment would use proprietary agent network coverage data.

---

## Module 2 — Credit Risk Scoring

### Feature Engineering
All features use information available at sign-up only (no transaction history). This reflects the cold-start constraint for new customer onboarding.

- `downpayment_pct` is the ratio of initial payment to total device cost — the single most predictive feature per GOGLA PERFORM benchmarks.
- `wealth_index` is derived from the Meta RWI grid cell containing the customer's registered location.
- `mobile_money_freq` is a proxy for financial behaviour regularity, encoded 0–3 (none/monthly/weekly/daily).
- `prior_credit` is a binary flag for any formal credit history (from FinAccess survey-based inference).

### Simulation Calibration
The synthetic default labels are generated from a logistic model whose intercept is set so that the base default rate ≈ 28% (matching the GOGLA sector average of 72% repayment). Feature coefficients are directionally consistent with published sector research:
- Higher downpayment → lower default (GOGLA PERFORM)
- Female household heads → better repayment (GOGLA PERFORM, CGAP)
- Mobile money usage → proxy for financial capability and reliability

### Model Selection
Three models are compared (Logistic Regression, Random Forest, XGBoost). XGBoost is expected to outperform on AUC-ROC given non-linear interaction effects (e.g. downpayment × urban status). Logistic Regression is retained as the interpretable baseline for regulatory and compliance contexts.

Evaluation uses AUC-ROC (discrimination) and Average Precision / Precision-Recall (calibration for imbalanced outcome), with 80/20 stratified train/test split.

---

## Module 3 — Churn Prediction

### Churn Definition
A customer is flagged as churned if they miss 7+ consecutive payment days, triggering a product lockout. This is operationally meaningful — it's the threshold at which a field agent intervention becomes urgent.

### Survival Analysis Choice
Kaplan-Meier provides non-parametric survival curves stratified by key groups (useful for stakeholder communication). Cox Proportional Hazard extends this to estimate adjusted hazard ratios per feature. Neither requires distributional assumptions on time-to-churn.

### 30-Day Classifier
Complements survival analysis with an operational trigger: a binary yes/no flag for "will this customer churn in the next 30 days". This is the format most useful for a call centre or field agent priority queue.

### Real-World Deployment Note
In production, the churn model would be retrained weekly on the live payment ledger. The features `days_since_last_payment`, `days_locked`, and `payment_vs_schedule_ratio` are real-time signals computed from transaction data — which is why this module requires simulated data in a portfolio context.

---

## General Assumptions & Limitations

1. **Simulated transaction data**: All customer-level analysis in Modules 2 & 3 uses synthetic data. Results directionally replicate known sector patterns but should not be interpreted as empirical portfolio findings.
2. **Temporal scope**: World Bank and GSMA indicators use the most recent available year (2021–2023). Country rankings could shift with updated data.
3. **Market maturity scores**: Lighting Global MAI scores encoded here are illustrative placeholders. Actual values must be read from the downloaded report.
4. **Spatial resolution**: Sub-national analysis uses admin-1 (county/region) level — too coarse for targeting individual villages. A deployment-grade analysis would use admin-2 with agent network coverage layers.
