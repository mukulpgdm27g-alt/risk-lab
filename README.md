# Portfolio risk lab

A single-page website. Visitors upload an Excel file of daily stock prices and the whole dashboard (returns, beta, VaR, Expected Shortfall, drawdown, efficient frontier, optimiser) is built in their browser. Nothing is uploaded to any server.

## Put it online (GitHub Pages)

1. Create a free GitHub account and click **New repository**. Name it, for example, `risk-lab`. Choose **Public**.
2. Click **Add file → Upload files**. Drag in `index.html` and `risk_lab_template.xlsx` (you can add `risk_lab_sample_data.xlsx` too). Click **Commit changes**.
   - The page file must be named exactly `index.html` and sit at the top level of the repository.
3. Open **Settings → Pages**. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose branch **main** and folder **/ (root)**, then **Save**.
4. Wait about a minute. Your site is at `https://YOUR-USERNAME.github.io/risk-lab/`.
5. The template can also be downloaded at `https://YOUR-USERNAME.github.io/risk-lab/risk_lab_template.xlsx`.

To change anything later, edit or re-upload the file in the repository; the site updates in a minute.

## Use it

1. Open the site. An upload box appears straight away.
2. Drop your Excel file (or click to choose it). The dashboard builds in a few seconds.
3. Use **Upload Excel** in the header to load another file. **Try with the sample data** shows the built-in demo.

## Excel format

| Sheet | What it holds |
|---|---|
| **Prices** | Row 1 headers: `Date`, then one column per stock, and a last column headed `NIFTY`. One row per trading day, oldest first. Daily adjusted closes. |
| **Portfolios** | Row 1 headers `A` and `B`. Exactly 10 tickers under each (A = high risk, B = low risk). Every ticker must be a column in Prices. No ticker in both. |
| **Info** (optional) | `Ticker`, `Name`, `Sector`, `Short name`. |
| **Settings** | `rf_today`, `rf_crisis`, `rf_calm` (annual risk-free rates, e.g. 0.068), `today_years`, `crisis_start`, `crisis_end` (yyyy-mm-dd). Optional `calm_start`, `calm_end`; leave blank and the calmest 252-day window is chosen automatically. |

Rules the site checks: about 800 or more daily rows (3.5 years), the crisis window inside your dates, and the same ticker spelling in every sheet. Rows with no NIFTY price are dropped; a missing stock price is filled from the previous day. If something is wrong, the upload box says what to fix.

## Getting prices

Run this in a Google Colab notebook (first cell: `!pip install yfinance openpyxl --quiet`), after replacing the tickers with yours. Keep `^NSEI` as the index.

```python
import yfinance as yf
from google.colab import files
stocks = ["TICKER1", "TICKER2"]   # NSE tickers without .NS
px = yf.download([s + ".NS" for s in stocks] + ["^NSEI"], start="2018-01-01",
                 auto_adjust=False, progress=False)["Adj Close"]
px.columns = [c.replace(".NS", "") for c in px.columns]
px = px.rename(columns={"^NSEI": "NIFTY"})
px.index.name = "Date"
px.to_excel("prices.xlsx", sheet_name="Prices")
files.download("prices.xlsx")
```

Copy the `Prices` sheet into the template, then fill in Portfolios, Info and Settings.

Educational project, not investment advice.
