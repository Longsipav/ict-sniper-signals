# ICT Sniper Signals — free static website

## What is included
- `index.html`: responsive dashboard, TradingView embeds, BTC and tokenized-gold proxy 15-minute signal scanner, entry/SL/TP, and browser-session signal history.
- No paid hosting or API key is needed for the Binance feeds in this prototype.

## Important market-data limitation
- BTC signals use Binance `BTCUSDT` spot candles.
- The Gold card's *signal engine* uses Binance `PAXGUSDT` (Pax Gold token), **not XAUUSD spot or your broker's gold CFD**. It is a gold proxy and can differ from XAUUSD.
- The TradingView Gold chart displays `OANDA:XAUUSD`, but the signal levels are not calculated from that chart.
- To make the Gold signal genuinely XAUUSD, connect a market-data provider that offers 15-minute XAUUSD candles (for example, a provider account/API key) and update `fetchCandles()` to use that provider. Do not put private API keys in public client-side code; use a server/worker secret instead.

## Run locally
1. Download and unzip the project.
2. Open `index.html` in a modern browser with an internet connection. If the browser blocks requests from `file://`, run a local static server:
   - Install Python 3 if needed.
   - Open a terminal in this folder and run `python -m http.server 8000`.
   - Visit `http://localhost:8000`.

## Publish for free with GitHub Pages
1. Create or sign in to a GitHub account at https://github.com.
2. Create a **public** repository named `ict-sniper-signals`.
3. Upload `index.html` and this README (or upload the project files).
4. Open repository **Settings → Pages**.
5. Under build/deployment, choose **Deploy from a branch**, choose `main` and `/(root)`, then save.
6. Wait for deployment. Your site URL will be similar to `https://YOUR-USERNAME.github.io/ict-sniper-signals/`.

## How the prototype rules work
The engine uses closed 15-minute candles. It checks for:
- a wick sweep of the recent 20-candle high/low followed by a close back inside;
- a recent 5-candle structure break;
- a three-candle gap approximation;
- price in discount for a bullish setup or premium for a bearish setup.

It emits a signal only when these checks align; otherwise it shows WAIT. These are simplified ICT-inspired mechanical rules, not a validated profitable strategy. Signals refresh every minute and the current forming candle is excluded.

## Before live use
- Backtest and paper-trade across market sessions and different volatility regimes.
- Add server-side logging and persistent history if required.
- If you later add alert notifications, keep secrets server-side and test all failure cases.
- This site does not place trades or connect to a broker. It is not financial advice.
