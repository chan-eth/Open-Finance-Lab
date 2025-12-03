# Phase 2 – Intermediate: Strategies & Backtesting

**Goal:** Turn raw data into strategies and test ideas on historical data.

---

## 📋 Learning Checklist

- [ ] Calculate returns and moving averages
- [ ] Implement technical indicators (RSI, MACD, Bollinger Bands)
- [ ] Design a simple stock strategy
- [ ] Design a simple crypto strategy
- [ ] Understand options P&L
- [ ] Build a basic backtester
- [ ] Calculate performance metrics (Sharpe, max drawdown)
- [ ] Implement position sizing rules
- [ ] Model trading costs (fees, slippage)
- [ ] Run and analyze strategy results

---

## 📚 Lessons

### 1. Time Series Basics

**What you'll learn:**
- Price returns (simple vs. log)
- Rolling calculations (moving averages)
- Volatility measures
- Working with pandas DataFrames

**Key Concepts:**
```python
import pandas as pd

# Calculate returns
returns = prices.pct_change()

# Moving average
ma_20 = prices.rolling(window=20).mean()

# Volatility (std dev of returns)
volatility = returns.rolling(window=20).std()
```

---

### 2. Technical Indicators

**What you'll learn:**
- Moving averages (SMA, EMA)
- RSI (Relative Strength Index)
- MACD (Moving Average Convergence Divergence)
- Bollinger Bands
- Volume indicators

**Popular Indicators for Each Asset Class:**

**Stocks (HPC/AI, Robotics):**
- Momentum indicators (RSI, MACD)
- Trend following (moving average crossovers)
- Volume analysis

**Crypto (HYPE, SOL, BTC, ZEC):**
- High volatility → use wider bands
- Funding rates (for perps)
- On-chain metrics (advanced)

**Options:**
- Implied volatility (IV)
- Greeks monitoring
- IV rank/percentile

---

### 3. Stock Trading Strategies

**What you'll learn:**
- Trend following
- Mean reversion
- Momentum strategies
- Sector rotation
- Earnings plays

**Example Strategies:**

**Strategy 1: Moving Average Crossover**
- When fast MA crosses above slow MA → Buy
- When fast MA crosses below slow MA → Sell
- Works on trending stocks (NVDA, AMD)

**Strategy 2: Momentum**
- Buy stocks with strong recent returns
- Hold for fixed period
- Good for HPC/AI sector during bull runs

**Strategy 3: Mean Reversion**
- Buy when price is X% below moving average
- Sell when price returns to average
- Works on less volatile, range-bound stocks

---

### 4. Options Strategies

**What you'll learn:**
- Covered calls
- Cash-secured puts
- Vertical spreads (bull/bear)
- Iron condors (advanced)
- Earnings strategies

**Beginner-Friendly Options Strategies:**

**Covered Calls:**
- Own 100 shares of stock
- Sell call option for premium
- Income generation strategy

**Cash-Secured Puts:**
- Sell put option
- Set aside cash to buy if assigned
- Get paid to potentially buy stocks cheaper

**Simple Spread:**
- Buy one option, sell another
- Defined risk, defined reward
- Lower capital requirement

---

### 5. Crypto Trading Strategies

**What you'll learn:**
- Trend following on high volatility
- Funding rate arbitrage
- Spot-perp arbitrage
- Grid trading
- DCA strategies

**Crypto-Specific Considerations:**
- 24/7 market (no gaps)
- Higher volatility → wider stops
- Funding rates matter (perps)
- Liquidation risks (leverage)

**Example Crypto Strategies:**

**Strategy 1: Trend Following (BTC)**
- Use longer-term MAs (50/200 day)
- Exit on clear trend breaks
- Low frequency trading

**Strategy 2: Funding Arbitrage**
- When funding rate is high → short perp, long spot
- Collect funding payments
- Market neutral strategy

**Strategy 3: Volatility Breakout (HYPE, ZEC)**
- Identify consolidation periods
- Enter on breakout with volume
- Tight stops, good R:R

---

### 6. Backtesting Fundamentals

**What you'll learn:**
- Event-driven backtesting
- Avoiding look-ahead bias
- Position sizing
- Entry and exit rules
- Modeling slippage and fees

**Backtesting Framework:**
```python
# Pseudo-code structure
for each_bar in historical_data:
    # 1. Calculate indicators
    # 2. Generate signals
    # 3. Execute trades (if signal)
    # 4. Update positions
    # 5. Calculate PnL
    # 6. Record metrics
```

**Critical Rules:**
- Only use data available at that point in time
- Include realistic costs (commissions, slippage)
- Don't overfit to historical data
- Test on out-of-sample data

---

### 7. Performance Metrics

**What you'll learn:**
- Total return
- Sharpe ratio
- Maximum drawdown
- Win rate
- Profit factor
- Risk-adjusted returns

**Key Metrics:**

**Returns:**
- Total return: (End - Start) / Start
- Annualized return
- Compound annual growth rate (CAGR)

**Risk:**
- Maximum drawdown: Largest peak-to-trough decline
- Volatility: Std dev of returns
- Sharpe ratio: Return / Risk

**Trade Quality:**
- Win rate: % of winning trades
- Avg win / avg loss ratio
- Profit factor: Gross profit / gross loss

---

### 8. Risk Management

**What you'll learn:**
- Position sizing (fixed % risk)
- Stop losses
- Take profit levels
- Portfolio heat
- Correlation management

**Position Sizing Methods:**

**Fixed Percentage:**
- Risk 1-2% of capital per trade
- Adjust position size based on stop distance

**Volatility-Based:**
- Larger positions in low volatility
- Smaller positions in high volatility

