# MT5-First Automation Research

Primary platform: **MetaTrader 5 (MT5)**  
Status: Architecture guidance only — no live trading integration is authorized.

## Recommended separation of responsibilities

1. **Research/LLM layer:** interprets supplied market context, proposes a conditional setup, explains evidence, and can return WAIT. It does not have broker credentials or authority to place orders.
2. **Deterministic MQL5 Expert Advisor (EA):** validates the signal schema, checks current quotes and trading conditions, calculates volume from verified contract specifications, and enforces hard risk limits.
3. **Broker/MT5 terminal:** owns order routing and reports actual fills, rejections, and position state.
4. **Audit log:** records the input snapshot, prompt/version, signal, EA decision, order request, broker response, costs, and resulting trade.

## MT5 compatibility checklist

Before testing any symbol, record its exact broker-specific MT5 name and verify:
- Contract size and calculation mode.
- Tick size, tick value, digits, and point size.
- Minimum/maximum volume and volume step.
- Stops/freeze levels and allowed order types.
- Trading sessions, holidays, and rollover behavior.
- Spread characteristics, commission, swaps, and execution mode.
- Account currency, leverage, margin requirements, and hedging/netting mode.

For XAUUSD, do not assume a universal contract size, tick value, lot size, or quote precision. Read the values from the broker's symbol specification and validate calculations against MT5.

## Test sequence

1. Compile and unit-test deterministic MQL5 logic.
2. Run MT5 Strategy Tester on historical data. Document tick model, data coverage, spread assumptions, and modelling limitations.
3. Use chronological out-of-sample and walk-forward periods.
4. Run a demo forward test and compare requested prices with actual fills.
5. Test failure cases: disconnected terminal, stale quote, rejected order, spread spike, market closed, duplicate signal, partial fill, and breached daily loss limit.
6. Require explicit human review before any live deployment.

## Non-negotiable controls

- EA-side risk limits must remain active even if the LLM returns malformed or unsafe output.
- Reject stale, incomplete, malformed, duplicate, or out-of-session signals.
- Never widen a stop or increase volume to recover losses.
- Enforce per-trade, daily, and aggregate exposure limits plus a manual kill switch.
- Do not store API keys, passwords, broker credentials, or account identifiers in prompts or GitHub.
- Do not let a model-generated confidence score determine position size.
- Log every rejected signal and order request for audit.

## Suggested signal contract

Use a strict schema with fields such as:
- schema_version
- signal_id
- symbol
- generated_at_utc
- valid_until_utc
- timeframe
- direction (BUY / SELL / NONE)
- setup_name
- trigger_condition
- invalidation_condition
- stop_price (optional until triggered)
- target_levels (optional)
- max_risk_fraction (must not exceed EA-configured cap)
- rationale
- data_timestamp

The EA must independently validate symbol, expiry, quote freshness, trading session, volume, stop distance, margin, and risk. A signal cannot override EA settings.

## Integration options to investigate

Evaluate MT5-native MQL5 EAs first. If an external Python service is considered for research or signal generation, keep it isolated from execution authority and define authenticated, local-only communication, schema validation, timeouts, and fail-closed behavior. Do not select a bridge or third-party execution package until its maintenance, security model, and compatibility are reviewed.
