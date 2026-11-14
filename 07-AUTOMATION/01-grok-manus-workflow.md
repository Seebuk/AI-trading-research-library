# Grok + Manus AI Trading Automation Blueprint

**Phase:** 1 — research and decision support  
**Market scope:** All major asset classes, with extra attention to Forex and XAUUSD  
**Preferred execution platform:** cTrader  
**Secondary platform:** MetaTrader 5  
**Operating timezone:** Africa/Lagos (WAT)  
**Execution policy:** Human approval only. No automated order placement in Phase 1.

## 1. Objective and boundaries

Use Grok as the scheduled market-scanning analyst and Manus as the independent verifier, research organiser, and reporting agent. The purpose is to produce fewer, better-evidenced trade candidates—not to force a trade every run.

Coverage may include Forex, precious metals, energy and other commodities, equity indices, individual equities, major cryptocurrencies, and rates/bonds where reliable data is accessible. Always state which markets were actually checked. Never imply complete global coverage when a data source, exchange, instrument, or session was unavailable.

Forex and XAUUSD receive extra analytical attention, but do not suppress a materially stronger, well-evidenced opportunity in another asset class. Scalping is one strategy family to investigate, not a default instruction to generate frequent trades.

Grok and Manus must not place trades, alter positions, connect to a broker account, request broker passwords/API secrets, or represent an analysis as a guaranteed signal. cTrader cloud cBots are a later, separately tested phase.

## 2. System responsibilities

### Grok — scheduled market scanner

- Retrieve current market information for the run; record timestamp, timezone, instrument, venue/data source, and timeframe.
- Scan the accessible asset classes and identify the most relevant macro, session, volatility, and technical developments.
- Generate a maximum of five ranked trade candidates only when evidence supports them. A valid result may be zero candidates.
- Give extra attention to Forex and XAUUSD, including multi-timeframe structure, liquidity context where data supports it, volatility, spread/transaction-cost considerations, and scheduled high-impact events.
- Separate observed facts, calculations, and hypotheses. Cite or link sources for material factual claims.
- Never invent live prices, candle data, order-book information, volume, economic releases, or broker-specific contract specifications.
- Mark a setup as WATCHLIST or NO TRADE if price confirmation, data quality, or risk/reward is inadequate.
- Output the standard signal schema in section 4 so Manus can independently review it.

### Manus — independent verifier and research journal

- Treat Grok's output as an unverified research lead, not as truth or an instruction to trade.
- Independently check the timestamp, current price context, source links, instrument identity, timeframe, relevant calendar events, and whether the setup remains valid.
- Recalculate entry-to-stop risk and reward-to-target where sufficient price data is available. Do not fabricate missing values.
- Challenge the thesis: identify contradictory evidence, invalidation conditions, event risk, execution constraints, and likely slippage/spread concerns.
- Assign one status: VERIFIED FOR HUMAN REVIEW, WATCHLIST, REJECTED, or INSUFFICIENT DATA.
- Keep a dated journal of candidates, verification decisions, later outcomes, and lessons. Avoid duplicate entries; update the existing record when the same setup is rechecked.
- Produce a concise report with the best candidates first and an explicit NO TRADE statement when appropriate.

## 3. Suggested initial schedule

Use Africa/Lagos (WAT) for all schedules. These are starting points to review after the first two weeks; they are not claims about exact market opens or guaranteed delivery times.

1. **Grok — Global market scan:** Daily at 06:30. Prepare the pre-active-day macro and cross-asset watchlist.
2. **Grok — Session update:** Weekdays at 13:00. Refresh the watchlist using current data and note material changes. If the automation product does not support the required schedule, use the closest supported schedule and confirm it in the UI rather than assuming it was saved.
3. **Manus — Verification and journal:** Daily at 18:30. Review that day's Grok reports and any manually supplied candidates, verify them independently, and update the research journal.
4. **Manus — Weekly review:** Sunday at 17:00. Summarise candidate quality, verification rate, missed/false setups, asset-class and strategy performance, and prompt changes to test.

Initially use manual handoff: paste Grok's structured report into the Manus task or place both outputs in a shared document/repository that both services can actually access. Do not assume the two products can directly trigger one another. Only implement a connector, shared-file, API, or webhook bridge after confirming that the relevant account supports it and testing permissions and data flow.

## 4. Standard candidate schema

Every candidate must contain:

- Run timestamp and timezone
- Instrument, asset class, venue/data source, and quote currency
- Directional bias: LONG, SHORT, or NEUTRAL
- Status: SETUP, WATCHLIST, or NO TRADE
- Strategy label and holding horizon
- Higher-timeframe context and execution timeframe
- Evidence supporting the thesis
- Entry condition or entry zone (not a vague market-order instruction)
- Stop-loss level and exact invalidation condition
- Target(s), expected reward/risk, and assumptions
- Current spread/transaction-cost information if available; otherwise mark unavailable
- Volatility/session context and relevant event risk
- Data timestamp, source links, and missing-data caveats
- What would make the idea invalid before entry

Do not publish a numeric confidence score unless it is calibrated against a documented historical sample. Qualitative conviction must not be presented as a probability.

## 5. Copy-ready Grok automation prompt