**Kelly Criterion (Advanced):**
- Optimal position size based on win rate and payoff
- Usually too aggressive, use fractional Kelly

**Stop Loss Guidelines:**
- Stocks: 2-5% typical
- Crypto: 5-15% (higher volatility)
- Options: 25-50% of premium paid

---

### 9. Transaction Costs

**What you'll learn:**
- Commissions and fees
- Bid-ask spread
- Slippage
- Market impact
- Modeling costs in backtests

**Cost Breakdown by Platform:**

**Public Brokerage (Stocks/Options):**
- Stock trades: $0 commission
- Options: ~$0.65 per contract
- Spread: Typically tight on liquid stocks

**Hyperliquid (Crypto):**
- Maker: ~0.02% rebate
- Taker: ~0.04% fee
- Funding: Variable (perps)

**Slippage:**
- Small orders (<1% daily volume): Minimal
- Larger orders: Model 0.05-0.2%
- Crypto (low liquidity pairs): Higher

---

### 10. Strategy Development Process

**What you'll learn:**
- Hypothesis formation
- Strategy design
- Parameter selection
- Backtest execution
- Results analysis
- Iteration and improvement

**Development Workflow:**

1. **Research Phase:**
   - Market observation
   - Hypothesis about edge
   - Literature review (optional)

2. **Design Phase:**
   - Define entry rules
   - Define exit rules
   - Position sizing logic
   - Risk controls

3. **Backtest Phase:**
   - Implement in code
   - Run on historical data
   - Check for bugs
   - Review trades manually

4. **Analysis Phase:**
   - Performance metrics
   - Equity curve examination
   - Drawdown analysis
   - Parameter sensitivity

5. **Iteration:**
   - Refine rules
   - Test robustness
   - Out-of-sample validation

---

## 🎯 Projects

See `/projects/phase2/` for hands-on projects:

1. **strategy-lab** - Jupyter notebooks for testing indicators and strategies
2. **backtester-v1** - Build a simple event-driven backtesting engine
3. **paper-trader** - Simulate live trading with real-time prices

---

## 📖 Recommended Learning Path

**Week 1-2:** Technical foundations
- Time series analysis
- Implement 3-5 technical indicators
- Practice with pandas

**Week 3-4:** Strategy design
- Design one stock strategy
- Design one crypto strategy
- Research options strategies

**Week 5-6:** Backtesting
- Build simple backtester
- Test strategies on historical data
- Calculate performance metrics

**Week 7-8:** Refinement
- Improve strategy rules
- Add risk management
- Paper trade strategies

---

## 📊 Suggested Notebook Structure

For `/notebooks/`:

**stocks/:**
- `01_stock_data_analysis.ipynb` - Explore stock price patterns
- `02_indicator_testing.ipynb` - Test various indicators
- `03_momentum_strategy.ipynb` - Develop momentum strategy
- `04_mean_reversion_strategy.ipynb` - Mean reversion tests

**options/:**
- `01_options_basics.ipynb` - Options P&L calculations
- `02_covered_call_analysis.ipynb` - Model covered calls
- `03_spreads_modeling.ipynb` - Vertical spread analysis

**crypto/:**
- `01_crypto_volatility.ipynb` - Analyze crypto volatility
- `02_funding_rates.ipynb` - Funding rate analysis (perps)
- `03_trend_following.ipynb` - Crypto trend strategies
- `04_btc_altcoin_correlation.ipynb` - BTC vs. alts

---

## ✅ Phase Completion Criteria

You're ready for Phase 3 when you can:

- [ ] Calculate returns and indicators from price data
- [ ] Implement at least one stock strategy
- [ ] Implement at least one crypto strategy
- [ ] Understand options P&L
- [ ] Build a basic backtester (even if simple)
- [ ] Calculate Sharpe ratio and max drawdown
- [ ] Apply position sizing rules
- [ ] Model transaction costs
- [ ] Interpret backtest results
- [ ] Identify overfitting vs. robust strategies

---

## 🔑 Key Concepts Mastered

By the end of Phase 2, you should understand:

- **Technical:** pandas, indicators, backtesting frameworks
- **Markets:** Strategy types, asset-specific considerations
- **Risk:** Position sizing, stops, portfolio heat
- **Performance:** Metrics, risk-adjusted returns, trade analysis
- **Process:** Hypothesis → Design → Test → Analyze → Iterate

---

## 🆘 Common Pitfalls

**Overfitting:**
- Too many parameters
- Strategy works perfectly on past data, fails live
- Solution: Keep strategies simple, test out-of-sample

**Look-Ahead Bias:**
- Using future data in calculations
- Solution: Be very careful with indicators, use shift()

**Ignoring Costs:**
- Strategy looks great, but costs kill it
- Solution: Model realistic costs from day one

**Unrealistic Assumptions:**
- Perfect fills, no slippage
- Solution: Be conservative in estimates

**Not Enough Data:**
- Testing on 3 months of data
- Solution: Use at least 1-2 years, ideally more

---

## 📚 Additional Resources

**Books:**
- "Evidence-Based Technical Analysis" - David Aronson
- "Quantitative Trading" - Ernest Chan
- "Trade Your Way to Financial Freedom" - Van Tharp

**Free Online:**
- QuantStart blog
- Quantopian lectures (archived)
- YouTube: QuantPy, Part Time Larry

**Python Libraries:**
- pandas - data manipulation
- numpy - numerical computing
- matplotlib/plotly - visualization
- ta-lib - technical indicators (optional)

---

**Remember:** A simple strategy that you understand is better than a complex one you don't. Start simple, iterate, and gradually add complexity only when needed!
