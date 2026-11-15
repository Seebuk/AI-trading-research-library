# REA — Reverse Engineer Anything: Source Assessment

**Original project:** https://github.com/morluto/rea  
**User's reference copy:** https://github.com/Seebuk/Reversed-engineer-anything-to-be-considered-  
**Category:** AI-assisted software reverse engineering / MCP tooling  
**Library status:** Research candidate — useful for development research, not a trading-signal engine  
**Assessment date:** 2026-11-15

## Executive assessment

REA is an open-source toolkit that exposes reverse-engineering workflows to AI agents through MCP and command-line tools. Its documented targets include native binaries, JavaScript/Electron applications, .NET assemblies, websites, desktop installations, firmware-related artifacts and other technical artifacts. Depending on the target, it can return evidence such as pseudocode, assembly, strings, symbols, calls/references, module relationships and runtime observations.

Potential value to this trading research library: investigate how software features and algorithms are implemented, inspect open-source trading tools and indicators, understand integrations, and support independent implementation of documented behaviour.

REA does **not** itself provide a market-data feed, trading strategy discovery, profitable signals, broker connectivity, MT5 execution, cTrader execution, or scheduled market scanning. It should not be treated as a trading bot.

## Relevance to this project

| Use case | Potential value | Caveat |
|---|---|---|
| Inspect open-source MT5 Expert Advisors | High | Respect each repository's licence; source code is preferable where available |
| Inspect open-source cTrader cBots | High | C# source inspection is usually preferable to reverse engineering binaries |
| Understand indicator implementations | High | Verify calculations against independent references and test data |
| Study trading application integrations | Medium | Reverse engineering does not guarantee API compatibility |
| Investigate website or desktop application behaviour | Medium | Respect terms, access controls, privacy and applicable law |
| Discover profitable trading strategies automatically | Low / not a documented capability | REA is a software analysis toolkit, not a strategy researcher |
| Generate Grok or Manus scheduled market reports | Not applicable | Use the dedicated automation prompts and supported product features |

## Installation and operating requirements

The project README documents Node.js and npm requirements, with supported versions including Node.js 22.x (>=22.23.4), 24.x (>=24.22.1), or 26.12.1+, plus npm. The documented setup command is:

```bash
npx rea-agents setup
```

The setup flow supports several agents, including Claude Code, Codex, Cursor, Gemini CLI and Grok Build, subject to the project's current installation documentation. It configures an MCP server and matching workflow instructions; review proposed changes and approve only those you understand. Restart the configured agent after setup.

Native binary analysis may require a compatible provider such as Hopper, Ghidra, IDA or Kuna. Static JavaScript/Electron analysis has different requirements. Consult the upstream installation guide for current platform support, dependencies and limitations before installing.

Official documentation:
- Repository: https://github.com/morluto/rea
- Installation guide: https://github.com/morluto/rea/blob/main/docs/getting-started/installation.md
- MCP contracts: https://github.com/morluto/rea/blob/main/docs/reference/mcp-contracts.md
- Website and guides: https://rea.tools/
- npm package: https://www.npmjs.com/package/rea-agents

The repository README states that the project is MIT-licensed. Confirm the current licence and any third-party component licences before redistributing or incorporating code.

## Recommended safe evaluation plan

1. Start with an open-source trading indicator or EA whose licence permits inspection. Prefer source code over compiled binaries.
2. Ask REA to map the application structure, identify relevant functions, trace indicator calculations and cite the evidence used.
3. Independently compare the findings against the source, documentation and a small set of known input/output examples.
4. For MT5, test any understood indicator or strategy in MetaTrader 5 Strategy Tester; for cTrader, implement a separate cBot and use cTrader's backtesting tools.
5. Record the original repository, commit/version, licence, inspected files, REA version, tool/provider configuration, findings, uncertainties and test results.
6. Do not use REA to bypass licensing, authentication, access controls, payment restrictions, anti-cheat protections, or other technical safeguards. Do not inspect software or data without authorisation.

## Fit with the Grok + Manus automation architecture

REA is a **development-research tool**, separate from the Phase 1 scheduled market-research pipeline:

- Grok: scan accessible markets and produce structured, evidence-based candidate setups.
- Manus: independently verify candidates, maintain the research journal and produce reports.
- REA: investigate software implementations, indicator logic, open-source trading systems and integration code when development research is required.
- cTrader: human-approved execution in Phase 1; cloud cBots may be considered later after deterministic rules and risk controls are validated.

REA is a local agent/MCP workflow. Do not assume it can run as a Grok or Manus cloud schedule, or that either service can invoke its local tools. Confirm agent compatibility, local runtime access and permissions before attempting integration.

## Decision

**Keep REA in the library as a useful development-research candidate.** Do not make it a prerequisite for Phase 1. First validate the Grok/Manus research prompts and their handoff. Evaluate REA later when there is a specific EA, cBot, indicator, application or integration that needs investigation.

**Evidence discipline:** REA findings are hypotheses supported by tool output. They must be checked against source material and reproducible tests. Reverse engineering a program does not establish that its trading logic is profitable.
