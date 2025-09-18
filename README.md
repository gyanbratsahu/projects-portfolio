# projects-portfolio
Automation projects done under a contractual work

> **Quick note (read first)**
>
> Thank you for looking at this project. These tools were developed as *contract work* for a company, so the original source code is proprietary and cannot be shared. What I can provide here (and have provided) are **Windows executables (.exe)** that demonstrate the core MVP features I implemented. The README below describes what each executable does, how to evaluate it, what to look for as a recruiter or reviewer, and a short, honest account of constraints and next steps.

---

## Table of contents

1. Project snapshot
2. What’s included
3. Quick start (run and test)
4. Deep-dive: features & flows

   * a. `data_fetcher.exe` (UID-locked, login / registration)
   * b. Data fetch (no-login) — fetch historical ticks / bars
   * c. `dashboard_nologin` — interactive analysis dashboard
5. Screenshots (key views)
6. How recruiters / reviewers should evaluate this
7. Technical notes & design decisions
8. Limitations, security & contractual note
9. How I'd extend this (if given time)
10. Contact / next steps

---

## 1) Project snapshot

This is a small suite of local tools for **intraday trade data fetching and post-trade analysis**. The goal was to produce a lightweight, reliable local pipeline that:

* fetches market data (by timeframe) and stores it to a file
* ingests a trade log and automatically pairs buys/sells where possible
* computes standard trading metrics (P/L, drawdown, win rate, hold-time metrics, distribution charts)
* provides a polished, interactive dashboard for exploratory analysis

Because this was built for a client as contract work, the deliverables you will see are packaged executables (MVPs) rather than source repositories.

---

## 2) What’s included (delivered files you should have)

* `data_fetcher.exe` — **login / registration required** (UID-based key tied to device). This is the one that enforces device-level licensing.
* `data_fetch` (no-login mode) — lightweight data fetcher where you provide `from`/`to` dates, timeframe (1min/3min/5min/etc.), SmartAPI symbol token and an output filename. This will fetch data and save to a CSV.
* `dashboard_nologin.exe` — interactive dashboard that accepts a specific trade file format (see notes below) and generates the charts shown in screenshots.

> Note: filenames may vary slightly depending on the pack delivered. The important part is the behavior described above.

---

## 3) Quick start (run & test — recruiter friendly)

**Environment:** Windows 10/11 machine (executables built for Windows). The tools are local web apps and open a browser page at `127.0.0.1:5000`.

**Steps I recommend for a quick review:**

