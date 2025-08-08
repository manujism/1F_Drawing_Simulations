# 1F_Drawing_Simulations

Comprehensive Explanation of the Code Logic
Purpose
This project is a financial simulation tool that projects a client’s net worth from their current age to a target future age under multiple investment strategies.

It accounts for:

Regular income and expenses (including large one-off expenses)

Market variability and uncertainty (Monte Carlo simulations)

Different investment allocation approaches

The aim is to produce a range of possible outcomes, not a single prediction — enabling strategy comparison and risk evaluation.

1. Inputs & Setup
Key parameters defined at the start:

Time Frame: From the client’s current age (e.g., 30) to the end age (e.g., 55), broken into quarterly periods (e.g., 100 quarters).

Initial Corpus: Starting investment amount (e.g., ₹1.12 Cr).

Investment Strategies: Multiple predefined allocation styles, from conservative to ultra-aggressive.

Simulation Volume:

num_simulations → Number of Monte Carlo runs per strategy (e.g., 10 for testing, thousands for production).

Each run uses different random market conditions.

Why it matters:
This sets the time horizon, starting resources, and investment approaches to be tested.

2. Data Sources
The simulation uses two datasets:

Quarterly Asset Returns
Historical returns for each asset class (Equity, Debt, Alternatives).

If missing, realistic dummy data is generated.

Quarterly Income & Expenses
Quarterly records of income and spending.

Net Cash Flow = Income − Expenses.

Large expenses appear as negative Net Cash Flow values.

Why it matters:
Both market performance and lifestyle costs affect net worth growth.

3. Simulation Logic
The run_monte_carlo_simulation() function executes the core model.

Steps per strategy and run:

Portfolio Initialization

Split the initial corpus into asset classes according to the starting allocation.

Quarter-by-Quarter Loop

Retrieve the quarter’s Net Cash Flow.

If positive → invest according to SIP allocation.

If negative → withdraw proportionally from all assets.

Apply random market returns by selecting a historical quarter’s return (with replacement) for each asset.

Update asset values and recalculate total corpus.

If corpus < 0 → set to 0.

Result Storage

Final corpus at end age.

Entire growth path of corpus.

Final asset breakdown.

Why it matters:
Mimics real-world conditions — income fluctuations, volatility, and withdrawals for big costs.

4. Running Across All Strategies
Iterate over each predefined strategy.

Keep the same starting allocation but vary the SIP allocation for new investments.

Store results for later analysis.

5. Analysis & Risk Metrics
For each strategy, calculate:

Mean & median final corpus

Volatility (standard deviation)

5th & 95th percentile outcomes (worst/best case)

Probability of ending below starting corpus

Sharpe Ratio (return vs total risk)

Sortino Ratio (return vs downside risk)

Why it matters:
Evaluates both return potential and risk profile.

6. Net Worth Breakdown
Show starting allocation in currency terms.

Show average final allocation after simulations.

Highlights portfolio drift over time due to returns and withdrawals.

7. Visualizations
For each strategy:

Histogram of final corpus outcomes.

Growth path chart:

Median line

Shaded 5th–95th percentile range

Why it matters:
Graphs make it easy to spot stable vs volatile strategies.

8. Treatment of Large Expenses
No special handling — part of Net Cash Flow.

If expenses exceed income:

Net Cash Flow becomes negative.

Investments are liquidated proportionally to cover the gap.

Impact:

Immediate corpus drop.

Possible sale of high-return assets.

Reduced compounding potential.

Multiple large events can significantly impact long-term results.

Key Takeaways
What it does:
Tests multiple investment strategies under realistic conditions, combining market volatility with personal cash flow.

Why it’s valuable:
Provides statistical & visual insights for comparing strategies.

Realism:
Uses historical market data and realistic income-expense records.

Decision-making:
Helps select an investment mix balancing growth and resilience.
