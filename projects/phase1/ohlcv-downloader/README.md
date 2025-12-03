# OHLCV Downloader

Download and save historical candlestick data (Open, High, Low, Close, Volume) for stocks and crypto to CSV files for later analysis.

---

## 🎯 Project Goals

- [ ] Download historical OHLCV data for stocks
- [ ] Download historical OHLCV data for crypto
- [ ] Support multiple timeframes (1d, 1h, 5m, etc.)
- [ ] Save data to CSV files
- [ ] Handle date ranges
- [ ] Resume interrupted downloads

---

## 📊 OHLCV Data Explained

**OHLCV** (sometimes called "candles") represents price action over a time period:

- **O**pen: First price in the period
- **H**igh: Highest price reached
- **L**ow: Lowest price reached
- **C**lose: Last price in the period
- **V**olume: Number of shares/coins traded

Example:
```
Date        Open     High     Low      Close    Volume
2024-01-15  505.00   512.50   502.30   510.20   45,200,000
```

---

## 📁 Suggested Structure

```
ohlcv-downloader/
├── src/
│   ├── __init__.py
│   ├── downloaders/
│   │   ├── stock_downloader.py
│   │   └── crypto_downloader.py
│   ├── utils.py
│   └── main.py
├── data/
│   ├── stocks/
│   │   ├── NVDA_1d.csv
│   │   └── AMD_1h.csv
│   └── crypto/
│       ├── BTC_1d.csv
│       └── SOL_1h.csv
├── config/
│   └── download_config.json
├── requirements.txt
└── README.md
```

---

## 🚀 Implementation Guide

### Step 1: Setup

**requirements.txt:**
```
yfinance>=0.2.0
pandas>=2.0.0
requests>=2.31.0
python-dotenv>=1.0.0
```

### Step 2: Stock Downloader

**src/downloaders/stock_downloader.py:**
```python
import yfinance as yf
import pandas as pd
from pathlib import Path
from datetime import datetime, timedelta

def download_stock_data(
    symbol: str,
    interval: str = '1d',
    period: str = None,
    start_date: str = None,
    end_date: str = None,
    save_dir: str = 'data/stocks'
) -> pd.DataFrame:
    """
    Download stock OHLCV data

    Args:
        symbol: Stock ticker (e.g., 'NVDA')
        interval: Data interval (1m, 5m, 15m, 1h, 1d, 1wk, 1mo)
        period: Period to download (1d, 5d, 1mo, 3mo, 6mo, 1y, 2y, 5y, max)
        start_date: Start date (YYYY-MM-DD)
        end_date: End date (YYYY-MM-DD)
        save_dir: Directory to save CSV

    Returns:
        DataFrame with OHLCV data
    """

    print(f"Downloading {symbol} data ({interval})...")

    try:
        ticker = yf.Ticker(symbol)

        # Download data
        if start_date and end_date:
            df = ticker.history(interval=interval, start=start_date, end=end_date)
        elif period:
            df = ticker.history(interval=interval, period=period)
        else:
            # Default to 1 year
            df = ticker.history(interval=interval, period='1y')

        if df.empty:
            print(f"  ⚠ No data returned for {symbol}")
            return None

        # Clean up DataFrame
        df = df.reset_index()
        df.columns = [col.lower() for col in df.columns]

        # Remove timezone info if present
        if 'date' in df.columns:
            df['date'] = pd.to_datetime(df['date']).dt.tz_localize(None)
        elif 'datetime' in df.columns:
            df['date'] = pd.to_datetime(df['datetime']).dt.tz_localize(None)
            df = df.drop('datetime', axis=1)

        # Save to CSV
        Path(save_dir).mkdir(parents=True, exist_ok=True)
        filename = f"{symbol}_{interval}.csv"
        filepath = Path(save_dir) / filename
        df.to_csv(filepath, index=False)

        print(f"  ✓ Saved {len(df)} candles to {filepath}")
        return df

    except Exception as e:
        print(f"  ✗ Error downloading {symbol}: {e}")
        return None

def download_multiple_stocks(
    symbols: list,
    interval: str = '1d',
    period: str = '1y'
):
    """Download data for multiple stocks"""

    print(f"\nDownloading {len(symbols)} stocks...")
    print(f"Interval: {interval}, Period: {period}\n")

    results = {}
    for symbol in symbols:
        df = download_stock_data(symbol, interval=interval, period=period)
        results[symbol] = df

    successful = sum(1 for df in results.values() if df is not None)
    print(f"\n✓ Downloaded {successful}/{len(symbols)} stocks successfully")

    return results
```

