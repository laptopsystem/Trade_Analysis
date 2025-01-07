# Binance Account Performance Analysis

## Overview

This analysis aims to evaluate the financial performance of Binance accounts based on historical trade data. Key performance metrics were calculated for each account, and the accounts were ranked accordingly. The top 20 accounts, based on performance, were identified for further analysis. 

## Methodology

The following steps were followed to conduct the analysis:

### 1. Data Loading and Cleaning

- The dataset (`trade.csv`) was loaded and cleaned.
- The `timestamp` column was converted to a `datetime` format, and rows with invalid timestamps were removed.
- The `Trade_History` column, which contains historical trades, was exploded into individual trades and normalized into a structured DataFrame.
- Invalid or missing `Trade_History` entries were handled using a safe parsing function (`ast.literal_eval`), and rows with invalid data were dropped.

### 2. Feature Engineering

- A new column `position` was created by combining `side` (BUY/SELL) and `positionSide` (LONG/SHORT). This helps identify whether a trade is an opening or closing position.
- Key metrics were derived from the trade data:
  - **ROI (Return on Investment)**: Calculated as net profit over total investment for an account.
  - **PnL (Profit and Loss)**: The total sum of realized profits for an account.
  - **Sharpe Ratio**: A risk-adjusted performance measure, calculated using daily returns.
  - **MDD (Maximum Drawdown)**: The maximum loss from the peak of cumulative profit.
  - **Win Rate**: The percentage of profitable trades compared to total trades.
  - **Win Positions**: The count of profitable trades (where `realizedProfit > 0`).

### 3. Ranking Algorithm

For each account, a composite score was assigned based on the weighted values of the following metrics:
- **ROI** (weight: 40%)
- **Sharpe Ratio** (weight: 30%)
- **Win Rate** (weight: 20%)
- **MDD** (weight: 10%)

Accounts were ranked based on this score in descending order to identify the top performers.

### 4. Output

- The calculated metrics were saved to a CSV file called `Calculated_Metrics.csv`.
- The top 20 ranked accounts were displayed for further analysis and reporting.

## Findings

### 1. Top 20 Accounts

The top 20 accounts were identified based on their composite score, which combined ROI, Sharpe Ratio, Win Rate, and MDD. Accounts with:
- Higher ROI, greater Sharpe Ratios, and minimal MDDs (low drawdowns) performed well in the ranking.
- Higher Win Rates correlated with better performance, as profitable accounts consistently made successful trades.

### 2. Insights from Metrics

- **ROI**: Accounts with the highest ROI were able to generate significant profit from their investments, indicating strategic and profitable trading.
- **Sharpe Ratio**: Accounts with a higher Sharpe Ratio not only made profits but did so efficiently with smaller risks, maintaining consistent returns.
- **Win Rate**: Accounts with a higher Win Rate had more profitable trades, reflecting their ability to make successful trading decisions.
- **MDD**: Accounts with smaller MDD (drawdowns) were ranked higher, showing better risk management and less volatility in returns.
- **Win Positions**: Accounts with a higher Win Rate and ROI had more profitable trades, indicating a robust and consistent trading approach.

## Assumptions

1. **Data Quality**:
   - The dataset is assumed to be accurate and complete, with no prominent data issues outside of what was handled in the cleaning process (e.g., missing `timestamp`, invalid `Trade_History` entries).
   - The `realizedProfit` values are assumed to represent actual profit or loss generated from each trade.

2. **Position Classification**:
   - Trades were classified based on `side` (BUY/SELL) and `positionSide` (LONG/SHORT).
   - It is assumed that `side` indicates the direction of the trade, whether it is opening or closing a position.

3. **Trade Data Interpretation**:
   - `quantity` was treated as the notional value of the trade, and `qty` was treated as the notional coin amount used in the trade.
   - The `realizedProfit` column was used to identify Win Positions, with any trade having positive realized profit being classified as a win.

4. **Risk-Free Rate**:
   - For the computation of the Sharpe Ratio, a zero risk-free rate was assumed due to lack of specific information about a risk-free rate in the dataset.

## Conclusion

This analysis calculated major performance metrics for each account and ranked them based on financial performance. The methodology focused on ROI, Sharpe Ratio, Win Rate, and MDD to identify the top 20 accounts showing regular profitability and sound risk management. These results provide valuable insights into the trading strategies of the top performers.

## Files

- `trade.csv`: The original dataset containing the historical trade data.
- `Calculated_Metrics.csv`: The CSV file containing the calculated metrics for each account.
- Top 20 Ranked Accounts: Displayed for further reporting and analysis.