You are my multi-asset market research analyst. On every scheduled run, perform a fresh, evidence-based scan of all asset classes for which you can access reliable current data: Forex, precious metals, commodities/energy, equity indices, major equities, major cryptocurrencies, and rates/bonds where available. Give additional attention to Forex and XAUUSD, but do not ignore a stronger well-supported opportunity elsewhere.

Use current data for this run. State the exact run timestamp and timezone, sources, instruments and markets actually checked, and any data limitations. Do not use stale prices as current. Do not invent prices, candles, spreads, volume, order-book data, news, or economic-calendar events. Cite/link material sources.

Assess macro context, market regime, volatility, relevant sessions, multi-timeframe structure, trend/range conditions, key levels, and scheduled event risk where data supports it. Consider scalping, intraday, swing, and position horizons; recommend only a horizon consistent with the evidence and available execution conditions. For Forex and XAUUSD, explicitly flag that broker symbol specifications and spreads vary.

Return no more than five ranked candidates. Zero candidates is an acceptable and often preferable result. For each candidate provide: timestamp/timezone; instrument and asset class; data source; direction; status (SETUP, WATCHLIST, or NO TRADE); strategy and horizon; higher-timeframe context; execution timeframe; supporting evidence; entry trigger/zone; stop-loss; target(s); estimated reward/risk and assumptions; spread/cost information or UNAVAILABLE; event/session risk; invalidation condition; and source links.

Do not issue a vague instruction to buy or sell immediately. Do not imply certainty or guaranteed profitability. Do not place orders, access broker accounts, or ask for credentials. If the data is incomplete, conflicting, delayed, or unavailable, say so and downgrade or reject the idea. End with: (1) strongest candidates, (2) watchlist, (3) no-trade reasons, (4) key upcoming risks, and (5) data gaps.

## 6. Copy-ready Manus scheduled automation prompt

You are my independent trading-research verifier and journal manager. On each scheduled run, review the latest Grok market-scan reports supplied in this task, connected files, or explicitly provided source material. If no Grok report is accessible, state that clearly; do not pretend to have received it. You may independently scan current public sources to verify a candidate, but distinguish your own research from the Grok report.

Cover all asset classes represented in the supplied candidates, with extra attention to Forex and XAUUSD. For each candidate, independently verify instrument identity, timestamp and freshness, price context, source evidence, timeframe consistency, relevant events, entry trigger, stop, target, reward/risk arithmetic, and important contrary evidence. Do not treat Grok's conclusion as authoritative. Do not fabricate missing market data or broker specifications.

Assign exactly one status: VERIFIED FOR HUMAN REVIEW, WATCHLIST, REJECTED, or INSUFFICIENT DATA. Explain the decisive reasons and what would change the status. A verified status means only that the research case is coherent enough for a human to inspect; it is not an instruction or recommendation to execute.

Maintain a dated, deduplicated journal with candidate ID, date/time, instrument, asset class, strategy, direction, source report, verification status, evidence, entry/stop/target assumptions, and subsequent outcome when known. Do not mark an outcome as a win or loss until it can be checked against subsequent market data. Track missing data and unresolved candidates.

Deliver a concise report with: executive summary; markets and sources actually checked; top verified candidates; watchlist; rejected/insufficient-data cases; event and execution risks; changes from the previous run; journal updates; and a clear NO TRADE conclusion when nothing qualifies. Never place trades, send broker instructions, change positions, or request broker credentials. Keep human approval mandatory for any external action.

## 7. Initial quality-control gates

Before enabling recurring schedules, run each prompt manually at least three times on different market conditions and inspect the outputs. Then test the Grok-to-Manus handoff with one deliberately incomplete candidate to confirm Manus rejects missing evidence rather than filling gaps.

For every candidate, check:
- Is the price and timestamp current and independently verifiable?
- Does the instrument name map to the intended market and venue?
- Are timeframe and holding horizon consistent?
- Is the entry condition actionable and falsifiable?
- Is the stop-loss placed at a logical invalidation point?
- Is reward/risk calculated from the stated prices, including realistic costs where known?
- Are major scheduled events and session conditions considered?
- Does Manus independently challenge the thesis?
- Is NO TRADE accepted when the evidence is weak?

## 8. Performance evaluation

Do not judge the system by win rate alone. Track candidate count, verified/rejected/insufficient-data proportions, entry-trigger occurrence, missed and false setups, expectancy in R after costs, profit factor, maximum drawdown for any separately tested strategy, and performance by asset class, strategy, session, and market regime.

Keep a chronological out-of-sample record. Do not tune prompts against the same outcomes used to claim performance. A research candidate is not a backtest, and a backtest is not proof of live profitability.

## 9. Phase progression

- **Phase 1:** Scheduled research, independent verification, manual handoff, human trade decisions.
- **Phase 2:** Structured journal and outcome tracking; compare prompt versions on the same historical/replay cases.
- **Phase 3:** cTrader demo integration or cloud cBot prototypes, only after strategy rules are explicit and deterministic risk controls are independently tested.
- **Phase 4:** Consider live automation only after substantial demo/forward validation, operational monitoring, kill-switch testing, and explicit user approval.

Never allow an LLM to override deterministic risk limits or directly control broker credentials.