### Step 3: Crypto Downloader

**src/downloaders/crypto_downloader.py:**
```python
import requests
import pandas as pd
from pathlib import Path
from datetime import datetime
import time

def download_crypto_data(
    symbol: str,
    vs_currency: str = 'usd',
    days: int = 365,
    save_dir: str = 'data/crypto'
) -> pd.DataFrame:
    """
    Download crypto OHLCV data from CoinGecko

    Args:
        symbol: Crypto symbol (e.g., 'bitcoin', 'solana')
        vs_currency: Currency to price in (usd, eur, etc.)
        days: Number of days of history (1-365)
        save_dir: Directory to save CSV
    """

    print(f"Downloading {symbol} data...")

    try:
        url = f"https://api.coingecko.com/api/v3/coins/{symbol}/ohlc"
        params = {
            'vs_currency': vs_currency,
            'days': days
        }

        response = requests.get(url, params=params)
        response.raise_for_status()
        data = response.json()

        if not data:
            print(f"  ⚠ No data returned for {symbol}")
            return None

        # Convert to DataFrame
        df = pd.DataFrame(data, columns=['timestamp', 'open', 'high', 'low', 'close'])
        df['date'] = pd.to_datetime(df['timestamp'], unit='ms')
        df = df.drop('timestamp', axis=1)
        df = df[['date', 'open', 'high', 'low', 'close']]

        # Save to CSV
        Path(save_dir).mkdir(parents=True, exist_ok=True)
        filename = f"{symbol}_1d.csv"
        filepath = Path(save_dir) / filename
        df.to_csv(filepath, index=False)

        print(f"  ✓ Saved {len(df)} candles to {filepath}")
        return df

    except Exception as e:
        print(f"  ✗ Error downloading {symbol}: {e}")
        return None

def download_multiple_crypto(
    symbols: list,
    days: int = 365
):
    """Download data for multiple cryptocurrencies"""

    # Map common symbols to CoinGecko IDs
    symbol_map = {
        'BTC': 'bitcoin',
        'SOL': 'solana',
        'ZEC': 'zcash',
        'HYPE': 'hyperliquid',  # Verify this ID
        'ETH': 'ethereum'
    }

    print(f"\nDownloading {len(symbols)} cryptocurrencies...")
    print(f"Days: {days}\n")

    results = {}
    for symbol in symbols:
        coin_id = symbol_map.get(symbol.upper(), symbol.lower())
        df = download_crypto_data(coin_id, days=days)
        results[symbol] = df

        # Rate limiting - CoinGecko free tier
        time.sleep(1.5)

    successful = sum(1 for df in results.values() if df is not None)
    print(f"\n✓ Downloaded {successful}/{len(symbols)} cryptocurrencies successfully")

    return results
```

### Step 4: Main Application

**src/main.py:**
```python
import argparse
from downloaders.stock_downloader import download_multiple_stocks
from downloaders.crypto_downloader import download_multiple_crypto

def main():
    parser = argparse.ArgumentParser(description='Download OHLCV data')
    parser.add_argument('--type', choices=['stocks', 'crypto', 'all'],
                       default='all', help='Asset type to download')
    parser.add_argument('--interval', default='1d',
                       help='Data interval for stocks (1d, 1h, etc.)')
    parser.add_argument('--period', default='1y',
                       help='Period for stocks (1y, 2y, max, etc.)')
    parser.add_argument('--days', type=int, default=365,
                       help='Days of crypto data to download')

    args = parser.parse_args()

    # Define assets to download
    stock_symbols = ['NVDA', 'AMD', 'TSLA', 'GOOGL', 'MSFT', 'AAPL']
    crypto_symbols = ['BTC', 'SOL', 'ZEC', 'HYPE']

    if args.type in ['stocks', 'all']:
        download_multiple_stocks(
            stock_symbols,
            interval=args.interval,
            period=args.period
        )

    if args.type in ['crypto', 'all']:
        download_multiple_crypto(
            crypto_symbols,
            days=args.days
        )

if __name__ == "__main__":
    main()
```

