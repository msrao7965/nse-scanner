# TradeLab India — NSE Research Terminal

A static, browser-based research prototype for Indian equity OHLCV data. It includes a technical screener, watchlist, price/EMA chart, rule-based long-only backtester, and weekly +50% target / -30% stop study.

## Deploy to Vercel

1. Open https://vercel.com/new and sign in with GitHub.
2. Import **msrao7965/nse-scanner**.
3. Select **Other** as the framework preset. No build command or environment variables are required.
4. Keep the project root as `./` and deploy.
5. Open the generated Vercel URL on mobile or desktop.

This is a static `index.html` application. It does not require a Python runtime, server, database, or API key for the included functionality.

## Import data

Upload a CSV with these required headers:

```csv
symbol,date,open,high,low,close,volume
RELIANCE,2025-01-01,1200,1220,1190,1210,2500000
```

Header names are case-insensitive. ISO dates (`YYYY-MM-DD`) are recommended. Use consistently adjusted prices for long-horizon research. Each symbol should have one row per candle timestamp. The app validates OHLC relationships and removes duplicate symbol/date rows.

## Included modules

- Dashboard and data coverage
- AND/OR technical screener: Close, EMA 20/50, RSI 14, volume, 20-bar average volume, relative volume, change, previous 20-bar high
- Saved screeners and watchlist (browser local storage)
- Historical close/EMA chart
- Long-only backtest with next-bar-open entry, stop/target, max holding bars, position sizing, estimated costs, MFE/MAE, equity curve, win rate, profit factor and drawdown
- Weekly 50/30 study with target-first / stop-first outcomes, post-target maximum high, post-stop minimum low, MFE/MAE and CSV export

## Important limitations

- **No live NSE feed is included.** The app does not claim to scan live markets. It operates on historical CSV data you supply.
- **No market data is bundled.** Coverage and quality depend on the source, corporate-action adjustment, symbol history and completeness.
- Candles are held in browser memory for the current session. Saved screeners and watchlist use local storage. Re-import your CSV after a refresh; large files may be limited by browser memory.
- All processing occurs in the browser. There is no account, cloud database, server-side ingestion, or multi-device sync.
- Weekly study aggregates daily OHLC into weekly bars. If both barriers are touched in one weekly candle, stop-first is assumed. This is conservative but cannot reveal the true intraperiod path.
- Backtest assumptions are simplified. Slippage, taxes, liquidity, survivorship bias, delisted securities, corporate actions, execution latency and portfolio-level capital contention need further modelling.
- Chart.js is loaded from jsDelivr and fonts from Google Fonts; internet access is needed for those presentation assets.
- This is research software, not investment advice.

## License and market data

The app code in this repository is provided under the MIT License. This does not grant rights to third-party exchange data. Check the applicable provider and exchange terms before using, redistributing, or commercializing any imported dataset or offering data-backed services.