1. Put the supplied executables in a folder (e.g., `C:\TradeTools\`) and double-click `data_fetcher.exe` (or `dashboard_nologin.exe`). A browser window should open at `http://127.0.0.1:5000/`.

2. **Login-demo:** Launch `data_fetcher.exe` (this demonstrates the UID-based restriction). The app will show a small registration/login card and will display the local UID / key request. (See screenshot below.)

3. **Data fetch (no-login):** Launch the no-login fetcher. Provide `from` and `to` dates, select a timeframe (1min, 3min, 5min, etc.), enter a SmartAPI symbol token (this is the token for the instrument you want to fetch), and choose an output filename. Click `Fetch` — the app will produce a CSV in the local folder.

4. **Dashboard:** Launch `dashboard_nologin.exe`, upload the CSV produced in step 3 (or a compatible trades file). The dashboard will analyze the file and present metrics and interactive charts.

---

## 4) Deep-dive: features & flows

### a) `data_fetcher.exe` — UID-locked registration (why and what to expect)

* Purpose: demonstrate a licensing/usage lock that ties a generated key to the machine UID (or MAC). The app asks for a registration `Key:` based on the displayed UID so the executable cannot be copied and reused across machines with the same username/password.

* What you will see: a minimal registration card that shows `Your UID: <UID string>` and a `Key:` input. If a license is expired, the app will show a polite message and block functionality (this is part of the contract deliverable). Example screenshot:

<img width="1920" height="865" alt="Screenshot (141)" src="https://github.com/user-attachments/assets/680e6e50-91fc-42a7-a710-d70a1b554672" />


*Caption:* The UID-registration view. The key field is tied to the device UID which restricts copying.

### b) Data fetch (no-login)

* Purpose: fetch OHLC/time-series/tick-like data for a symbol over a date range at a chosen timeframe.
* Inputs you provide: `from date`, `to date`, `timeframe` (1min, 3min, 5min, ...), **SmartAPI symbol token**, and `output filename`.
* Output: a CSV (or simple tabular file) containing the collected bars/ticks for the period.

> Example input (for a quick smoke test):
>
> * From: `2024-11-27`
> * To: `2024-11-29`
> * Timeframe: `1min`
> * Symbol token: `12345` (example)
> * Output: `sample_fetch.csv`

---

### c) `dashboard_nologin` — interactive analysis dashboard (what to expect)

* Purpose: allow a reviewer to drop in a trade/export file and see a structured post-trade analysis (P/L, drawdown, win/loss counts, distribution by holding period, buying time ranges, and calendar-selection to slice days).
* File expectation: a restricted/simple trade-log CSV (a single file with buy/sell events or paired trade rows). The dashboard will try to pair buy & sell rows automatically; if the structure differs the UI provides hints or shows mismatches.

Below are representative dashboard screenshots showing:

* overview (total trades, P/L)
* trading metrics panel (total days, ROI, win rate, avg capital employed)
* drawdown chart & trade distribution pie chart
* binning by holding period and buying-time range

<img width="1920" height="857" alt="Screenshot (142)" src="https://github.com/user-attachments/assets/6bbb1128-c3a2-42a8-839e-8336d8f6f0d9" />

*Caption:* Project landing page and top-level metrics, with calendar-based slicing.



<img width="1920" height="868" alt="Screenshot (143)" src="https://github.com/user-attachments/assets/9a126412-c768-4112-8125-45a57461bc49" />

*Caption:* Trading metrics panel and interactive calendar.



<img width="1920" height="867" alt="Screenshot (144)" src="https://github.com/user-attachments/assets/b7622a8d-07d4-4c50-a32e-2223379e957f" />

*Caption:* Drawdown and trade mix views.



<img width="1920" height="863" alt="Screenshot (145)" src="https://github.com/user-attachments/assets/31a56e8e-511d-424b-b304-7f9f323cbd10" />


<img width="1920" height="868" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/418f5145-1759-46c5-93b0-93588539dd62" />

*Caption:* Time-of-day buying distribution and profit-by-day chart.

---

## 5) What to look for as a reviewer (how to evaluate quickly)

If you are short on time, these checks highlight the work behind the deliverable:

* **Functionality**

  * Launch each executable and confirm a local web UI is served at `127.0.0.1:5000`.
  * Test the no-login fetch flow with a short date range and verify a CSV output is generated.
  * Upload the CSV to the dashboard and confirm charts populate, and that metrics (Total P/L, Win Rate, etc.) appear coherent.

* **Data correctness & pairing logic**

  * Inspect a few rows in the uploaded file and confirm buy/sell pairing & P/L calculations match manual calculation.

* **Robustness**

  * Try slightly malformed files (e.g., missing a column) and observe whether the UI shows clear errors or guidance.

* **UI / UX**

  * The dashboard should be interactive: calendar slices should change the charts; hovering on charts should show tooltips.

* **Packaging & deployment**

  * Confirm the app is packaged and runs locally without additional installs (beyond a standard Windows environment).

---

## 6) Technical notes & design decisions (concise)

* **Local-first app**: delivered as Windows executables which spin up a local HTTP UI (browser-based) on `127.0.0.1:5000`. This makes it simple to demo without server infra.
* **Modular pipeline**: data fetcher -> normalizer -> exporter -> dashboard. This separation was intentional so each step can be tested in isolation.
* **Dashboard capabilities**: calendar-based filtering, holding-period bins, drawdown plotting, pie and bar charts for quick distribution analysis.
* **Packaging**: the executables are delivered for convenience and to comply with contractual IP restrictions.

> If you'd like to know exact libraries and architecture (for example, whether this used Flask, Plotly, Chart.js, pandas, PyInstaller, etc.), I can provide a technical walkthrough or reproduce a small reference implementation under an NDA.

---

## 7) Limitations, security & contractual note

* The **source code is not included** here. These were built under a client contract; I can discuss architecture and re-implement small examples on request.
* `data_fetcher.exe` uses a machine UID-based key check. This is by design to prevent unlicensed copying (part of the contract). If you want to test this behavior on a clean machine, I can provide a temporary demo key under a short agreement.
* The dashboard requires a **restricted file format** for automated pairing. This restriction prevents accidental sharing of live client files: if a file is not accepted, the app will show a helpful hint.

---

## 8) How I contributed (concise, recruiter-friendly)

I led the end-to-end delivery of the MVP including:

* designing the ingestion pipeline and the file format contract
* building the fetcher and robust retry logic for short ranges
* implementing trade pairing, P/L and drawdown calculation logic
* creating the interactive dashboard (charts, calendar, and drilldowns)
* packaging the tools as Windows executables for client delivery

Core skills demonstrated: data engineering (ETL), time-series data handling, trade analytics, interactive visualization, product-minded packaging for non-technical users, and pragmatic security (UID-based license).

---

## 10) Contact / closing note

Thanks for reviewing this work. I’ve kept the README practical and honest, with a balance of context and demonstration. In an interview setting, I’d be glad to discuss:

specific algorithms

design choices, tradeoffs, and possible extensions

Happy to take the conversation in whichever direction is most useful.

<!-- end of README -->