---

## 🎯 Usage Examples

### Basic Usage

```bash
# Download all assets (stocks + crypto)
python src/main.py

# Download only stocks
python src/main.py --type stocks

# Download only crypto
python src/main.py --type crypto

# Download 2 years of daily stock data
python src/main.py --type stocks --period 2y

# Download hourly stock data for 1 month
python src/main.py --type stocks --interval 1h --period 1mo

# Download 90 days of crypto data
python src/main.py --type crypto --days 90
```

### Loading Downloaded Data

```python
import pandas as pd

# Load stock data
nvda_data = pd.read_csv('data/stocks/NVDA_1d.csv', parse_dates=['date'])
print(nvda_data.head())

# Basic analysis
print(f"Date range: {nvda_data['date'].min()} to {nvda_data['date'].max()}")
print(f"Rows: {len(nvda_data)}")
print(f"Avg close: ${nvda_data['close'].mean():.2f}")
```

---

## 🎯 Challenges & Extensions

### Challenge 1: Update Existing Data
Check if CSV exists and only download new candles:
```python
def update_data(symbol, filepath):
    if filepath.exists():
        existing = pd.read_csv(filepath)
        last_date = existing['date'].max()
        # Download only from last_date to now
    else:
        # Download all data
```

### Challenge 2: Multiple Timeframes
Download the same assets in multiple timeframes:
```bash
python src/main.py --intervals 1d,1h,15m
```

### Challenge 3: Data Quality Checks
Add validation for downloaded data:
```python
def validate_data(df):
    # Check for missing dates
    # Check for price anomalies (gaps, spikes)
    # Check for negative volumes
    # Check for OHLC relationship (Low <= Open/Close <= High)
```

### Challenge 4: Progress Bar
Show download progress:
```bash
pip install tqdm
```
```python
from tqdm import tqdm
for symbol in tqdm(symbols):
    download_stock_data(symbol)
```

### Challenge 5: Database Storage
Instead of CSV, save to SQLite:
```python
import sqlite3
df.to_sql('ohlcv_data', conn, if_exists='append')
```

---

## ✅ Success Criteria

- [ ] Downloads stock data successfully
- [ ] Downloads crypto data successfully
- [ ] Saves to organized CSV files
- [ ] Handles errors gracefully
- [ ] Supports different timeframes
- [ ] Can load and verify downloaded data

---

## 🎓 What You're Learning

**Technical:**
- Working with time series data
- File I/O and directory management
- Command-line arguments (argparse)
- Data cleaning and formatting
- Error handling and retry logic

**Market Data:**
- OHLCV candle structure
- Different data intervals
- Data sources and APIs
- Data quality issues
- Historical vs. real-time data

---

## 📊 Data Intervals Explained

**Stock Market (via yfinance):**
- `1m` - 1 minute (7 days max)
- `5m` - 5 minutes (60 days max)
- `15m` - 15 minutes (60 days max)
- `1h` - 1 hour
- `1d` - Daily
- `1wk` - Weekly
- `1mo` - Monthly

**Crypto (CoinGecko free tier):**
- Daily only for historical data
- Limited to 365 days on free tier
- For intraday, need different API (e.g., Binance)

---

## 🆘 Troubleshooting

**"No data returned"**
- Check symbol is correct
- Verify market hours (for stocks)
- Check API rate limits
- Try different period/interval

**"Too many requests"**
- Add delays between API calls (`time.sleep(1)`)
- Respect rate limits
- Consider caching

**"Missing candles"**
- Markets closed on weekends/holidays
- Low volume may result in missing data
- Check exchange hours

**"File permissions error"**
- Make sure data directories exist
- Check write permissions

---

## 📚 Next Steps

- Build a data update script (run daily)
- Create a data explorer/visualizer
- Implement data quality checks
- Add more data sources
- Build a time series database
- Create backtest using this data

---

**This project gives you the raw material for all future backtesting and analysis. Good historical data is foundational to quant trading!**
