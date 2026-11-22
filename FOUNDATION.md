# SHELL / FOUNDATION

## Purpose
This repository contains the approved starting foundation for future Binance scanner projects. New scanner projects should begin from this baseline rather than rebuilding the common infrastructure.

## Baseline
- Binance USDⓈ-M USDT perpetual market universe.
- Includes only contracts that are trading, perpetual, quoted in USDT, and margined in USDT. USDC contracts are excluded.
- Independently configurable Top X gainers and Bottom Y losers, including zero for either side.
- Minimum 24-hour quote-volume filter; default: 2,000,000 USDT.
- Configurable concurrent-worker setting from 1 to 20; default: 8. The current shell exposes this setting, but coin-level worker jobs are not yet active.
- Auto-refresh choices: Off, 10 seconds, 30 seconds, 60 seconds, 2 minutes, and Continuous.
- Continuous mode starts the next universe refresh immediately after the previous refresh completes.
- Start scanning, scan once, stop, and save-settings controls.
- Public Binance market-data endpoints only. No API key and no trade execution.

## Diagnostics included
- Universe counts and selection accounting.
- Full audit of eligible contracts, including selected and not-selected reasons.
- REST request counts, request concurrency, load duration, errors, cooldown, and refresh-cycle history.
- Performance placeholders for coin jobs and candle-cache activity, which remain inactive until those systems are implemented.
- A reserved signal-diagnostics section; no RSI, MACD, or alert logic is included in the foundation.

## Architecture notes
- The current foundation uses REST requests for exchange information and 24-hour ticker data.
- WebSocket price/candle streams are not yet connected.
- The current refresh process rebuilds the market universe; it does not yet scan individual coins through a worker pool.
- Rate-limit handling includes Binance HTTP 418/429 cooldown behavior.
- No Open Interest components are included.

## Rules for future projects
1. Start from this SHELL / FOUNDATION baseline.
2. Preserve the universe-selection controls, common UI shell, request handling, refresh controls, and diagnostics unless a change is explicitly requested.
3. Add each project's signal logic as a separate layer. Do not import signal rules from another scanner unless specifically requested.
4. Keep project-specific alerts, indicators, and filters separate from the shared foundation.
5. Do not add Open Interest or trading/execution functionality unless explicitly requested.
6. Make changes incrementally and preserve a known-good foundation before introducing new features.

## Current reference
- Repository: [RSI-MACD-REVERSAL-ALARM](https://github.com/kingddenton/RSI-MACD-REVERSAL-ALARM)
- Scanner: [Live GitHub Pages site](https://kingddenton.github.io/RSI-MACD-REVERSAL-ALARM/)
- Foundation branch: `FOUNDATION`
- Baseline commit: `467aa808a5645b1307bc42273242ca2fcae9c5ad`

## Project brief
**Name:** SHELL / FOUNDATION

**Objective:** Provide a stable, reusable starting point for future Binance market-scanner projects.

**Scope:** Shared interface, USDT perpetual universe selection, REST request management, refresh scheduling, settings persistence, and diagnostics.

**Out of scope:** Project-specific trading signals, RSI/MACD rules, alerts, Open Interest, WebSocket streams, and trade execution. These may be added later as separately approved modules.

**Acceptance principle:** A new project should be able to start from this baseline and add its own signal engine without having to recreate the common scanner shell and universe infrastructure.
