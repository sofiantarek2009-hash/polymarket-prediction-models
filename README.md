# Polymarket Prediction Models (Public Showcase)

> **Public Runnable Proof Gist:** [**Execute & Inspect Live Proof Gist ->**](https://gist.github.com/sofiantarek2009-hash/9b62a1b39b175a7574452c393e16f71f)  
> **Visibility Policy:** This public showcase publishes the reproducible calibration, walk-forward IRLS, and scoring harness. Proprietary market feeds, alpha features, and ~78% historical contract-model weights remain **private**.

---

## Run the Reproducible Proof Locally (Zero Dependencies)

Requires **Python 3.9+ standard library only**:

```bash
gh gist clone 9b62a1b39b175a7574452c393e16f71f polymarket-proof
cd polymarket-proof
python3 polymarket_stat_model.py --test
```

## Verified Calibration & Walk-Forward Benchmark (`polymarket_stat_model.py --test`)

Evaluates a damped Newton-Raphson **IRLS L2 Logistic Classifier** with **Out-of-Fold Platt Scaling** across a chronological 600-contract binary CLOB order-book sequence (`360` training / 4-fold OOF calibration -> `240` unseen out-of-sample contracts):

- **IRLS Convergence:** `iters = 6`, `||grad||_inf = 2.71e-12`
- **Unseen OOS Calibrated Model (`240` contracts):** Accuracy `67.92%` · Brier `0.1893` · LogLoss `0.5530` · 10-Bin ECE `0.0697`
- **Unseen OOS Naive Market Baseline:** Accuracy `66.25%` · Brier `0.2087` · LogLoss `0.5978` · 10-Bin ECE `0.0719`
- **Measured Skill Improvement:** **`+9.33%` Brier Skill Score** vs. raw implied midpoint probability; **4/4 `--test` assertions PASS** (gradient convergence, calibration dominance over naive baseline, non-trivial edge, and directional monotonicity).

*Scope Note: The public gist verifies the exact mathematical pipeline on a deterministic synthetic CLOB corpus so any reviewer can reproduce it without private credentials; proprietary live-feed backtests (~78% historical accuracy) stay private.*

---

**Author:** Sofian Mousa · **Contact:** `sofianmousa@apodictic.dev`
