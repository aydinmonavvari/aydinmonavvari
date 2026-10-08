# PORTFOLIO.md — Research Portfolio of Aydin Monavvari

**Purpose.** This document is the narrative companion to my 10-repository quantitative finance research portfolio. It explains what each repository studies, what was actually found (all numbers below are committed pipeline outputs, not aspirations), how the repositories build on each other, and how any reviewer can verify every claim locally.

**Who this is for.** Graduate admissions committees, potential research supervisors, and reviewers who want to judge my preparation for graduate study in quantitative finance, financial engineering, econometrics, or financial data science.

**Timeline.** Built October 2026 (final year of BSc in Financial Management). All repositories are public, MIT-licensed, CI-tested, and pinned to real data sources with documented provenance.

---

## 1 · Design principles

The portfolio was designed around five principles, applied uniformly:

1. **Real data only.** Every study runs on public, attributable data: Yahoo Finance daily bars, FRED CSV series, World Bank indicators, UCI ML repository datasets, the Financial PhraseBank (Malo et al. 2014), and Federal Reserve Beige Book releases. Synthetic data appears only where it is labeled synthetic (fraud detection, unit-test fixtures).
2. **Complete research cycle per repository.** Data acquisition (cached, provenance-recorded) → methodology → offline test suite → a real executed run with committed outputs (`reports/`, `figures/`) → cautious interpretation + explicit limitations.
3. **Honesty about results.** Negative and null results are reported as prominently as positive ones. Three of the ten studies are deliberate null-result studies (see §3); the value lies in the *demonstrated evaluation hygiene* that makes the null credible.
4. **Reproducibility.** Deterministic pipelines, fixed seeds, one-command entry points, CI on every push, committed metrics/figures, `CITATION.cff` in every repository.
5. **Cautious academic language.** No claim anywhere states or implies that a method "predicts the market" or is production-ready. Trading-system framing is explicitly disclaimed.

## 2 · The repository chain

The repositories are ordered so that each wave builds on the skills and artifacts of the previous one:

```
WAVE 1 — Foundations
  01 finance-data-analysis-lab      → returns/risk/diagnostics layer
  02 macro-forecasting-lab          → econometric forecasting & DM evaluation
  03 ml-market-prediction-study     → leakage-free ML evaluation protocol
WAVE 2 — Decision-oriented methods
  04 portfolio-optimization-lab     → optimization + cost-aware backtesting
  05 credit-risk-modeling           → classification, calibration, fairness
  06 fraud-anomaly-detection        → imbalance, unsupervised baselines
WAVE 3 — Modern methods
  07 dl-financial-time-series       → deep learning under strict protocol
  08 financial-nlp-sentiment        → domain NLP benchmark
  09 fin-rag-research-assistant     → retrieval + grounded generation + refusal
WAVE 4 — Integration
  10 finscope-ai-research           → flagship workbench unifying 01–09 methods
```

## 3 · Repository summaries (real results)

### 01 · finance-data-analysis-lab
Descriptive quantitative analytics over 7 large caps + SPY (2018-01-02 → 2026-10-07, 2,203 trading days, Yahoo Finance): return distributions, annualized risk/return, drawdowns, normality (Jarque-Bera), stationarity (ADF), autocorrelation (Ljung-Box).
**Headline:** excess kurtosis 4.6–13.7 and JB rejection for all 8 series; log prices non-stationary while log returns are stationary; Ljung-Box(20) significant for 7/8 series. AAPL Sharpe 0.95 (rf=0), SPY 0.82. **46 tests, CI green.**

### 02 · macro-forecasting-lab
US CPI inflation and unemployment forecasting from FRED (rolling-origin evaluation, step 3, Tashman 2000; SARIMA/OLS/GBM/naive baselines; Diebold-Mariano tests with Holm correction).
**Headline:** results are horizon-dependent — under the corrected (h−1) HAC bandwidth, all 7 non-benchmark models are significantly better than seasonal-naive for inflation h=1 (raw DM p ≤ 0.00035, surviving the 28-comparison family correction at threshold ≈ 0.0018; the lag-1 bandwidth is reported alongside as a sensitivity and does not survive); at unemployment h=12 no model significantly beats seasonal-naive and OLS is significantly *worse* (raw p = 0.030 full window / 0.013 ex-Covid); SARIMA is worst by RMSE (5.13) and random forest worst by MASE (2.66). **48 tests, CI green.**

