# 👋 Aydin Monavvari — Quantitative Finance Research Portfolio

**BSc Financial Management (final year) · Building an honest, reproducible Python research portfolio for graduate study in quantitative finance / financial engineering / econometrics.**

I build small, end-to-end research studies on **real public data** — each repository is a complete cycle: data acquisition with provenance → methodology → offline-tested code → real run with committed results → cautious interpretation with explicit limitations. I care as much about **documenting what doesn't work** as about positive results, because that is what honest research looks like.

> ⚠️ **Scope.** Everything here is educational research — a record of methods I studied and evaluated on public data. Nothing is investment advice, nothing is a production trading system, and I make no claim that any method here "beats the market." Several of my headline results are honest null results.

---

## 🔭 The portfolio (10 repositories)

| # | Repository | Focus | Headline (real, committed result) |
|---|-----------|-------|-----------------------------------|
| 01 | [finance-data-analysis-lab](https://github.com/aydinmonavvari/finance-data-analysis-lab) | Returns/risk analytics & diagnostics on 7 large caps + SPY (2018–2026) | JB rejects normality for all 8 series; log returns stationary (ADF); SPY Sharpe 0.82 |
| 02 | [m[macro-forecasting-lab](https://github.com/aydinmonavvari/macro-forecasting-lab) | US inflation & unemployment forecasting (FRED), rolling-origin evaluation | Nothing beats seasonal-naive for unemployment at h=12 (all DM p>0.59) — reported honestly |
| 03 | [m[ml-market-prediction-study](https://github.com/aydinmonavvari/ml-market-prediction-study) | Leakage-free walk-forward ML on SPY direction (2010–2026) | **Null result:** no model beats the majority baseline (best ROC-AUC 0.502); GBM significantly *worse* (Holm p=0.011) |
| 04 | [portfolio-optimization-lab](https://github.com/aydinmonavvari/portfolio-optimization-lab) | Mean-variance, risk parity, tangency; walk-forward OOS net of costs | Naive 1/n wins OOS (Sharpe 1.006 vs 0.876 max-Sharpe) — replicates DeMiguel et al. (2009) |
| 05 | [credit-risk-modeling](https://github.com/aydinmonavvari/credit-risk-modeling) | Probability of default (UCI, 30k rows): calibration, cost-based thresholds, fairness | GBM ROC-AUC 0.778 / KS 0.416; calibration is an instructive null on ranking metrics |
| 06 | [fraud-anomaly-detection](https://github.com/aydinmonavvari/fraud-anomaly-detection) | Fraud detection under extreme imbalance (seeded synthetic + documented Kaggle path) | ROC-AUC misleads under imbalance: all models 0.91–0.98 ROC but PR-AUC spans 5.6× |
| 07 | [dl-financial-time-series](https://github.com/aydinmonavvari/dl-financial-time-series) | LSTM/GRU/CNN/Transformer vs baselines, strict walk-forward | **Null result:** every AUC ≤ 0.50; no-signal control proves a leak-free harness |
| 08 | [financial-nlp-sentiment](https://github.com/aydinmonavvari/financial-nlp-sentiment) | Financial PhraseBank benchmark: VADER → TF-IDF → embeddings → FinBERT | FinBERT 0.865 macro-F1 vs embeddings 0.733 (McNemar p=2.3e-07) |
| 09 | [fin-rag-research-assistant](https://github.com/aydinmonavvari/fin-rag-research-assistant) | RAG over Fed Beige Book: BM25 vs dense vs hybrid, grounded generation, refusal | BM25 Recall@5 1.00 vs dense 0.20; documented hallucination + refusal-failure findings |
| 10 | 🚩 [finscope-ai-research](https://github.com/aydinmonavvari/finscope-ai-research) | **Flagship workbench** unifying the portfolio's methods end-to-end | Seasonal-naive beats OLS/ridge on inflation (direction-aware DM); tangency falls back in 31/31 OOS folds |

Every repository ships with: offline test suite (30–56 tests), ruff-clean code, GitHub Actions CI, 23-section README, 13-section research report, real committed results (`reports/`), figures, `CITATION.cff`, MIT license.

---

## 🚩 Flagship: finscope-ai-research

The capstone that ties the portfolio together: a modular research workbench running the full cycle — ingestion (yfinance/FRED) → diagnostics → forecasting study → portfolio construction → VaR/ES risk reporting → an evidence-first research brief with a mandatory limitations section. It is explicitly **not** a trading system: it is a harness for *evaluating methods* and *reporting findings honestly*.

## 🧭 Methods I have implemented and evaluated

- **Statistics & econometrics:** Jarque-Bera, ADF/KPSS, Ljung-Box, OLS/ridge, ARIMA/SARIMA, Diebold-Mariano with multiple-testing correction (Holm), rolling-origin backtesting (Tashman)
- **Machine learning:** logistic/ridge/GBM/XGBoost/random forests, calibration (Platt/isotonic), cost-sensitive thresholds, permutation importance, McNemar tests
- **Deep learning:** LSTM, GRU, temporal CNN, small Transformer encoders (CPU-reproducible), early stopping, no-leakage walk-forward
- **Portfolio theory:** mean-variance (SLSQP), risk parity (cyclical coordinate descent), tangency + fallbacks, Ledoit-Wolf shrinkage, transaction-cost-aware backtests
- **Risk:** historical/Gaussian VaR & ES, drawdown analysis
- **NLP/LLM:** FinBERT, sentence embeddings, VADER, RAG (BM25/dense/RRF hybrid), citation-grounded generation, refusal policies, hallucination measurement
- **Engineering:** pytest offline suites, ruff, GitHub Actions CI, deterministic pipelines, data provenance records, reproducible figures/reports

## 🔬 Research integrity rules I hold myself to

1. **No fabricated data, results, or references** — every number in a README comes from a committed pipeline run.
2. **Cautious language** — "evaluating whether…", "no reliable edge found", never "AI predicts the market".
3. **Strict chronology** in time-series evaluation (no shuffling; embargoed walk-forward) and leakage controls verified by no-signal controls.
4. **Costs and limitations included** — transaction costs, multiple-testing caveats, proxy-metric warnings.
5. **Real data with provenance** (FRED, Yahoo Finance, SEC/EDGAR, World Bank, UCI, Federal Reserve) — and documented pivots when sources become unavailable.

## 📄 Documents

- **[PORTFOLIO.md](https://github.com/aydinmonavvari/aydinmonavvari/blob/main/PORTFOLIO.md)** — full portfolio narrative with per-repo summaries and verification instructions
- **[docs/graduate-portfolio-map.md](https://github.com/aydinmonavvari/aydinmonavvari/blob/main/docs/graduate-portfolio-map.md)** — maps each repo to graduate-program skill areas
- **[docs/self-assessment.md](https://github.com/aydinmonavvari/aydinmonavvari/blob/main/docs/self-assessment.md)** — rubric-based self-assessment of the portfolio

## 📫 Contact

- GitHub: [@aydinmonavvari](https://github.com/aydinmonavvari) (preferred contact: GitHub issues on any research repo)
- Email: via GitHub noreply `245710241+aydinmonavvari@users.noreply.github.com`

---

*© 2026 Aydin Monavvari · Code: MIT · Documents: CC BY 4.0*
