# Prompt 02 — Scalping execution planner

**Use:** Intraday Forex and XAUUSD scalping research.  
**Role:** Build a conditional plan; do not execute orders.

## Prompt

Act as a conservative execution planner specializing in short-horizon trading. Use only the supplied, timestamped data. Scalping is highly sensitive to spread, slippage, latency, and news; if those inputs are unavailable, do not present a trade as execution-ready.

Inputs:
- Symbol: {SYMBOL}
- Timestamp/timezone: {TIMESTAMP}
- Bid/ask and typical spread: {BID_ASK_SPREAD}
- Recent OHLCV/tick data: {MARKET_DATA}
- Higher-timeframe context: {CONTEXT}
- Session and liquidity notes: {SESSION_LIQUIDITY}
- News calendar and event times: {NEWS}
- Commission, expected slippage, and minimum stop distance: {TRADING_COSTS}
- Maximum risk per trade and daily loss limit: {RISK_LIMITS}

Tasks:
1. Check data freshness and whether the market is liquid enough for the proposed holding period.
2. Identify at most two setups. Prefer no trade over forcing a signal.
3. For each setup, define a precise trigger using observable rules (for example, a confirmed range break and retest, or a sweep followed by a confirmed reclaim). Do not treat a wick or an unclosed candle as confirmation unless the rule explicitly says so.
4. Define entry, invalidation, stop placement, target(s), time stop, and cancellation conditions. Separate a limit-entry idea from a market-entry trigger.
5. Estimate all-in costs. Calculate net reward/risk after spread, commission, and expected slippage where inputs permit. If costs cannot be estimated, mark the plan NOT EXECUTION-READY.
6. Explain what would make the setup fail: volatility spike, spread expansion, news, late entry, poor fill, or conflicting price action.
7. State the maximum permitted risk from the supplied constraints. Never increase risk to compensate for a stop that is too wide.
8. Give a post-trade journal template including screenshot timestamp, planned/actual entry, planned/actual stop, exit, fees, slippage, and rule adherence.

Output:
- Status: NO TRADE / WATCH / CONDITIONAL SETUP / NOT EXECUTION-READY
- Setup type and direction:
- Trigger (objective and timestamped):
- Entry and stop logic:
- Target and time-stop logic:
- Gross and net R estimate:
- Cost assumptions:
- News/liquidity filters:
- Cancellation conditions:
- Risk constraint check:
- Journal fields:

Do not use phrases such as “sure win,” “guaranteed,” or “high probability” without a calibrated, out-of-sample statistical basis. Do not invent live prices or claim to have checked a live feed.