### 03 · ml-market-prediction-study
Leakage-controlled walk-forward study: can classic ML find exploitable direction signal in SPY daily data (2010→2026, 4,193 rows, 8-fold walk-forward + 1-day embargo, holdout n=839)?
**Headline (null):** no model beats the majority baseline; best holdout ROC-AUC 0.5022 (RF), with stationary-bootstrap 95% CIs that all include 0.5; GBM significantly *worse* (McNemar, Holm p=0.011); permutation control and a leakage-mutation test sanity-check the harness (controls, not proofs); best strategy +59.5% vs buy&hold +92.7% after 10 bps costs. **34 tests, CI green.**

### 04 · portfolio-optimization-lab
Mean-variance optimization (SLSQP with documented numerical fixes), risk parity via cyclical coordinate descent, closed-form tangency with frontier scan; walk-forward OOS backtest net of 10 bps.
**Headline:** equal-weight wins OOS net of 10 bps costs (net Sharpe 1.005; gross 1.006) over risk parity (0.972), max-Sharpe (0.957, with 1.86% cumulative costs) and min-variance (0.691) — an in-repo replication of the 1/n result of DeMiguel et al. (2009), over 1,890 OOS days and 30 quarterly rebalances. Tangency infeasibility handled with a documented min-variance fallback. **30 tests green, CI green.**

### 05 · credit-risk-modeling
Probability-of-default modeling on UCI credit default (30,000 rows, 22.12% default rate): three-way split (train/calibration/untouched test), GBM vs logistic, Platt/isotonic calibration, cost-based thresholding (FN=5×FP), fairness diagnostics (SEX excluded from features).
**Headline:** GBM ROC-AUC 0.778 (raw model), PR-AUC 0.558 (raw), KS 0.416 (calibrated; raw-model KS 0.419); cost-optimal thresholds 0.16–0.20; calibration left ranking metrics essentially unchanged (instructive null); equal-opportunity difference 0.009. **7 tests green, CI green.**

### 06 · fraud-anomaly-detection
Fraud/anomaly detection under extreme class imbalance, with an integrity-first data pattern: a seeded synthetic generator (60,000 rows, 102 frauds ≈ 0.17% base rate; 15% of frauds are "stealth" rows redrawn from the legitimate distribution so that no univariate signal exists — detectability capped by design) plus a documented user-side Kaggle acquisition path (ULB dataset) — zero fabricated real-data claims.
**Headline:** RF PR-AUC 0.614 vs Isolation Forest 0.095, while ROC-AUC sits at 0.87–0.94 for all models — the ROC-misleads-under-imbalance lesson in one table; precision@1% of 0.139 is ≈81× the 0.17% base rate; the cost-optimal threshold (0.13) is selected on a dedicated validation split, so the test set is touched once. **10 tests green, CI green.**

### 07 · dl-financial-time-series
Small deep architectures (LSTM, GRU, temporal CNN, tiny Transformer; 4.5k–9k parameters) for next-day SPY direction, strict walk-forward (3 expanding folds, 1-day embargo), vs classical baselines.
**Headline (null):** every model's pooled OOS ROC-AUC ≤ 0.50; best accuracy inside the majority baseline's Wilson CI [0.517, 0.569]; a no-signal control (pure-noise features) confirms the harness is leak-free; transformer backtest +101.5% vs buy&hold +97.8% is within noise. **34 tests, CI green.**

### 08 · financial-nlp-sentiment
Benchmark of financial sentiment classification on the Financial PhraseBank (Malo et al. 2014; 4,838 unique sentences, 59.4% neutral): VADER lexicon, TF-IDF+LogReg, frozen MiniLM embeddings+LogReg, and FinBERT (inference only, overlap caveat documented).
**Headline:** FinBERT 0.870 accuracy / 0.865 macro-F1; MiniLM+LR 0.777 / 0.733; TF-IDF 0.756 / 0.699; VADER 0.587 / 0.500; McNemar FinBERT-vs-MiniLM p=2.285e-07. **30 tests, CI green.**

