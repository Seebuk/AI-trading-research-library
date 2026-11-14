# Curated Prompt Test Shortlist

Status: **Candidate prompts — not yet validated**
Review date: 2026-11-14

This shortlist prioritizes prompts that produce specific, falsifiable trading decisions for Forex and XAUUSD, with MetaTrader 5 (MT5) as the primary test and eventual automation environment. It deliberately separates analysis from risk authorization. No prompt is approved for live execution.

## Selection criteria

1. Clear, rule-based outputs: setup, trigger, invalidation, stop, targets, and no-trade conditions.
2. Multi-timeframe context without hindsight or repainting.
3. Explicit handling of spread, slippage, commissions, volatility, and news.
4. Ability to say **no trade** when evidence is insufficient.
5. Testability on timestamped historical data and forward paper trading.
6. No unsupported claims that an AI confidence score is a win probability.

## Initial test order

| Priority | Prompt | Purpose | Why test it |
|---|---|---|---|
| 1 | [Multi-timeframe setup analyst](01-multi-timeframe-setup-analyst.md) | Identify and qualify setups | Establishes a consistent baseline for FX and gold |
| 2 | [Scalping execution planner](02-scalping-execution-planner.md) | Define precise scalp entry/exit rules | Directly targets the user's scalping interest |
| 3 | [Independent risk auditor](03-independent-risk-auditor.md) | Reject unsafe or incomplete trades | Adds a separate risk gate instead of trusting the analyst |
| 4 | [Strategy research and backtest designer](04-strategy-backtest-designer.md) | Convert ideas into reproducible tests | Prevents visual chart narratives from being mistaken for edge |

## MT5-first test priorities

- Use the broker's actual MT5 symbol names (including suffixes/prefixes), contract specifications, tick size/value, volume step/minimum, stops level, trading sessions, and account currency.
- Use MT5 Strategy Tester for deterministic Expert Advisor (EA) rules, with the closest available tick modelling and variable-spread assumptions. Record modelling quality and data limitations.
- Validate on demo before any live use. Do not let an LLM directly hold broker credentials or bypass EA-side risk checks.
- Treat an LLM as an optional research/signal explanation layer. Keep order validation, position sizing, stop enforcement, exposure limits, and kill-switch logic deterministic in the EA.
- Confirm whether the broker offers the intended instrument as spot FX, CFD, or another contract; XAUUSD specifications differ by broker.

## How to test

- Use the same historical sample, instrument, timeframe, and data for each candidate.
- Give prompts only information that would have been available at the decision timestamp.
- Freeze prompt versions during each test batch.
- Record every signal, including rejected and no-trade decisions.
- Compare against simple baselines (e.g. no-trade, session breakout, moving-average trend filter).
- Evaluate net results after realistic spread, commission, swap/funding where applicable, and slippage.
- Use chronological train/validation/test splits and walk-forward checks. Never tune on the final holdout.
- Paper trade before any live consideration.

## Minimum evaluation metrics

Trade count; win rate; average win/loss; expectancy in R; profit factor; maximum drawdown; consecutive losses; exposure; missed/false signals; and performance by instrument, session, volatility regime, and news condition. Report confidence intervals where possible.

## Promotion rule

A prompt advances only if it improves a predeclared metric versus the baseline on unseen data, remains stable across multiple periods/regimes, and passes the independent risk audit. A high win rate alone is insufficient.

## Important limitations

A language model reading chart descriptions is not a substitute for reliable OHLCV/tick data. If screenshots are used, record their timestamp and visible timeframe and do not infer unavailable price details. AI output is a hypothesis generator, not an execution signal.
