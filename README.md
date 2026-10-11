# Portfolio Risk Lab: A vs B

**Does a risk label survive a crash?** An interactive dashboard for FRA Group Project 1.

Two ₹15 lakh portfolios of 10 stocks each (no overlap): **A** is high risk, **B** is low risk. The dashboard tests:

1. **The call:** why A is high risk and B low risk (beta and standard deviation, with the full calculation shown step by step).
2. **Test 1, the risk label:** one-day VaR and Expected Shortfall (90%, 95% or 99%) for both portfolios in a crisis (2020), a calm year, and today.
3. **Test 2, the allocation:** at today's return, would the efficient frontier rebuilt from each era's data pick the same weights?

## Live site
`https://<your-username>.github.io/<repo-name>/` (replace after publishing)

## Run locally
Open `index.html` in a browser. It is a single self-contained file (data and charts included), so it needs no server, install or internet connection.

## Controls
Portfolio (A/B), period (Today / Crisis 2020 / Calm year), VaR confidence (90/95/99%), weight limits (none or 5% to 50% per stock), and the investment amount.

## Data and assumptions
- Daily adjusted closing prices (Yahoo Finance), 20 stocks and Nifty 50, 2018 to October 2026.
- Historical one-day VaR and ES; portfolios rebalanced daily to fixed weights.
- Risk-free rate: India 10-year government bond yield, by era.

## Team
- Mukul Singh
- Manik Ratty
- Pari Aggarwal
- Kanika Khandelwal
- Venu Pratap Singh

*Educational project, not investment advice.*
