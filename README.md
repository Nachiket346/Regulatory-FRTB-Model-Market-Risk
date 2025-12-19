Objective
Designed and implemented a simplified yet regulatorily consistent FRTB market risk capital model, incorporating Expected Shortfall (ES 97.5%), liquidity horizon scaling, multi-factor risk aggregation, and stress/scenario analysis, to estimate portfolio-level capital requirements under tail risk conditions.

Methodology
Simulated multi-factor market risk returns across Equity, Rates, Credit Spreads, FX, Commodities, and Volatility, aligned with FRTB risk class structure.
Applied FRTB-style Liquidity Horizon (LH) scaling (20d–120d) to capture liquidity-adjusted tail risk per risk factor.
Computed Expected Shortfall (97.5%) on horizon-scaled returns, consistent with Basel III / FRTB ES standards.
Calculated individual capital charges using regulatory-style formulation:
Capital = ES × Risk Weight × Capital Multiplier (1.5).
Performed scenario-based stress testing (equity crash, rate shock, commodity spike) to assess portfolio P&L sensitivity under extreme but plausible conditions.
Aggregated portfolio capital requirement through factor-level capital summation, serving as a baseline FRTB aggregation approach.

Tech Stack:Python,NumPy,Pandas,Matplotlib.

Results

FRTB Capital Results (Liquidity-Horizon Scaled)
| Risk Factor      | LH-Scaled ES | Capital Charge |
| ---------------- | -----------: | -------------: |
| Equity           |      0.05775 |        0.02165 |
| Rates            |      0.04424 |        0.01327 |
| Credit Spread    |      0.08516 |        0.02555 |
| FX Majors        |      0.03241 |        0.00729 |
| Commodity (Oil)  |      0.13847 |        0.02077 |
| Volatility Index |      0.15820 |        0.02373 |

Interpretation:
Credit Spread and Volatility dominate capital consumption, contributing the highest capital charges (0.0256 and 0.0237), despite lower volatility than Commodities, highlighting ES sensitivity to tail losses rather than average risk.
Volatility risk exhibits the largest tail exposure with ES of 0.1582, nearly 2.7× higher than Equity ES (0.0578), confirming volatility shocks as the primary driver of extreme portfolio losses.
Equity risk contributes moderate capital (0.0217), materially below Credit and Volatility, indicating meaningful exposure but better diversification relative to tail-heavy factors.
Rates and FX are structurally low-risk, with combined capital of 0.0206 (<25% of total capital), validating their stabilizing role under FRTB liquidity-adjusted ES.

Scenario Analysis – Portfolio Impact
| Scenario          | Shock Value | Portfolio Weight–Adjusted Impact |
| ----------------- | ----------: | -------------------------------: |
| Equity −15% Crash |       −0.15 |                      **−0.0375** |
| Rates +200 bps    |       −0.02 |                      **−0.0040** |
| Oil +25% Spike    |       +0.25 |                      **+0.0250** |

Interpretation:
Equity −15% stress produces the largest portfolio loss (−3.75%), exceeding rate shock losses by ~9×, confirming equity downside as the dominant directional risk.
Rates +200 bps shock results in a limited loss (−0.40%), consistent with its low ES (0.0442) and minimal capital allocation.
Oil +25% spike generates a positive P&L impact (+2.5%), demonstrating asymmetric commodity exposure and partial natural hedging within the portfolio.
Scenario results align with ES-based capital rankings, reinforcing consistency between distribution-based tail risk measures and deterministic stress outcomes.

Future Enhancements
Implement NMRF (Non-Modellable Risk Factor) capital add-ons and data sufficiency tests.
Replace simple aggregation with correlation-based FRTB aggregation.
Integrate real market data (CDS, FX forwards, equity indices, commodities).
Add PLA testing and backtesting framework for IMA eligibility.
Extend to SA-FRTB sensitivities, curvature risk, and bucket-level capital.

Key Insights
FRTB Expected Shortfall materially reallocates capital away from low-volatility assets toward tail-risk-intensive factors, particularly Credit and Volatility.
Liquidity Horizon scaling is a critical capital amplifier, especially for illiquid risk factors, and materially changes risk rankings versus VaR-based frameworks.
Scenario analysis complements ES by exposing directional vulnerabilities (e.g., equity crashes) that pure distribution-based metrics may understate.
The framework demonstrates how portfolio composition, not just volatility, drives regulatory capital, aligning with real-world FRTB desk-level risk management.






