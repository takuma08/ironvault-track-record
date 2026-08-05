# IronVault — Track Record

Automated performance record for **IronVault Algo System v3.7**.

The record files in this repository are written automatically by the live
system. No trade or signal record is created or edited by hand. This README is
maintained by hand; changes to it are in the commit history like everything else.

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
| `signals.csv` | Every signal at detection time: timestamp, symbol, side, entry, SL, TP, config version |
| `trades.csv` | Every closed trade: entry/exit price, result, P/L %, config version |
| `performance.json` | Running balance, trade count, win rate, peak, per-config breakdown |

## What is published

- Detection timestamps and bar timestamps
- Symbol, timeframe, direction
- Entry price, stop loss, take profit
- Exit price, exit reason, P/L %
- Account balance and summary statistics
- The configuration version in effect when each record was generated

## What is not published

- Strategy logic
- Indicator parameters and thresholds
- Internal strategy labels
- Backtest data and research code

The system runs 19 strategies selected from 2,500+ backtested variants. The
selection process is not public; the results are.

## Operating policy

- Records are appended, never rewritten
- Losing trades are published the same as winning trades
- No cherry-picking, no retroactive edits
- If a record ever needs correction, the correction is a new commit — the
  original stays in history

## Configuration changes

The system's configuration is not frozen. When it changes, it is recorded here,
including changes to what this repository publishes.

Records generated under different configurations are not directly comparable.
The `config_version` field in `signals.csv` and `trades.csv` marks which
configuration produced each record.

### 2026-08-05 (UTC) — v3.7.0 → v3.7.1

**What changed.** The smoothing method for three indicators (ATR, RSI, ADX) was
changed from a rolling mean to an exponentially weighted moving average.

**Why.** The live system and the system used to validate the strategy selection
had different implementations of these three indicators. The live system was
therefore running under conditions that had never been validated. This change
aligns the live system with the validated one. It was found during an internal
audit, not reported from outside.

**Effect.** Signals generated before and after this timestamp come from
different conditions and are not directly comparable. Records from before the
change are labelled `v3.7.0` and are left exactly as they were; records from
after are labelled `v3.7.1`.

A trade is labelled by the configuration in effect when it was **entered**, not
when it closed.

### 2026-08-04 (UTC) — record format and disclosure policy

**Record format.** Added a `config_version` column to `signals.csv` and
`trades.csv`, and `config_version` / `by_config` fields to `performance.json`.
All existing records are labelled `v3.7.0`.

This is a column addition, not a rewrite of values. Every previously published
number is unchanged. Because the files are regenerated in full on each update,
the commit for this change shows a diff on every row; that diff is the new
column only.

**Disclosure policy.** The "What is not published" list previously read
"Strategy logic and indicator formulas". It now reads "Strategy logic" and
"Indicator parameters and thresholds" as separate items.

This was narrowed deliberately, so that the configuration change recorded below
can be described concretely rather than in vague terms. Naming which indicators
changed does not reveal the strategy set. Their periods, spans and thresholds
remain unpublished.

Changing what we disclose is itself disclosed. It is recorded here rather than
made silently.

---

*Simulated results. Not investment advice. Past performance does not
guarantee future results.*