### 09 · fin-rag-research-assistant
Retrieval-augmented QA over 26 Federal Reserve Beige Book documents (public domain; documented pivot from SEC EDGAR after persistent 403 blocking; SHA-256 corpus manifest): BM25 vs dense (MiniLM) vs hybrid RRF over a two-part self-authored QA design — SET A (20 dev questions) for τ selection, SET B (12 held-out paraphrased questions) for the headline — plus refusal-threshold analysis and citation-grounded generation with Qwen2.5-0.5B.
**Headline (held-out SET B):** BM25 Recall@5 0.833 / MRR 0.586 vs dense 0.333 / hybrid 0.417 (dev SET A: BM25 1.00 / 0.847 — dev-only evaluation overstates retrieval quality); τ=0.369 selected on SET A generalized with 0% false refusals on held-out questions but refused 0/2 out-of-scope probes in both splits; generation citations existed 12/12 (0 fabricated) yet groundedness F1 0.020 (answer-precision 0.425) with 8/14 bare-citation answers and a documented hallucination — grounding and refusal fail independently and must be measured. **79 tests, CI green.**

### 10 · finscope-ai-research (flagship)
A modular research workbench unifying the portfolio's methods on one codebase: ingestion (yfinance/FRED) → diagnostics → rolling-origin inflation forecasting study → portfolio construction → VaR/ES risk reporting → evidence-first research brief with mandatory limitations section.
**Headline:** seasonal-naive beats OLS (DM p=0.004) and ridge (p=0.005) on 12-month CPI inflation (35 forecast origins) — direction-aware honest verdict; tangency fallback triggered in 31/31 OOS folds (estimation error as first-class finding); min-variance/max-Sharpe OOS Sharpe 1.36 net of costs (equal-weight 1.23) over 93 monthly OOS observations; equal-weight ES99 9.7%. **51 tests, CI green.**

## 4 · What the portfolio demonstrates (for admissions)

| Skill area | Evidence |
|---|---|
| Statistics & econometrics | 01 (diagnostics), 02 (SARIMA, DM tests), 10 |
| Machine learning methodology | 03, 05, 06 (leakage control, calibration, imbalance) |
| Deep learning | 07 (four architectures, honest null) |
| Optimization & portfolio theory | 04, 10 (numerical robustness, cost-aware OOS) |
| Risk management | 04, 10 (VaR/ES, drawdowns) |
| NLP & LLM systems | 08, 09 (benchmarks, RAG, refusal measurement) |
| Software engineering | All: offline test suites (357 test functions total; 7–79 per repository), ruff, CI, provenance |
| Research writing | All: 13-section research reports with real references |

## 5 · How to verify any claim

1. Open any repository → read `README.md` §12 (Results) — numbers must match `reports/`.
2. Run `pip install -e ".[dev]"` then `pytest tests/ -q` (offline) — CI badge shows the same on every push.
3. Heavy pipelines: `python scripts/run_study.py all` (or the repo's documented entry point) regenerates every figure and metric from cached/public data.
4. Git history shows the conventional-commit trail (`feat:`, `test:`, `docs:`, `fix:`, `ci:`) for every stage of each build.

## 6 · Known limitations (portfolio level)

- All market studies are single-asset or small-universe daily-frequency studies; conclusions are corpus- and asset-conditional.
- Deep learning studies use deliberately small CPU-budget models; the point is protocol honesty, not scale.
- The fraud study's real-data path (Kaggle ULB) is documented but user-side by design (license) — committed results are on labeled synthetic data, clearly labeled as such.
- The RAG study's QA set is a researcher-authored instrument, not a public benchmark (documented in-repo).
- The fin-rag corpus pivot (SEC 403 → Federal Reserve Beige Book) is documented transparently in code and reports.

## 7 · License & citation

- Code: MIT (per repository). Documents in this profile repository: CC BY 4.0.
- Cite any repository via its `CITATION.cff` (BibTeX blocks in each README §21).

— **Aydin Monavvari**, October 2026
