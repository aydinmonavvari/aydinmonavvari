# Graduate Portfolio Map

**Purpose.** Map each repository in this portfolio to the skill areas and graduate coursework it evidences, so that admissions committees and supervisors can quickly locate proof of specific competencies.

**Convention.** 🚩 = flagship. Each row cites concrete artifacts (modules, reports, figures) that exist in the linked repository.

---

## Map A · By graduate course / curriculum area

| Graduate course area | Primary evidence | Concrete artifacts |
|---|---|---|
| Statistics & Econometrics I–II | [finance-data-analysis-lab](https://github.com/aydinmonavvari/finance-data-analysis-lab), [m[macro-forecasting-lab](https://github.com/aydinmonavvari/macro-forecasting-lab) | JB/ADF/Ljung-Box diagnostics (`src/*/analytics`), SARIMA selection, Diebold-Mariano + Holm (`src/macro_forecasting_lab/evaluation.py`), rolling-origin design (Tashman 2000) |
| Time Series & Forecasting | macro-forecasting-lab, [dl-financial-time-series](https://github.com/aydinmonavvari/dl-financial-time-series) | 16 figures incl. backtest diagnostics; walk-forward folds + embargo; DM test tables in `reports/` |
| Empirical Asset Pricing / Investments | finance-data-analysis-lab, [portfolio-optimization-lab](https://github.com/aydinmonavvari/portfolio-optimization-lab) | Risk/return & drawdown analytics; efficient-frontier code; OOS net-of-costs backtests; 1/n replication (DeMiguel et al. 2009) |
| Financial Machine Learning | [m[ml-market-prediction-study](https://github.com/aydinmonavvari/ml-market-prediction-study), dl-financial-time-series | Walk-forward protocol (Lopez de Prado-style embargo), McNemar + Holm, permutation control, no-signal leakage control |
| Credit Risk & Banking | [credit-risk-modeling](https://github.com/aydinmonavvari/credit-risk-modeling) | PD models, calibration curves, cost-based thresholds, KS statistic, fairness diagnostics (`reports/`) |
| Fraud / AML Analytics | [fraud-anomaly-detection](https://github.com/aydinmonavvari/fraud-anomaly-detection) | PR-AUC-first evaluation, Isolation Forest vs RF, precision@k lift tables |
| Risk Management | portfolio-optimization-lab, 🚩 [finscope-ai-research](https://github.com/aydinmonavvari/finscope-ai-research) | Historical/Gaussian VaR & ES modules, drawdown reports, `fig08_var_es.png` |
| NLP for Finance | [financial-nlp-sentiment](https://github.com/aydinmonavvari/financial-nlp-sentiment) | PhraseBank benchmark, FinBERT vs lexicon/embedding baselines, McNemar test |
| LLM / RAG Systems for Research | [fin-rag-research-assistant](https://github.com/aydinmonavvari/fin-rag-research-assistant) | BM25/dense/RRF retrievers, gold-verified QA set, refusal policy + failure analysis, hallucination documentation |
| Data Engineering & Reproducibility | All 10 repositories | CI workflows, 300+ offline tests, provenance JSON, deterministic chunk/seed logic, one-command pipelines |

## Map B · By method → repository → result

| Method | Where implemented | Real committed result |
|---|---|---|
| ARIMA/SARIMA with rolling-origin eval | macro-forecasting-lab | Inflation h=1 best RMSE 0.246 (not significant after Holm) |
| Diebold-Mariano comparative testing | macro-forecasting-lab; finscope-ai-research | Unemployment h=12: nothing beats seasonal-naive (p>0.59); inflation: OLS/ridge significantly worse |
| GBM / XGBoost classification | ml-market-prediction-study; credit-risk-modeling | No SPY edge (AUC 0.502); PD ROC-AUC 0.778 |
| Platt/isotonic calibration | credit-risk-modeling | Brier barely moved — instructive null on ranking metrics |
| Risk parity (cyclical coord. descent) | portfolio-optimization-lab | OOS Sharpe 0.975 < 1/n 1.006 |
| Mean-variance SLSQP + tangency | portfolio-optimization-lab; finscope-ai-research | Tangency fallback in 31/31 OOS folds (flagship) |
| LSTM / GRU / CNN / Transformer | dl-financial-time-series | All AUC ≤ 0.50 (honest null, leak-free control) |
| FinBERT inference + classical NLP baselines | financial-nlp-sentiment | Macro-F1 0.865 vs 0.733 (McNemar p=2.3e-07) |
| BM25 / dense / RRF hybrid retrieval | fin-rag-research-assistant | Recall@5: 1.00 / 0.20 / 0.45 |
| Citation-grounded generation + refusal | fin-rag-research-assistant | Citations 8/8 valid; groundedness 0.035; refusal probes 0/2 |
| Historical & Gaussian VaR/ES | finscope-ai-research | e.g. equal-weight monthly VaR95 7.9%, ES95 9.2% |

## Map C · Research-integrity evidence (thesis-ready habits)

| Habit | Where demonstrated |
|---|---|
| Null results reported as results | ml-market-prediction-study; dl-financial-time-series; calibration null in credit-risk-modeling |
| Multiple-testing caution (Holm) | macro-forecasting-lab; ml-market-prediction-study |
| Leakage controls with positive proof | no-signal control (dl-financial-time-series); permutation control (ml-market-prediction-study) |
| Transaction costs in backtests | portfolio-optimization-lab; ml-market-prediction-study; finscope-ai-research |
| Data provenance & documented pivots | fin-rag-research-assistant (SEC 403 → Beige Book pivot, in code + report) |
| Cautious claims & explicit disclaimers | every README §1/§14 and research report §Discussion/Limitations |

## Map D · Suggested reading paths for reviewers

- **10-minute path:** finscope-ai-research README → its `reports/research_brief.md` → ml-market-prediction-study README §12–13.
- **30-minute path:** the above + fin-rag-research-assistant `docs/research_report.md` + financial-nlp-sentiment README §12.
- **Deep dive (econometrics):** macro-forecasting-lab `docs/research_report.md` then its `reports/` tables and DM-test code.
