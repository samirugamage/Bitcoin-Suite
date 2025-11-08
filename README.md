# Bitcoin-Suite

Single file crypto toolkit in React.  
Seasonal chart with year overlays. TradingView price chart. Fee & FX calculator.  
PnL with per-row FX on buy date. Dark mode. Proxy toggle for CORS.


---

## Features

| Area | What you get |
| --- | --- |
| **Seasonal chart** | Coinbase-style area line with past-year overlays, optional normalization. Quote in LKR, USD, USDT, SGD, AUD, EUR, GBP, INR, HKD, JPY. |
| **Prices page** | TradingView Advanced Chart (tv.js): candles, bars, line, area, volume + indicators. Symbols: `BINANCE:BTCUSDT`, `COINBASE:BTCUSD`, `BYBIT:BTCUSDT`, `BITSTAMP:BTCUSD`, `KRAKEN:XBTUSD`. |
| **Fees & FX** | Live BTC price (Binance/Coinbase). Mempool fees (mempool.space / Blockstream fallback). Multi-source FX. Computes fee in sats, BTC, and your fiat; per-byte cost & percent of amount. |
| **Acquisition estimator** | P2P → exchange → hot wallet. Enter unit price, % fees, fixed USDT fee, and on-chain fee. Shows effective entry, network fee, total fees, and net BTC to wallet. |
| **PnL** | Add many buys with local currency & time. Looks up day-of FX and nearby BTC price. Shows BTC bought, current value, P/L, and totals by currency. |
| **UX** | Dark/Light themes (all text light in dark mode). CORS proxy switch. No build step — runs as a static page. |

---

## Quick start

This is a **single HTML file**. No build. No npm.

```bash
# Option 1: open directly
# Double-click index.html in a modern browser

# Option 2: serve locally (recommended)
# Python 3
python -m http.server 8080

# Node
npx serve -l 8080

# Then visit:
http://localhost:8080
```

**Notes**

- Some browsers block network fetches for `file://` URLs — prefer a local server.
- If Binance/FX endpoints hit CORS, toggle **CORS proxy** in the top bar.
- TradingView widgets load from the internet and need an active connection.

---

## Data sources

All requests run in the browser.

- **BTC price:** Binance ticker, Coinbase spot
- **Fees:** mempool.space API, Blockstream fee estimates (fallback)
- **FX rates:** fawazahmed0 currency API (jsDelivr & GitHub), exchangerate.host, open.er-api
- **Candles (seasonality):** Binance klines
- **Prices page:** TradingView Advanced Chart (tv.js)

When the proxy is on, requests go through `corsproxy.io`.

---

## Usage guide

### Seasonal chart

- Pick **Quote** currency (LKR, USD, USDT, …)
- Choose window: **1Y / 6M / 3M / 1M**
- Select **Overlays** (previous years)
- Toggle **Normalize** to align past curves to the current start value

### Prices page (TradingView)

- Select an **exchange symbol**
- Choose **Style**: Candles, Bars, Line, or Area
- Use TradingView’s tools, volume, and indicators inside the widget

### Fees & FX

- **Live** shows BTC spot & fee tiers
- **Network fee calc**: set sat/vB and size (vB)
- Optional **Amount sent** → shows fee as % of amount
- Per-byte cost shown in your selected fiat

### Acquisition estimator

- Enter **Amount paid (fiat)** and **P2P unit price (fiat/USDT)**
- Set **P2P fee %**, **Exchange fee %**, optional **Fixed USDT fee**
- Uses the network fee from the calculator
- Outputs net BTC to wallet, effective entry, and total fees

### PnL

- Add rows with **Amount, Currency, Date, Time (optional), Fee% (optional)**
- Click **Compute** to fetch FX (day) and nearby BTC price
- See **BTC bought, Now value, P/L**, and **totals** by currency

---

## Configuration

Open the HTML and edit these small bits:

- **Currencies:** update `FIATS` to add/remove quote currencies
- **Price symbols:** edit the list under `PricesPage`
- **Default tab:** `const [tab,setTab] = useState('seasonal')`
- **Theme:** saved in `localStorage` as `btctheme`

---

## Deploy

Any static host works.

- **GitHub Pages** — Use `index.html` at repo root.
- **Netlify / Vercel** — Static deploy, no build command
- **Cloudflare Pages** — Same

**Tip:** If TradingView is blank on a custom domain, check ad-blockers, mixed content, and CSP.

---

## Troubleshooting

- **Nothing loads from file URL** → Serve via `http://localhost:8080`
- **CORS errors** → Enable the **CORS proxy** switch
- **TradingView blank** → Ensure online, try another browser, disable content blockers; tv.js often requires a secure origin
- **Gaps in FX** → The app walks back a few days; try again if a source is down

---

## Security & privacy

- All logic runs **client-side**
- When proxy is enabled, requests go via **corsproxy.io** — use only if needed

---

## Tech stack

- **React 18** (UMD)
- **TradingView** Lightweight Charts + Advanced Chart widget
- **Plain CSS** with CSS variables
- **No bundler, no build**

---

## License

- **App code:** MIT  
- **TradingView tv.js / widget:** subject to TradingView terms  
- **API data:** respect providers’ rate limits & terms

---

## Contributing

PRs welcome!

- Keep it **single-file** and dependency-free
- Add features behind clear toggles
- Match design tokens, spacing, and style

---

## Acknowledgements

- TradingView for charts
- Binance, Coinbase, mempool.space, Blockstream, exchangerate.host, fawazahmed0 currency API (jsDelivr/GitHub), open.er-api for public endpoints

*Enjoy the charts.*
