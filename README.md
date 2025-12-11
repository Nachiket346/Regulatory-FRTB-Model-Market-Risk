Objective:
To build a simplified but realistic FRTB (Fundamental Review of the Trading Book) market risk capital model in Python, using simulated multi-factor risk returns, liquidity-horizon scaling, Expected Shortfall, scenario analysis, and portfolio-level capital aggregation.

Process:
Generate multi-factor market data
Equity, Rates, Credit Spreads, FX, Commodities, and Volatility index simulated through Gaussian daily returns.

Apply Liquidity Horizon Scaling (FRTB-style)
Each factor is scaled using its regulatory liquidity horizon (20d → 120d).

Compute Bucket-level Expected Shortfall
ES(97.5%) is applied on horizon-scaled returns.

Calculate Individual Capital Charges
FRTB capital = ES × Risk Weight × 1.5
(Risk weights defined per factor.)

Perform Scenario Analysis
Shocks applied:
Equity -15%
Rates +200 bps
Oil +25% spike
Weighted portfolio impacts are computed using portfolio factor weights.

Aggregate Portfolio Capital Charge
Sum of individual capital charges to produce total capital requirement.

Results:
| Risk Factor      | LH-Scaled ES | Capital Charge |
| ---------------- | ------------ | -------------- |
| Equity           | 0.05775      | 0.02165        |
| Rates            | 0.04424      | 0.01327        |
| Credit Spread    | 0.08516      | 0.02555        |
| FX Majors        | 0.03241      | 0.00729        |
| Commodity Oil    | 0.13847      | 0.02077        |
| Volatility Index | 0.15820      | 0.02373        |

Interpretation (Quantified & Comparative)
Equity:
ES (0.0577) and capital charge (0.0216) indicate moderate tail risk exposure.
Lower risk intensity than Credit and Vol Index but still a meaningful contributor to overall capital.

Rates:
Low ES (0.0442) and low capital (0.0133), showing minimal sensitivity to rate shocks.
One of the most stable and least risky factors in the portfolio.

Credit Spread:
High ES (0.0852) and highest capital charge (0.02555), making it the strongest driver of capital requirements.
Indicates significant exposure to credit-market tail events.

FX Majors:
Lowest ES (0.0324) and smallest capital charge (0.00729), confirming FX is the least risky factor.
Reflects strong diversification or low portfolio sensitivity to currency moves.

Commodity (Oil):
Very high ES (0.1385), among the most volatile factors.
Capital charge (0.0208) is significant but below Credit/Vol Index due to lower relative weight.

Vol Index:
Highest ES of all factors (0.1582) and a large capital charge (0.02373).
Indicates volatility shocks dominate the portfolio’s tail-risk profile.

Scenario Analysis

Scenario shocks applied with portfolio exposure weights

| Scenario          | Shock Value | Portfolio Weight Adjusted Impact |
| ----------------- | ----------- | -------------------------------- |
| Equity -15% Crash | −0.15       | **−0.0375**                      |
| Rates +200 bps    | −0.02       | **−0.0040**                      |
| Oil +25% Spike    | +0.25       | **+0.0250**                      |


Interpretation:
Equity −15% generates the largest loss (−0.0375), showing extreme sensitivity to equity crashes.
Rates +200bps results in a mild loss (−0.0040), consistent with low rate-risk capital requirements.
Oil +25% Spike creates a positive impact (+0.025), indicating the portfolio benefits from commodity upside exposure.

Techstack:Python,NumPy,Pandas,Matplotlib.

Future Enhancements:
Add FRTB IMA modellability rules (NMRF capital add-on).
Include correlation-driven aggregation instead of simple sums.
Integrate real market data (FX, commodities, CDS, equity indices).
Add PLA (Profit & Loss Attribution) test & backtesting module.
Implement full 5-bucket sensitivities & curvature risk (SA-FRTB).



