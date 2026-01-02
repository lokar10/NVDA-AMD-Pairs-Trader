![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# NVDA-AMD-Pairs-Trader 📈

A Python-based **Statistical Arbitrage** (Pairs Trading) bot that trades the price relationship between **NVIDIA (NVDA)** and **AMD**. This project uses cointegration and mean reversion to identify and trade price inefficiencies between the two semiconductor giants.

## 🧠 Strategy Overview
Pairs trading is a market-neutral strategy. Instead of betting on whether the market goes up or down, this bot bets that the historical relationship between NVDA and AMD will persist.

### The Math behind the Bot:
1. **Cointegration:** We use the Engle-Granger two-step method to ensure the pair shares a long-term equilibrium.
2. **Hedge Ratio ($\beta$):** Calculated using Ordinary Least Squares (OLS) regression:
   $$Price_{NVDA} = \alpha + \beta \cdot Price_{AMD} + \epsilon$$
3. **The Spread:** The residual ($\epsilon$) represents the price spread:
   $$Spread = Price_{NVDA} - (\beta \cdot Price_{AMD})$$
4. **Z-Score:** We normalize the spread to identify entry/exit signals:
   $$Z = \frac{Spread - \mu}{\sigma}$$

## 🛠️ Tech Stack
* **Python 3.x**
* **yfinance** - Financial data extraction
* **statsmodels** - Cointegration tests & OLS regression
* **pandas/numpy** - Vectorized data manipulation
* **matplotlib** - Performance visualization

## 📊 Strategy Results

## 1. 🔍 Initial Data & Statistical Testing

Before generating signals, the bot downloads historical adjusted closing prices and performs an initial check for cointegration. This ensures the two assets have a stable long-term relationship.

<img width="337" height="197" alt="pairsbotinitaldata2" src="https://github.com/user-attachments/assets/2bfb2717-2a60-4143-9668-74a62ac09546" />


### The Cointegration Test
The bot runs the **Engle-Granger test** to check if the spread is stationary. 
* **P-Value Output:** In the sample run above, the p-value was `0.9852`. 
* **Interpretation:** A high p-value suggests that over this specific short window, the pair is "decoupled." The bot uses this metric to determine if the relationship is strong enough to trade.

### 2. Performance Visualization
The following charts illustrate the bot's decision-making process. The **Top Chart** tracks the Z-Score relative to our $\pm 2.0$ thresholds. The **Bottom Chart** tracks the growth of the strategy's cumulative returns.

<img width="1189" height="790" alt="pairsbotcharts" src="https://github.com/user-attachments/assets/92a6c86f-a1dd-490d-b8ea-610ac13f13b6" />

## 🚀 How to Use
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/lokar10/NVDA-AMD-Pairs-Trader.git](https://github.com/lokar10/NVDA-AMD-Pairs-Trader.git)
2. **Install dependencies:**
   ```bash
   pip install yfinance statsmodels pandas matplotlib
3. **Run the script:**
   ```bash
   Pairs_Bot_NVIDIA_vs_AMD.ipynb

---



## ⚠️ Disclaimer

**This project is for educational and research purposes only.** * **Not Financial Advice:** The software and information provided in this repository are not intended to be investment, tax, or financial advice. 
* **High Risk:** Algorithmic trading involves significant risk of loss. Statistical relationships that existed in the past (like cointegration between NVDA and AMD) may break down at any time.
* **No Guarantees:** Past performance is not indicative of future results. The backtest results shown are hypothetical and do not account for slippage, transaction costs, or market liquidity.
* **Use at Your Own Risk:** The author is not responsible for any financial losses incurred from the use of this code. Always perform your own due diligence before trading with real capital.
