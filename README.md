# Crypto Signal AI (Web MVP)

Production-style fullstack MVP built with **Next.js App Router + PostgreSQL + Drizzle ORM**.

## Implemented in this version

- Modular market data provider interface (`MarketDataProvider`)
- Mock provider (`MockMarketDataProvider`) with realistic OHLCV generation
- Multi-symbol support (BTC/ETH/SOL/XRP/BNB/DOGE/ADA/AVAX/LINK)
- Multi-timeframe support (1m, 3m, 5m, 15m, 30m, 1h, 4h, 1d, 1w)
- Indicator engine (EMA, SMA, RSI, MACD, ATR, Bollinger, ADX, CCI, Stoch RSI, OBV)
- Market structure + support/resistance + regime detection
- Weighted signal scoring with confidence breakdown
- No-trade filters (stale data, spread, low RR, insufficient candles)
- Entry/SL/TP and risk:reward generation
- Signal history persistence in PostgreSQL
- Watchlist CRUD in PostgreSQL
- Backtesting endpoint (sequential evaluation, no look-ahead)
- Dashboard + scanner + analysis UI with candle chart and reasons
- Risk disclaimer surfaced in API/UI

## API endpoints

- `GET /api/health`
- `GET /api/markets`
- `GET /api/markets/{symbol}`
- `GET /api/candles/{symbol}`
- `GET /api/signal/{symbol}`
- `GET /api/signals`
- `GET /api/signals/history`
- `POST /api/backtest`
- `GET /api/scanner`
- `GET /api/watchlist`
- `POST /api/watchlist`
- `DELETE /api/watchlist/{symbol}`
- `GET /api/custom-sources`
- `POST /api/custom-sources`
- `POST /api/custom-sources/test` (verify extracted live price)
- `DELETE /api/custom-sources/{id}`
- `GET /api/signal-stream/{symbol}` (SSE live analysis updates)

## Setup

1. Copy `.env.example` to `.env` and set values.
2. Push schema:
   - `npx drizzle-kit push`
3. Run app:
   - `npm run dev`

## Notes

- This MVP uses mock market data by default (development-safe).
- To force custom-link analysis, pass `?provider=custom` to `/api/signal/{symbol}`, `/api/candles/{symbol}`, `/api/scanner`, and `/api/markets` after adding a custom source.
- `POST /api/custom-sources` accepts `symbol`, `url`, `extractor` (`json|html`), and optional `jsonPath` / `priceRegex`.
- For `html` extractor, set an explicit `priceRegex` capture group (required for stable extraction).
- Signals are decision support only; no auto-trading.
- Architecture is designed to plug in real REST/WebSocket exchange providers next.
