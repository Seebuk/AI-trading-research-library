# Prompt Evaluation Protocol

Status: Initial protocol  
Date: 2026-11-14

## Objective

Compare prompt quality and decision usefulness independently from strategy profitability. A prompt can produce clear, consistent analysis and still describe a strategy with no trading edge.

## Phase A — Offline reasoning test

Build a timestamped case set containing trend, range, breakout failure, reversal, high-volatility, quiet-session, and major-news examples for EURUSD, GBPUSD, and XAUUSD where suitable data exists.

For every case:
- Supply only data available at the stated timestamp.
- Include bid/ask, spread, session, and event calendar when available.
- Include examples where the correct research response is WAIT or INSUFFICIENT DATA.
- Blind prompt identity when grading outputs.
- Have a human reviewer grade factual accuracy, rule clarity, missing-data handling, trigger specificity, and risk discipline.

## Phase B — Historical signal replay

Freeze prompt versions and replay them chronologically. Prevent future candles, revised news, or later chart annotations from entering the prompt. Log every response, including no-trade decisions. Do not selectively report only winning examples.

## Phase C — Quantitative strategy test

Translate any repeatable setup into deterministic code before measuring performance. Use realistic instrument-specific contract specifications and transaction costs. For XAUUSD, verify the broker's actual contract size, tick value, quote precision, trading hours, spread behavior, and margin rules; specifications vary by broker.

Use chronological train/validation/holdout partitions and walk-forward evaluation. Freeze rules before final holdout. Report expectancy, profit factor, max drawdown, trade count, tail losses, and results by regime/session. Include cost-stress tests.

## Phase D — Forward paper test

Run on a demo/paper account with live timestamps and realistic costs. Record signal time, order time, fill assumptions, spread, slippage, rejected orders, and rule deviations. Do not use live capital during prompt selection.

## Prompt scorecard (0–5)

| Dimension | Score |
|---|---:|
| Factual grounding / no fabricated data | |
| Clear and reproducible trigger | |
| Explicit invalidation and exit logic | |
| Appropriate no-trade behavior | |
| Cost and execution awareness | |
| Risk-limit compliance | |
| Consistency across repeated cases | |
| Output completeness and auditability | |

Score prompts on process quality separately from strategy performance. Do not combine these into a single opaque score.

## Decision gates

- **Reject:** fabricates data, leaks future information, omits invalidation, violates risk constraints, or cannot identify missing inputs.
- **Revise:** useful structure but inconsistent or ambiguous rules.
- **Advance to replay:** passes offline review with no critical safety failures.
- **Advance to paper:** reproducible historical behavior and acceptable out-of-sample results after costs.
- **Live consideration:** requires separate human governance, broker-specific operational testing, and independent safeguards. This protocol does not authorize live deployment.
