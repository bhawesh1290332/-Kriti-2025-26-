# -Kriti-2025-26-
This was the first proper group project I was involved in, great experience and got to learn a lot from seniors. We made a long only alpha modeling strategy for equity market
# Combined Equity Strategy — Kriti 2026 Quant Finance Challenge

**Kriti 2026** · Finance and Economics Club, IIT Guwahati

---

## Overview

A combined quantitative equity strategy built on NSE (National Stock Exchange) price data, allocating capital across two complementary sleeves:

| Sleeve | Allocation | Strategy |
|--------|------------|----------|
| **IPO Sleeve** | 30% (10% for large universe) | Momentum-based entry on newly listed stocks with drawdown-triggered liquidation |
| **Portfolio Sleeve** | 70% (90% for large universe) | Mean-variance optimisation via `cvxportfolio` with transaction cost modelling |

Initial capital: ₹50,00,000

---

## My Contributions

- **Dataset analysis** — explored NSE price data to identify exploitable patterns in IPO listing behaviour, price action in the first few trading days, and sector-level return distributions
- **IPO sleeve strategy design** — developed the entry/exit logic including trailing stop-loss, re-entry conditions, and drawdown-based liquidation thresholds

---

## Strategy Details

### IPO Sleeve
Stocks are flagged as IPOs if their first appearance in the dataset post-dates the universe start date. Entry is triggered after a 5-day price check (entry only if closing price < ₹40). Key parameters:

- `IPO_TRAILING_STOP = 20%` — exit triggered if price falls 20% from peak
- `IPO_DD_HALF / FULL = 30% / 40%` — drawdown thresholds for partial and full sleeve liquidation
- `IPO_COOLDOWN = 5 days` — minimum wait before re-entry in same stock
- `IPO_REENTRY_RISE = 10%` — price must recover 10% from exit before re-entry
- Max 10 trades per symbol; max 10% of IPO capital in any single position

### Portfolio Sleeve
Uses `cvxportfolio` for convex portfolio optimisation, incorporating:
- Transaction cost modelling (`TXN_COST_PCT = 0.268%`)
- Max 100 total positions
- Excess returns from freed IPO capital injected dynamically into the portfolio sleeve

---

## Setup & Usage

```bash
pip install cvxpy cvxportfolio pandas numpy matplotlib
python 2613_CodeBase_QuantFinChallenge.py
```

**Required data file:** `nse_prices_complete.parquet` (or `.csv`) in the working directory, with columns: `date`, `symbol`, `open`, `high`, `low`, `close`, `exec_price`, and optionally `sector`, `lms`, `in_nse500`.

---

## Dependencies

`cvxpy`, `cvxportfolio`, `pandas`, `numpy`, `matplotlib`

---

*Developed as part of Kriti 2026 Quant Finance Challenge, IIT Guwahati.*
