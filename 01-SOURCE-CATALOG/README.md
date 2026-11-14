# Initial Source Catalog

Research leads collected from the initial Grok-assisted scan and follow-up review. These entries are leads, not endorsements or evidence of profitability. Verify each repository's current contents, activity, supported markets, and licence before adopting anything.

| Project | Research area | Initial assessment |
|---|---|---|
| [NoFxAiOS/nofx](https://github.com/NoFxAiOS/nofx) | AI trading terminal and prompt configuration | Review its prompt guide and risk settings. Verify broker, instrument, and execution support before assuming Forex or XAUUSD compatibility. |
| [kojott/LLM-trader-test](https://github.com/kojott/LLM-trader-test) | LLM paper trading and backtesting | Useful study of structured decisions, stop-loss/exit planning, and replay testing. Its documented exchange/data scope is crypto-centric, not a turnkey FX or gold system. |
| [0xethanq/astra-quant-agent](https://github.com/0xethanq/astra-quant-agent) | Multi-agent quant research and execution | Review separation between LLM analysis and deterministic risk gates. Check current exchange/instrument support; do not infer Forex/XAUUSD support. |
| [xlabsg/prompTrading](https://github.com/xlabsg/prompTrading) | Natural-language strategy generation and backtesting | Potentially useful for turning strategy descriptions into testable rules. Treat project performance claims as unverified until independently reproduced. |
| [timoranjes/trading-ai-prompts](https://github.com/timoranjes/trading-ai-prompts) | Trading prompt collection | Broad prompt-library lead. Inspect individual files and reconcile licence and any paid-library/redistribution terms before copying or adapting content. |
| [ternary-ai/prompts](https://github.com/ternary-ai/prompts) | Financial-agent prompts | Potentially useful for research, portfolio, and risk workflows. Treat trading-specific material as experimental until validated. |
| [ilincic66-lgtm/AI-Trading-Prompts](https://github.com/ilincic66-lgtm/AI-Trading-Prompts) | Trading prompts | Lead supplied for later verification; inspect contents, provenance, licence, and update history. |
| [motowntrades/quant-math-grok-prompts](https://github.com/motowntrades/quant-math-grok-prompts) | Quant prompts for Grok | Lead supplied for later verification; check repository availability, prompt quality, and licence. |
| [majiajue/longbridge](https://github.com/majiajue/longbridge) | Trading-agent/system-prompt lead | Verify exact project scope, supported markets, and current documentation before adopting. |
| [M-Pineapple/CryptoAnalysisMCP](https://github.com/M-Pineapple/CryptoAnalysisMCP) | Crypto analysis prompts/tools | Crypto-specific lead; potentially useful for agent/tool design, but not directly an FX or gold solution. |
| [ai-boost/awesome-prompts](https://github.com/ai-boost/awesome-prompts) | General prompt collection | Search for quantitative-agent material; evaluate quality and licensing at the individual prompt level. |
| [Lumiwealth/lumibot](https://github.com/Lumiwealth/lumibot) | Algorithmic trading framework | Framework lead for expressing and testing systematic rules. Check current broker/data integrations and instrument coverage before selecting it for FX or gold. |

## Evaluation checklist

- What markets, instruments, brokers, and data feeds are actually supported?
- Are fees, spread, slippage, latency, funding, and market impact modelled?
- Is there reproducible out-of-sample or walk-forward evaluation?
- Are drawdown, expectancy, profit factor, trade count, and risk metrics reported?
- Are risk checks deterministic and independent of the language model?
- What licence applies to code and prompts? Are there additional restrictions?
- Can it be run safely in a sandbox or paper-trading environment?

## Evidence status

Use **Unverified**, **Reviewed**, **Tested**, or **Rejected**. Record the review date and the commit or release inspected. Repository stars, screenshots, author claims, and AI-generated confidence scores are not proof of profitability.

## Next steps

Verify each lead against its live repository, then move only useful and legally reusable ideas into original custom prompts. Keep third-party material attributed and linked; do not copy whole prompt collections without permission.