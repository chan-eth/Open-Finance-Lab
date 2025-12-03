# Multi-Asset Price Watcher

Build a CLI tool that fetches and displays real-time prices for stocks, crypto, and options across multiple assets.

---

## 🎯 Project Goals

- [ ] Fetch stock prices (HPC/AI sector: NVDA, AMD, etc.)
- [ ] Fetch crypto prices (HYPE, SOL, BTC, ZEC)
- [ ] Display prices in a clean, formatted table
- [ ] Add timestamp information
- [ ] Handle API errors gracefully
- [ ] (Optional) Fetch options data

---

## 🎨 Example Output

```
╔══════════════════════════════════════════════════════════╗
║         Multi-Asset Price Watcher                        ║
║         Last Updated: 2024-01-15 10:30:45 EST           ║
╚══════════════════════════════════════════════════════════╝

┌─────────────────────── STOCKS ─────────────────────────┐
│ Symbol  │  Price    │  Change   │  Change %  │  Volume │
├─────────┼───────────┼───────────┼────────────┼─────────┤
│ NVDA    │  $505.48  │  +$12.30  │   +2.49%   │  45.2M  │
│ AMD     │  $165.23  │   -$2.15  │   -1.28%   │  52.8M  │
│ TSLA    │  $207.83  │   +$5.67  │   +2.80%   │  120.5M │
└─────────┴───────────┴───────────┴────────────┴─────────┘

┌─────────────────────── CRYPTO ────────────────────────┐
│ Symbol  │  Price        │  Change   │  24h Volume     │
├─────────┼───────────────┼───────────┼─────────────────┤
│ BTC     │  $42,150.32   │  +3.25%   │  $28.5B         │
│ SOL     │  $98.45       │  +5.67%   │  $2.1B          │
│ HYPE    │  $12.34       │  -2.15%   │  $150M          │
│ ZEC     │  $35.67       │  +1.23%   │  $85M           │
└─────────┴───────────────┴───────────┴─────────────────┘
```

---

## 📁 Suggested Structure

```
multi-asset-price-watcher/
├── src/
│   ├── __init__.py
│   ├── api_clients.py      # API wrapper functions
│   ├── formatters.py        # Display formatting
│   └── main.py              # Main application
├── config/
│   ├── .env.template        # Template for API keys
│   └── assets.json          # List of assets to track
├── requirements.txt
└── README.md
```

---

## 🚀 Implementation Guide

### Step 1: Setup

**requirements.txt:**
```
requests>=2.31.0
python-dotenv>=1.0.0
yfinance>=0.2.0
tabulate>=0.9.0
```

**Install:**
```bash
pip install -r requirements.txt
```

### Step 2: API Clients

**src/api_clients.py:**
```python
import yfinance as yf
import requests
from typing import Dict, Optional

def fetch_stock_price(symbol: str) -> Optional[Dict]:
    """Fetch stock price using yfinance"""
    try:
        ticker = yf.Ticker(symbol)
        info = ticker.info

        return {
            'symbol': symbol,
            'price': info.get('currentPrice', info.get('regularMarketPrice')),
            'change': info.get('regularMarketChange'),
            'change_percent': info.get('regularMarketChangePercent'),
            'volume': info.get('volume'),
        }
    except Exception as e:
        print(f"Error fetching {symbol}: {e}")
        return None

def fetch_crypto_prices(symbols: list) -> Dict:
    """Fetch crypto prices from CoinGecko"""
    try:
        # Map symbols to CoinGecko IDs
        coin_map = {
            'BTC': 'bitcoin',
            'SOL': 'solana',
            'ZEC': 'zcash',
            'HYPE': 'hyperliquid',  # Verify actual ID
        }

        ids = ','.join([coin_map.get(s, s.lower()) for s in symbols])

        url = "https://api.coingecko.com/api/v3/simple/price"
        params = {
            'ids': ids,
            'vs_currencies': 'usd',
            'include_24hr_change': 'true',
            'include_24hr_vol': 'true'
        }

        response = requests.get(url, params=params)
        response.raise_for_status()
        return response.json()

    except Exception as e:
        print(f"Error fetching crypto prices: {e}")
        return {}
```

### Step 3: Formatting

**src/formatters.py:**
```python
from tabulate import tabulate
from datetime import datetime

def format_price(price: float) -> str:
    """Format price with appropriate decimal places"""
    if price >= 1000:
        return f"${price:,.2f}"
    elif price >= 1:
        return f"${price:.2f}"
    else:
        return f"${price:.4f}"

def format_change(change: float, change_percent: float) -> tuple:
    """Format price change and percentage"""
    sign = "+" if change >= 0 else ""
    change_str = f"{sign}${change:.2f}"
    percent_str = f"{sign}{change_percent:.2f}%"
    return change_str, percent_str

def display_stocks(stocks_data: list):
    """Display stock prices in a table"""
    if not stocks_data:
        print("No stock data available")
        return

    table_data = []
    for stock in stocks_data:
        if stock:
            change_str, percent_str = format_change(
                stock['change'], stock['change_percent']
            )
            table_data.append([
                stock['symbol'],
                format_price(stock['price']),
                change_str,
                percent_str,
                f"{stock['volume'] / 1_000_000:.1f}M"
            ])

    headers = ["Symbol", "Price", "Change", "Change %", "Volume"]
    print("\n" + "="*60)
    print("STOCKS")
    print("="*60)
    print(tabulate(table_data, headers=headers, tablefmt="grid"))

def display_crypto(crypto_data: dict):
    """Display crypto prices in a table"""
    if not crypto_data:
        print("No crypto data available")
        return

    # Implementation similar to display_stocks
    pass
```

