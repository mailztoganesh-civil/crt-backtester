# CRT Backtester

Browser-based backtester for Candle Range Theory (CRT) on NSE stocks.
Upload intraday OHLC CSV files, choose timeframes and rules, and compare results.
Data never leaves the browser.

## Deploy on GitHub Pages
1. Create a repo and upload `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`.
2. Settings → Pages → Source: deploy from branch `main`, folder `/ (root)`.
3. Open `https://<username>.github.io/<repo>/`.

## CSV format
Header row with `timestamp` (or `date` + `time`) and `open, high, low, close`.
Accepted times: `2024-05-13 09:15:00+05:30`, `2024-05-13T09:15`, `13-05-2024 09:15`, or Unix epoch.
Rows outside 09:15–15:30 IST are ignored.

## Rules simulated
- Trend: fast EMA > slow EMA and close > slow EMA on the trend timeframe (mirror for shorts).
- Range candle (optionally a correction candle), next candle sweeps its low/high and closes back inside.
- Entry: limit order at the first FVG on the entry timeframe after the sweep closes.
- Stop beyond sweep wick or FVG edge; target at range end, N-candle high/low, or fixed R.
- Optional partial at X R with stop to breakeven; intraday square-off or max-hold exit.
- Fills on base bars; gaps through stop/target fill at the open; same bar stop + target counts as stop.
