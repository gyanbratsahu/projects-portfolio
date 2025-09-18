# Trade Analysis Tools — README

> **Quick note (read first)**
>
> Thank you for looking at this project. These tools were developed as *contract work* for a company, so the original source code is proprietary and cannot be shared. What I can provide here (and have provided) are **Windows executables (.exe)** packaged in `.zip` files that demonstrate the core MVP features I implemented. The README below describes what each executable does, how to evaluate it, what to look for as a recruiter or reviewer, and a short, honest account of constraints and next steps.

---

## Table of contents

1. Project snapshot
2. What’s included
3. Quick start (run and test)
4. Deep-dive: features & flows

   * a. `dashboard_login.zip` (UID/MAC-locked, login / registration)
   * b. `data_fetch_nologin.zip` — SmartAPI fetcher (no login)
   * c. `dashboard_nologin.zip` — interactive analysis dashboard (no login)
5. Screenshots (key views)
6. How interviewers should evaluate this
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

Because this was built for a client as contract work, the deliverables you will see are packaged executables (MVPs) in `.zip` files rather than source repositories.

---

## 2) What’s included (delivered files you should have)

* `dashboard_login.zip` — **login / registration required** (UID + MAC-based key tied to device). Demonstrates device-level licensing.
* `data_fetch_nologin.zip` — lightweight SmartAPI data fetcher where you provide `from`/`to` dates, timeframe (1min/3min/5min/etc.), SmartAPI symbol token and an output filename. Produces CSV output.
* `dashboard_nologin.zip` — interactive dashboard that accepts a specific trade file format (see notes below) and generates the charts shown in screenshots.

---

## 3) Quick start (run & test — interviewer friendly)

**Environment:** Windows 10/11 machine (executables built for Windows). The tools are local web apps and open a browser page at `127.0.0.1:5000`.

**Steps I recommend for a quick review:**

1. Extract the supplied `.zip` files into a folder (e.g., `C:\TradeTools\`).
2. **Login-demo:** Launch from `dashboard_login.zip` (this demonstrates the UID+MAC lock). The app will show a small registration/login card with local UID/key request.
3. **Data fetch (no-login):** Launch from `data_fetch_nologin.zip`. Provide `from` and `to` dates, select a timeframe, enter a SmartAPI symbol token, and choose an output filename. Click `Fetch` — the app will produce a CSV.
4. **Dashboard:** Launch from `dashboard_nologin.zip`, upload the CSV produced in step 3 (or a compatible trades file). The dashboard will analyze the file and present metrics and interactive charts.

---

## 4) Deep-dive: features & flows

### a) `dashboard_login.zip` — UID/MAC-locked registration (why and what to expect)

* Purpose: demonstrate a licensing/usage lock that ties a generated key to the machine UID/MAC. The app asks for a registration `Key:` based on the displayed UID so the executable cannot be copied across machines.
* What you will see: a minimal registration card that shows `Your UID: <UID string>` and a `Key:` input. If a license is expired, the app will show a polite message and block functionality. Example screenshot:

<img width="1920" height="865" alt="Screenshot (141)" src="https://github.com/user-attachments/assets/4a00feac-fffc-4677-9b94-b69a90d11eb8" />


*Caption:* The UID/MAC-registration view. The key field is tied to the device UID/MAC which restricts copying.

### b) `data_fetch_nologin.zip` — SmartAPI fetcher

* Purpose: fetch OHLC/time-series/tick-like data for a symbol over a date range at a chosen timeframe.
* Inputs: `from date`, `to date`, `timeframe` (1min, 3min, 5min, ...), **SmartAPI symbol token**, and `output filename`.
* Output: CSV containing the collected bars/ticks for the period.

### c) `dashboard_nologin.zip` — interactive analysis dashboard

* Purpose: allow a reviewer to drop in a trade/export file and see a structured post-trade analysis (P/L, drawdown, win/loss counts, distribution by holding period, buying time ranges, and calendar-based slicing).
* File expectation: a simple trade-log CSV with buy/sell events or paired trade rows. The dashboard will try to pair buy & sell rows automatically.

Screenshots below show the overview, trading metrics panel, drawdown chart, trade mix, and profit-by-day visualizations.

<img width="1920" height="857" alt="Screenshot (142)" src="https://github.com/user-attachments/assets/4127ba69-a884-4914-9e75-fefb7a81f2b3" />
<img width="1920" height="868" alt="Screenshot (143)" src="https://github.com/user-attachments/assets/d5f137c8-809c-44e2-85d7-52a0f3d0d955" />
<img width="1920" height="867" alt="Screenshot (144)" src="https://github.com/user-attachments/assets/1e59730b-6740-4d3b-986f-a668ee08532e" />
<img width="1920" height="863" alt="Screenshot (145)" src="https://github.com/user-attachments/assets/735a6030-6a49-4358-b6a2-0e3f4be09445" />
<img width="1920" height="868" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/a8c575e3-a99e-4a4f-8214-2f98cf31f27a" />


---

## 5) How interviewers should evaluate this

Focus on:

* **Core logic**: trade pairing, P/L, ROI, drawdowns, and holding period metrics.
* **Data pipeline**: Fetch → Normalize → Store → Analyze → Visualize.
* **Packaging choices**: Why UID/MAC lock for licensing.
* **Dashboard UX**: calendar filtering, interactive charts, error handling.
* **Scalability**: potential extension to real-time, larger datasets, or cloud.

---

## 6) Technical notes & design decisions

* **Local-first app**: packaged as Windows executables spinning up `127.0.0.1:5000` UI.
* **Modular pipeline**: fetcher → normalizer → exporter → dashboard.
* **Dashboard features**: calendar filtering, holding-period bins, drawdown plotting, distribution charts.
* **Security**: UID/MAC lock for client licensing requirements.

---

## 7) Limitations & contractual note

* **Source code not included** — proprietary under client contract.
* `dashboard_login.zip` enforces UID+MAC licensing.
* The dashboard requires a specific file format for trade analysis.

---

## 8) How I contributed

End-to-end delivery:

* pipeline design & file format contract
* fetcher implementation with retry logic
* trade pairing & analytics logic (P/L, drawdowns)
* interactive dashboard with charts & calendar
* packaging as Windows executables

Skills: data engineering, time-series handling, trade analytics, interactive visualization, packaging, pragmatic security.

---

## 9) Next steps (for interview)

I can:

* re-implement key algorithms (drawdown, win rate, etc.) live
* discuss design tradeoffs (local vs. cloud, UID lock vs. token auth)
* explore scaling (real-time ticks, parallel processing)

---

## 10) Contact / closing note

Thanks for reviewing this work. I’ve kept the README practical and honest, with a balance of context and demonstration. In an interview setting, I’d be glad to discuss:

* specific algorithms (drawdowns, P/L, streaks)
* simplified live examples or re-implementations
* design choices, tradeoffs, and possible extensions

Happy to take the conversation in whichever direction is most useful.

<!-- end of README -->