### Step 4: Main Application

**src/main.py:**
```python
from datetime import datetime
from api_clients import fetch_stock_price, fetch_crypto_prices
from formatters import display_stocks, display_crypto

def main():
    """Main application loop"""

    # Configuration
    stock_symbols = ['NVDA', 'AMD', 'TSLA', 'GOOGL', 'MSFT']
    crypto_symbols = ['BTC', 'SOL', 'HYPE', 'ZEC']

    print("\n" + "="*60)
    print("Multi-Asset Price Watcher".center(60))
    print(f"Last Updated: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}".center(60))
    print("="*60)

    # Fetch stock data
    print("\nFetching stock prices...")
    stocks_data = [fetch_stock_price(symbol) for symbol in stock_symbols]

    # Fetch crypto data
    print("Fetching crypto prices...")
    crypto_data = fetch_crypto_prices(crypto_symbols)

    # Display results
    display_stocks(stocks_data)
    display_crypto(crypto_data)

if __name__ == "__main__":
    main()
```

---

## 🎯 Challenges & Extensions

### Challenge 1: Configuration File
Create `config/assets.json` to manage your watchlist:
```json
{
  "stocks": {
    "hpc_ai": ["NVDA", "AMD", "INTC"],
    "robotics": ["TSLA", "ISRG"],
    "mag7": ["AAPL", "MSFT", "GOOGL", "AMZN", "META", "NVDA", "TSLA"]
  },
  "crypto": ["BTC", "SOL", "HYPE", "ZEC"]
}
```

### Challenge 2: Auto-Refresh
Add a loop to refresh prices every N seconds:
```python
import time

while True:
    main()
    print("\nRefreshing in 60 seconds... (Ctrl+C to exit)")
    time.sleep(60)
```

### Challenge 3: Color Coding
Use `colorama` to color positive changes green and negative changes red:
```bash
pip install colorama
```

```python
from colorama import Fore, Style

def colorize_change(change: float, text: str) -> str:
    if change > 0:
        return f"{Fore.GREEN}{text}{Style.RESET_ALL}"
    elif change < 0:
        return f"{Fore.RED}{text}{Style.RESET_ALL}"
    return text
```

### Challenge 4: Alerts
Add price alert functionality:
```python
# Alert if NVDA > $500
if stock['symbol'] == 'NVDA' and stock['price'] > 500:
    print("🚨 ALERT: NVDA above $500!")
```

### Challenge 5: Save to CSV
Log prices to a CSV file for later analysis:
```python
import csv
from datetime import datetime

def log_price(symbol, price, change):
    with open('price_log.csv', 'a', newline='') as f:
        writer = csv.writer(f)
        writer.writerow([datetime.now(), symbol, price, change])
```

---

## ✅ Success Criteria

Your project is complete when:

- [ ] It fetches at least 5 stock prices
- [ ] It fetches at least 3 crypto prices
- [ ] Prices are displayed in a clean, readable format
- [ ] Errors are handled without crashing
- [ ] You can easily add/remove assets
- [ ] Code is organized into logical modules

---

## 🎓 What You're Learning

**Programming Concepts:**
- Working with multiple APIs
- Data formatting and presentation
- Error handling across multiple operations
- Code organization (modules, functions)
- Configuration management

**Market Knowledge:**
- Real-time vs. delayed data
- Price change calculations
- Volume metrics
- Different data sources for stocks vs. crypto

---

## 🆘 Troubleshooting

**"yfinance returns None or empty data"**
- Yahoo Finance can be flaky; add retry logic
- Try different symbols
- Check if market is open (stocks)

**"CoinGecko rate limit"**
- Free tier: ~10-50 calls/minute
- Add `time.sleep(1)` between calls
- Cache results

**"Prices look wrong"**
- Check if using correct currency (USD)
- Verify symbol mapping (especially for HYPE)
- Print raw API response to debug

---

## 📚 Next Steps

After completing this project:

1. **Add options data** (if comfortable with options)
2. **Create a web interface** using Flask or Streamlit
3. **Add technical indicators** (RSI, moving averages)
4. **Build notifications** (email, Discord, Telegram)
5. **Connect to databases** for historical tracking

---

**This project is your foundation for all market data work ahead. Take time to understand it deeply!**
