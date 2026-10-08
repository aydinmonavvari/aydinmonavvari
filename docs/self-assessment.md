# Portfolio Self-Assessment

**Purpose.** A rubric-based self-assessment of this portfolio, written with the same honesty standards the portfolio itself follows. Scores are justified with evidence links; weaknesses are listed, not hidden.

**Scale.** 0 = absent · 1 = attempted · 2 = functional · 3 = solid · 4 = strong · 5 = defensible-before-a-committee.

---

## A · Technical depth & breadth

| Criterion | Score | Evidence & justification |
|---|---:|---|
| Statistics/econometrics coverage | 5 | Diagnostics (01), SARIMA + DM/Holm (02), rolling-origin design; every claim tied to committed tables |
| ML methodology | 5 | Leakage-free walk-forward protocol, calibration, imbalance handling, McNemar testing (03, 05, 06, 08) |
| Deep learning | 3 | Four architectures implemented and honestly evaluated on CPU budget (07); deliberately small-scale |
| Optimization & portfolio theory | 4 | SLSQP robustness fixes, risk parity via CCD, tangency + documented fallback (04, 10) |
| Risk management | 4 | Historical/Gaussian VaR/ES, drawdowns (04, 10) |
| NLP / LLM | 4 | FinBERT benchmark (08); full RAG evaluation incl. refusal failure measurement (09) |
| Data engineering | 4 | Cached/provenance-recorded ingestion, deterministic pipelines, idempotent stages |
| **Subtotal** | **29/35** | |

## B · Research integrity

| Criterion | Score | Evidence & justification |
|---|---:|---|
| No fabricated data/results/references | 5 | Every number traceable to `reports/` outputs; reference lists limited to verifiable classics |
| Honest null results | 5 | Three deliberate null-result studies with leakage controls that make the null credible (permutation control + leakage-mutation test in 03, no-signal control in 07, calibration null in 05) |
| Cautious claims language | 5 | No "predicts the market" claims anywhere; disclaimers in every README §1 and report |
| Multiple-testing & uncertainty care | 4 | Holm corrections, Wilson CIs, DM tests; no p-hacking framing |
| Cost/bias inclusion | 4 | 10 bps costs in all backtests; fairness diagnostics in 05; proxy-metric warnings in 09 |
| Data provenance & pivots | 4 | Provenance JSONs; SEC→Beige Book pivot documented in code + report |
| **Subtotal** | **27/30** | |

## C · Software engineering & reproducibility

| Criterion | Score | Evidence & justification |
|---|---:|---|
| Tests | 5 | 357 offline test functions across 10 repos (7–79 per repository; recounted during the v1.0.0 remediation pass); heavy tests skip cleanly in CI |
| CI/CD | 5 | GitHub Actions on every repo (light offline suites; heavy-model jobs documented per-repo) |
| Code quality | 4 | ruff-clean everywhere; conventional commits (7–17 per repo; verified range) |
| Reproducibility | 5 | One-command pipelines, fixed seeds, committed metrics/figures, CITATION.cff |
| Documentation depth | 5 | 22–23-section READMEs + 13-section research reports per repo |
| **Subtotal** | **24/25** | |

## D · Portfolio-level narrative

| Criterion | Score | Evidence & justification |
|---|---:|---|
| Coherent build-up | 4 | Waves 1→4: foundations → decision methods → modern methods → integration (PORTFOLIO.md §2) |
| Flagship integration | 4 | finscope-ai-research re-implements the portfolio's methods in one workbench with an honest research brief |
| Fit to graduate study | 4 | Maps directly to quant finance/FE/econometrics curricula (graduate-portfolio-map.md) |
| **Subtotal** | **12/15** | |

## Overall

| Section | Score | Cap |
|---|---:|---:|
| A · Technical | 29 | 35 |
| B · Integrity | 27 | 30 |
| C · Engineering | 24 | 25 |
| D · Narrative | 12 | 15 |
| **Total** | **92 / 105** | |

## Honest weaknesses (self-identified)

1. **Scale.** All market studies are small-universe, daily-frequency, CPU-budget studies. No high-frequency data, no multi-asset cross-sectional factor work, no GPU-scale training. A reviewer may reasonably ask for both.
2. **Statistical power.** Several null results rest on one asset and one sample split scheme; more assets/folds would strengthen them.
3. **Human evaluation.** The RAG study has no human faithfulness panel; all generation metrics are documented proxies.
4. **Real fraud data.** The committed fraud results are synthetic (license-driven); the Kaggle path is documented but user-side.
5. **Theory.** The portfolio is empirical; there is no novel theoretical contribution, and it does not claim one.
6. **Single-author confirmation bias.** QA sets and evaluation choices were authored by one person; an external reviewer pass is future work.

## Improvement roadmap (post-application)

- Cross-sectional factor study (multi-asset, Fama-MacBeth style) on real data.
- Point-in-time fundamentals via SEC EDGAR from a permitted egress environment.
- Human evaluation panel for RAG faithfulness; cross-encoder re-ranking.
- GPU-scale replication of the DL null result with larger architectures and ensembles.
- External code review pass on the flagship workbench.

*Self-assessed by Aydin Monavvari, October 2026.*
