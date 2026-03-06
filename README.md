# Portfolio Tracker

A local, self-hosted portfolio tracker for Indian investors. Track stocks, ETFs, gold ETFs, mutual funds, crypto, Provident Fund contributions, and Fixed Deposits — all in one place with live prices and historical charts.

![Python](https://img.shields.io/badge/Python-3.8+-blue) ![Flask](https://img.shields.io/badge/Flask-Backend-green) ![License](https://img.shields.io/badge/License-MIT-yellow)

## Features

### Asset Types
- **Stocks & ETFs** — NSE/BSE listed equities and ETFs (live prices via Yahoo Finance)
- **Gold ETFs** — Tracked separately for allocation visibility
- **Mutual Funds** — NAV fetched from mfapi.in, search by name or scheme code
- **Crypto** — Live prices via CoinGecko API (INR)
- **Provident Fund** — Monthly contribution tracking with configurable interest rate and annual compounding
- **Fixed Deposits** — Principal, rate, tenor with monthly/quarterly/half-yearly/yearly compounding options

### Portfolio Dashboard
- Total portfolio value, total invested, and gain/loss summary
- Pie chart breakdown by asset category
- Filter investments by **Current / Past / All**
- Manual price refresh
- INR default with USD conversion toggle

### Historical Charts
- **Portfolio Value** — Two-line chart showing portfolio value vs amount invested over time, making profit/loss visible at a glance
- **Returns %** — Percentage return over time with a 0% baseline
- **Current Holdings** — What your current holdings would have been worth historically (backwards projection)
- **Inflation adjustment** toggle using World Bank India CPI data (with extrapolation for recent years)

### Import
- Import Zerodha tradebook CSVs (both EQ and MF segments)
- Auto-classifies stocks vs ETFs vs gold ETFs
- Resolves mutual fund ISINs via AMFI data
- Duplicate trade detection using Zerodha trade IDs
- Multi-file upload support

### Investment Management
- Add investments manually with ticker/fund search
- Investments with the same ticker/fund are automatically merged
- Add, edit, and delete individual transactions
- Edit investment-level details (name, type, ticker)
- Transactions sorted newest-first

## Tech Stack

- **Backend:** Python Flask with JSON file storage (`portfolio.json`)
- **Frontend:** Single-page HTML with vanilla JS, Chart.js, and Flatpickr
- **APIs:**
  - Yahoo Finance v8 (stocks/ETFs — fetched via `curl` to avoid TLS blocking)
  - [mfapi.in](https://www.mfapi.in/) (mutual fund NAV and history)
  - [AMFI India](https://www.amfiindia.com/) (ISIN to scheme code mapping)
  - [CoinGecko](https://www.coingecko.com/en/api) (crypto prices, free tier — 365-day history limit)
  - [World Bank](https://data.worldbank.org/) (India CPI for inflation adjustment)
  - [ExchangeRate API](https://open.er-api.com/) (INR/USD conversion)

## Setup

### Prerequisites
- Python 3.8+
- `curl` (used for Yahoo Finance API calls)

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/portfolio-tracker.git
cd portfolio-tracker

# Install dependencies
pip install -r requirements.txt

# Run the app
python3 app.py
```

The app runs at `http://localhost:5000`.

### Importing Zerodha Trades

1. Download your tradebook from Zerodha Console (separate CSVs for EQ and MF segments)
2. Click the **Import** button in the app
3. Select one or more CSV files and import
4. Duplicates are automatically skipped based on trade IDs

## Data Storage

All portfolio data is stored locally in `portfolio.json`. No data is sent to any server — API calls are only made to fetch live/historical prices.

## Future Plans

- **Automated SIP tracking** — Define SIP schedules (amount, frequency, start date) and auto-generate recurring transactions
- **PF auto-contributions** — Set up monthly PF contribution schedules that automatically add entries each month
- **FD maturity alerts** — Notifications when FDs are approaching maturity
- **Benchmarking** — Compare portfolio returns against Nifty 50, Sensex, or other indices
- **XIRR calculation** — Annualized returns accounting for irregular cash flows
- **Asset rebalancing suggestions** — Target allocation vs actual allocation with rebalance recommendations
- **Export** — Download portfolio data as CSV/Excel
- **Multi-portfolio support** — Track separate portfolios (e.g., personal, family)
- **Groww/Kite API integration** — Auto-sync trades from broker accounts
- **Tax reporting** — Capital gains summary for ITR filing (STCG/LTCG breakdowns)
- **Dividend tracking** — Record and track dividend income from stocks and mutual funds
- **Graph Filters** - More filters on graphs to view performance over the past year, month, etc.

## License

MIT
