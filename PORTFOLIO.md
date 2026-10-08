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
**Headline:** excess kurtosis 4.6–13.7 and JB rejection for all 8 series; log prices non-stationary while log returns are stationary; Ljung-Box(20) significant for 7/8 series. AAPL Sharpe 0.95 (rf=0), SPY 0.82. **43 tests, CI green.**

### 02 · macro-forecasting-lab
US CPI inflation and unemployment forecasting from FRED (rolling-origin evaluation, step 3, Tashman 2000; SARIMA/OLS/GBM/naive baselines; Diebold-Mariano tests with Holm correction).
**Headline:** results are horizon-dependent — inflation h=1 SARIMA best (RMSE 0.246, DM p=0.014, not significant after Holm); unemployment h=12 nothing beats seasonal-naive (all DM p>0.59); SARIMA catastrophically worse (MASE 2.46). **34 tests, CI green.**

### 03 · ml-market-prediction-study
Leakage-controlled walk-forward study: can classic ML find exploitable direction signal in SPY daily data (2010→2026, 4,193 rows, 8-fold walk-forward + 1-day embargo, holdout n=839)?
**Headline (null):** no model beats the majority baseline; best holdout ROC-AUC 0.5022 (RF); GBM significantly *worse* (McNemar, Holm p=0.011); permutation control confirms no leakage; best strategy +59.5% vs buy&hold +92.7% after 10 bps costs. **30 tests, CI green.**

### 04 · portfolio-optimization-lab
Mean-variance optimization (SLSQP with documented numerical fixes), risk parity via cyclical coordinate descent, closed-form tangency with frontier scan; walk-forward OOS backtest net of 10 bps.
**Headline:** equal-weight wins OOS (Sharpe 1.006) over risk parity (0.975), max-Sharpe (0.876, with 1.85% cumulative costs) and min-variance (0.696) — an in-repo replication of the 1/n result of DeMiguel et al. (2009). Tangency infeasibility handled with a documented min-variance fallback. **Tests green, CI green.**

### 05 · credit-risk-modeling
Probability-of-default modeling on UCI credit default (30,000 rows, 22.12% default rate): three-way split (train/calibration/untouched test), GBM vs logistic, Platt/isotonic calibration, cost-based thresholding (FN=5×FP), fairness diagnostics (SEX excluded from features).
**Headline:** GBM ROC-AUC 0.778, PR-AUC 0.558, KS 0.416; cost-optimal thresholds 0.16–0.20; calibration left ranking metrics essentially unchanged (instructive null); equal-opportunity difference 0.009. **Tests green, CI green.**

### 06 · fraud-anomaly-detection
Fraud/anomaly detection under extreme class imbalance, with an integrity-first data pattern: a seeded synthetic generator with labeled 15% "stealth" fraud (tuned so perfect detection is impossible) plus a documented user-side Kaggle acquisition path (ULB dataset) — zero fabricated real-data claims.
**Headline:** RF PR-AUC 0.728 vs Isolation Forest 0.130, while ROC-AUC sits at 0.91–0.98 for both — the ROC-misleads-under-imbalance lesson in one table; precision@1% = 88× base-rate lift. **Tests green, CI green.**

### 07 · dl-financial-time-series
Small deep architectures (LSTM, GRU, temporal CNN, tiny Transformer; 4.5k–9k parameters) for next-day SPY direction, strict walk-forward (3 expanding folds, 1-day embargo), vs classical baselines.
**Headline (null):** every model's pooled OOS ROC-AUC ≤ 0.50; best accuracy inside the majority baseline's Wilson CI [0.517, 0.569]; a no-signal control (pure-noise features) confirms the harness is leak-free; transformer backtest +101.5% vs buy&hold +97.8% is within noise. **34 tests, CI green.**

### 08 · financial-nlp-sentiment
Benchmark of financial sentiment classification on the Financial PhraseBank (Malo et al. 2014; 4,838 unique sentences, 59.4% neutral): VADER lexicon, TF-IDF+LogReg, frozen MiniLM embeddings+LogReg, and FinBERT (inference only, overlap caveat documented).
**Headline:** FinBERT 0.870 accuracy / 0.865 macro-F1; MiniLM+LR 0.777 / 0.733; TF-IDF 0.756 / 0.699; VADER 0.587 / 0.500; McNemar FinBERT-vs-MiniLM p=2.285e-07. **27 tests, CI green.**

### 09 · fin-rag-research-assistant
Retrieval-augmented QA over 26 Federal Reserve Beige Book documents (public domain; documented pivot from SEC EDGAR after persistent 403 blocking): BM25 vs dense (MiniLM) vs hybrid RRF, a 20-question gold-verified QA set, refusal threshold analysis, and citation-grounded generation with Qwen2.5-0.5B.
**Headline:** BM25 Recall@5 1.00 / MRR 0.847 vs dense 0.20 / hybrid 0.45; refusal τ=0.369 gave 0% false refusals but refused 0/2 out-of-scope probes; generation citations 8/8 valid yet groundedness F1 0.035 with a documented hallucination — grounding and refusal fail independently and must be measured. **56 tests, CI green.**

### 10 · finscope-ai-research (flagship)
A modular research workbench unifying the portfolio's methods on one codebase: ingestion (yfinance/FRED) → diagnostics → rolling-origin inflation forecasting study → portfolio construction → VaR/ES risk reporting → evidence-first research brief with mandatory limitations section.
**Headline:** seasonal-naive beats OLS (DM p=0.004) and ridge (p=0.005) on 12-month CPI inflation — direction-aware honest verdict; tangency fallback triggered in 31/31 OOS folds (estimation error as first-class finding); min-var and max-Sharpe OOS Sharpe 1.36 net of costs; VaR/ES tables per portfolio. **48 tests, CI green.**

## 4 · What the portfolio demonstrates (for admissions)

| Skill area | Evidence |
|---|---|
| Statistics & econometrics | 01 (diagnostics), 02 (SARIMA, DM tests), 10 |
| Machine learning methodology | 03, 05, 06 (leakage control, calibration, imbalance) |
| Deep learning | 07 (four architectures, honest null) |
| Optimization & portfolio theory | 04, 10 (numerical robustness, cost-aware OOS) |
| Risk management | 04, 10 (VaR/ES, drawdowns) |
| NLP & LLM systems | 08, 09 (benchmarks, RAG, refusal measurement) |
| Software engineering | All: offline test suites (300+ tests total), ruff, CI, provenance |
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
