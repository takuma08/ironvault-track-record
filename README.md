# IronVault — Track Record

Automated performance record for **IronVault Algo System v3.7**.

This repository is updated automatically by the live system. Nothing here is
written or edited by hand.

---

## What this is

A tamper-evident log of every signal the system produces and every trade it
closes. Because the files are committed by an automated job, any edit to past
records would appear in the Git history.

**Verify it yourself:** check the commit history. Each commit is timestamped
and shows exactly what changed.

## Account type

**Demo (simulated) account.** Starting balance $5,000, 0.90% risk per trade.

The developer is based in Japan and cannot access Binance Futures due to
regional restrictions. All records here are therefore simulated fills on live
market data, not executed orders. This is stated up front rather than buried
in a disclaimer.

## Files

| File | Contents |
|---|---|
| `signals.csv` | Every signal at detection time: timestamp, symbol, side, entry, SL, TP |
| `trades.csv` | Every closed trade: entry/exit price, result, P/L % |
| `performance.json` | Running balance, trade count, win rate, peak |

## What is published

- Detection timestamps and bar timestamps
- Symbol, timeframe, direction
- Entry price, stop loss, take profit
- Exit price, exit reason, P/L %
- Account balance and summary statistics

## What is not published

- Strategy logic and indicator formulas
- Internal strategy labels and parameters
- Backtest data and research code

The system runs 19 strategies selected from 2,500+ backtested variants. The
selection process is not public; the results are.

## Operating policy

- Records are appended, never rewritten
- Losing trades are published the same as winning trades
- No cherry-picking, no retroactive edits
- If a record ever needs correction, the correction is a new commit — the
  original stays in history

---

*Simulated results. Not investment advice. Past performance does not
guarantee future results.*
