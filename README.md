projects-portfolio

Automation projects delivered as part of contractual work

⚠️ Quick note
These tools were developed as contract work, so the original source code cannot be shared. Instead, I’ve provided Windows executables (.exe) that demonstrate the MVP features.

Please do not use the login-locked executable (dashboard_login.zip) — it requires a device-specific key and will not run without activation. Focus on the no-login versions for review.

📑 Table of contents

Project snapshot

Delivered files

Quick start (run & test)

Features & flows

Screenshots

How to evaluate

Technical notes & design decisions

Limitations & contractual note

My contribution

Contact

🚀 1) Project snapshot

A small suite of tools for intraday trade data fetching and post-trade analysis. The pipeline:

Fetches market data (by timeframe)

Ingests a trade log and pairs buys/sells where possible

Computes trading metrics (P/L, drawdown, win rate, holding period, distributions)

Displays results in an interactive dashboard

All packaged as local executables for Windows.

📦 2) Delivered files

dashboard_login.zip – UID + MAC–based lock / registration system.

⚠️ Not usable for recruiters since it requires a license key.

data_fetch_nologin.zip – fetches historical data based on:

from–to date

timeframe (1min/3min/5min, etc.)

SmartAPI symbol token

output filename → produces a CSV.

dashboard_nologin.zip – analysis dashboard (no login required).
Upload a compatible trade file (or CSV from the fetcher) to view metrics and charts.

⚡ 3) Quick start (Windows-friendly)

Place executables in a folder, e.g. C:\TradeTools\.

Run data_fetch_nologin.exe → a local web page opens at http://127.0.0.1:5000/.

Input: date range, timeframe, SmartAPI token, filename → click Fetch. A CSV is saved locally.

Run dashboard_nologin.exe → upload the CSV → interactive charts and metrics appear.

🔎 4) Features & flows
data_fetch_nologin

Inputs: from–to dates, timeframe, SmartAPI token, output file

Output: CSV with OHLC/tick data

dashboard_nologin

Input: trade-log CSV or fetched data

Features:

Total trades, P/L, win rate, ROI

Drawdown visualization

Holding-period & time-of-day distributions

Calendar-based slicing

🖼 5) Screenshots

UID-based registration view (from dashboard_login.zip)
<img width="1920" height="865" alt="Screenshot (141)" src="https://github.com/user-attachments/assets/680e6e50-91fc-42a7-a710-d70a1b554672" />

Dashboard overview & top-level metrics
<img width="1920" height="857" alt="Screenshot (142)" src="https://github.com/user-attachments/assets/6bbb1128-c3a2-42a8-839e-8336d8f6f0d9" />

Trading metrics panel with calendar
<img width="1920" height="868" alt="Screenshot (143)" src="https://github.com/user-attachments/assets/9a126412-c768-4112-8125-45a57461bc49" />

Drawdown and trade mix views
<img width="1920" height="867" alt="Screenshot (144)" src="https://github.com/user-attachments/assets/b7622a8d-07d4-4c50-a32e-2223379e957f" />

Buying distribution and profit-by-day analysis
<img width="1920" height="863" alt="Screenshot (145)" src="https://github.com/user-attachments/assets/31a56e8e-511d-424b-b304-7f9f323cbd10" />

<img width="1920" height="868" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/418f5145-1759-46c5-93b0-93588539dd62" />
✅ 6) How to evaluate

Functionality → fetcher creates CSV → dashboard loads it into charts & metrics

Correctness → confirm buy/sell pairing & P/L against a few rows

Robustness → try malformed files → expect clear error messages

UI/UX → interactive charts, tooltips, calendar filters

Packaging → apps run locally, no installs needed

⚙️ 7) Technical notes

Local-first → executables serve a web UI on 127.0.0.1:5000

Modular pipeline → fetcher → normalizer → exporter → dashboard

Dashboard → exploratory analysis with multiple interactive charts

Packaging → delivered as Windows executables to respect IP boundaries

🚧 8) Limitations & contractual note

No source code included (contractual restriction)

dashboard_login.zip is not usable without a license key (UID/MAC lock)

Dashboard requires a simple trade-log format for correct pairing

🛠 9) My contribution

I designed and built the MVP end-to-end:

Data fetcher with retry logic

Trade pairing, P/L and drawdown calculations

Interactive dashboard with metrics and charts

Packaging as standalone Windows executables

Skills demonstrated:
data engineering (ETL), time-series handling, trade analytics, visualization, packaging, and lightweight licensing logic.

📬 10) Contact

Thanks for reviewing.
In an interview I’d be glad to discuss:

Algorithms behind trade pairing and metrics

Design decisions & tradeoffs

How I’d extend this into a more scalable system
