# Phase 1 – Beginner Fintech & Market Data

**Goal:** Get comfortable with Python, APIs, and basic market concepts using real assets.

---

## 📋 Learning Checklist

- [ ] Understand Python functions and modules
- [ ] Work with JSON data
- [ ] Make HTTP requests to multiple APIs
- [ ] Fetch stock prices (NVDA, AMD, TSLA, etc.)
- [ ] Fetch crypto prices (HYPE, SOL, BTC, ZEC)
- [ ] Understand OHLCV data (Open, High, Low, Close, Volume)
- [ ] Calculate simple PnL (Profit and Loss)
- [ ] Save data to CSV files
- [ ] Handle API errors gracefully

---

## 📚 Lessons

### 1. Python Functions & Modules

**What you'll learn:**
- Creating functions with def
- Function parameters and return values
- Importing modules
- Installing packages with pip

**Example:**
```python
def fetch_price(symbol):
    """Fetch the current price for a symbol"""
    # API call logic here
    return price

# Import a module
import requests
```

---

### 2. Working with JSON

**What you'll learn:**
- Understanding JSON structure
- Parsing JSON responses
- Accessing nested data
- Converting between JSON and Python dicts

**Example:**
```python
import json

# Parse JSON string
data = json.loads('{"symbol": "BTC", "price": 50000}')
print(data['price'])  # 50000
```

---

### 3. HTTP Requests & APIs

**What you'll learn:**
- Using the `requests` library
- GET requests with parameters
- Reading response status codes
- Handling API authentication

**Example:**
```python
import requests

response = requests.get('https://api.example.com/price',
                       params={'symbol': 'NVDA'})
if response.status_code == 200:
    data = response.json()
```

---

### 4. Stock Market Basics

**What you'll learn:**
- Stock symbols/tickers
- Bid/ask spreads
- Market vs. limit orders
- OHLCV candles
- Market hours

**Key Terms:**
- **Ticker:** Symbol representing a stock (e.g., NVDA, TSLA)
- **OHLCV:** Open, High, Low, Close, Volume
- **PnL:** Profit and Loss
- **Position:** Shares you own

---

### 5. Crypto Market Basics

**What you'll learn:**
- Crypto tickers (BTC, SOL, HYPE, ZEC)
- Spot vs. perpetual futures
- 24/7 trading
- Funding rates (for perps)

**Key Differences from Stocks:**
- No market hours (24/7)
- Higher volatility
- Different trading venues
- Perpetual futures (no expiry)

---

### 6. Options Basics

**What you'll learn:**
- Calls vs. puts
- Strike price and expiration
- Options Greeks (Delta, Gamma, Theta, Vega)
- Premium and intrinsic value

**Key Terms:**
- **Call:** Right to buy at strike price
- **Put:** Right to sell at strike price
- **Strike:** Price at which option can be exercised
- **Premium:** Cost of the option

---

### 7. Free API Resources

**Stock/Options APIs:**
- Alpha Vantage (get free API key)
- yfinance (no key needed!)
- Polygon.io (free tier)

**Crypto APIs:**
- CoinGecko (free API)
- Hyperliquid public endpoints
- CryptoCompare (free tier)

**Getting Started:**
```python
# Example: Using yfinance (easiest to start)
import yfinance as yf

ticker = yf.Ticker("NVDA")
data = ticker.history(period="1d")
print(data)
```

---

### 8. Environment Variables

**What you'll learn:**
- Storing API keys securely
- Using .env files
- The python-dotenv library
- Never committing secrets to git

**Setup:**
```bash
pip install python-dotenv
```

**Create `.env` file:**
```
ALPHA_VANTAGE_KEY=your_key_here
COINGECKO_KEY=your_key_here
```

**Load in Python:**
```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv('ALPHA_VANTAGE_KEY')
```

---

### 9. Error Handling

**What you'll learn:**
- Try/except blocks
- Handling network errors
- API rate limits
- Logging errors

**Example:**
```python
try:
    response = requests.get(url)
    response.raise_for_status()
    data = response.json()
except requests.exceptions.RequestException as e:
    print(f"Error fetching data: {e}")
```

---

### 10. Data Storage Basics

**What you'll learn:**
- Writing to CSV files
- Reading from CSV files
- Using pandas (optional but helpful)
- Organizing data files

**Example:**
```python
import csv

# Write to CSV
with open('prices.csv', 'w', newline='') as f:
    writer = csv.writer(f)
    writer.writerow(['symbol', 'price', 'timestamp'])
    writer.writerow(['BTC', 50000, '2024-01-01'])
```

---

## 🎯 Projects

See `/projects/phase1/` for hands-on projects:

1. **multi-asset-price-watcher** - Fetch real-time prices for stocks and crypto
2. **portfolio-tracker** - Track a mock portfolio's value and PnL
3. **ohlcv-downloader** - Download and save historical candle data

---

## 📖 Recommended Learning Path

**Week 1-2:** Python fundamentals, APIs, JSON
- Complete lessons 1-3
- Start hello-python-cli project
- Make your first API call

**Week 3-4:** Market basics and data fetching
- Complete lessons 4-7
- Build multi-asset-price-watcher
- Get API keys for free services

**Week 5-6:** Data management and project completion
- Complete lessons 8-10
- Build portfolio-tracker
- Build ohlcv-downloader

---

## 📝 Project Ideas (Beyond Required)

Once you complete the core projects, try:

- **Price Alert System:** Send yourself an alert when a stock hits a target price
- **Correlation Tracker:** Track correlation between BTC and tech stocks
- **Sector Dashboard:** Show all HPC/AI stocks performance for the day
- **Crypto Dominance:** Track BTC dominance vs. alts
- **Options Scanner:** Find options with high IV or unusual volume

---

## ✅ Phase Completion Criteria

You're ready for Phase 2 when you can:

- [ ] Fetch stock prices from a free API
- [ ] Fetch crypto prices from a free API
- [ ] Parse JSON responses and extract data
- [ ] Store data in CSV files
- [ ] Calculate simple PnL on a mock portfolio
- [ ] Handle API errors without crashes
- [ ] Use environment variables for API keys
- [ ] Explain OHLCV data
- [ ] Understand the difference between stocks, options, and crypto

---

## 🔑 Key Concepts Mastered

By the end of Phase 1, you should understand:

- **Technical:** HTTP requests, JSON, CSV files, error handling
- **Markets:** Stocks, options, crypto differences
- **Data:** OHLCV candles, tickers, price data
- **Workflow:** API keys, rate limits, data storage

---

## 🆘 Getting Help

- **Can't connect to API?** Check your API key and rate limits
- **JSON confusing?** Use online JSON formatters to visualize structure
- **Code not working?** Ask AI to explain each line
- **Stuck on project?** Break it into smaller pieces

**Remember:** Real-world APIs are messy. Learning to handle errors and edge cases is part of the process!
