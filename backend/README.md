# Market Watch backend

The backend keeps the AI key server-side and exposes `/health`, `/api/analyze`, and an optional `/api/events` provider proxy.

## Run locally
1. Install Node.js 20+.
2. In this folder run `npm install`.
3. Copy `.env.example` to `.env` and set `OPENAI_API_KEY` privately.
4. Run `npm start`.

Do not commit `.env`. The default frontend only tries `http://localhost:8787` when opened on localhost. When hosted on GitHub Pages, configure a secure HTTPS backend and set `API_BASE` in `app.js` to that URL.

## Calendar and market data
Forex Factory is linked as a source for manual verification, but this project does not scrape it and does not claim its calendar data are live. It does not have an official generally available public API that this project can safely assume. Configure `CALENDAR_API_URL` to a provider you are authorized to use, and normalize the provider response before using it in the frontend. The endpoint proxy is deliberately generic and does not guarantee compatibility with any arbitrary provider schema. Actual, consensus, previous and revised-previous fields should be mapped and provenance retained.

Official release sites (BLS, BEA, Fed, ECB, EIA) are useful for verifying released figures; consensus forecasts usually require a dedicated licensed provider. CoinGecko can provide crypto market data, but it is not an economic-calendar source.

## AI behavior
The model receives only the event and context sent by the frontend. It must not invent missing data, price targets or pip moves. Treat output as a probabilistic explanation, not a trading signal. Add authentication/rate limiting and restrict `ALLOWED_ORIGIN` before public deployment to prevent abuse and unexpected API costs.
