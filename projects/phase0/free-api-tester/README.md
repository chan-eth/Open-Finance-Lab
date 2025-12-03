# Free API Tester

Learn to make API calls and handle JSON responses by testing connections to free market data APIs.

---

## 🎯 Project Goals

- [ ] Install the `requests` library
- [ ] Make your first HTTP GET request
- [ ] Parse JSON responses
- [ ] Test multiple free APIs
- [ ] Handle errors gracefully
- [ ] Display results in a readable format

---

## 📚 APIs to Test

### 1. CoinGecko (No API Key Needed!)

**Easiest to start with - no registration required**

**Endpoint:** `https://api.coingecko.com/api/v3/simple/price`

**Example:**
```python
import requests

url = "https://api.coingecko.com/api/v3/simple/price"
params = {
    'ids': 'bitcoin,solana,zcash',
    'vs_currencies': 'usd'
}

response = requests.get(url, params=params)
data = response.json()
print(data)
```

### 2. CryptoCompare (Free Tier)

**Get API key:** https://min-api.cryptocompare.com/

**Example:**
```python
url = "https://min-api.cryptocompare.com/data/price"
params = {
    'fsym': 'BTC',
    'tsyms': 'USD'
}
# Add your API key in headers
```

### 3. Alpha Vantage (Stocks)

**Get free API key:** https://www.alphavantage.co/support/#api-key

**Example:**
```python
url = "https://www.alphavantage.co/query"
params = {
    'function': 'GLOBAL_QUOTE',
    'symbol': 'NVDA',
    'apikey': 'YOUR_KEY'
}
```

### 4. yfinance (Easiest for Stocks!)

**No API key needed - uses Yahoo Finance**

**Install:**
```bash
pip install yfinance
```

**Example:**
```python
import yfinance as yf

ticker = yf.Ticker("NVDA")
data = ticker.history(period="1d")
print(f"Latest price: ${data['Close'].iloc[-1]:.2f}")
```

---

## 🚀 Getting Started

### Step 1: Setup

```bash
# Install required package
pip install requests

# Optional: Install yfinance
pip install yfinance
```

### Step 2: Create Your Script

Create `api_tester.py`:

```python
import requests
import json

def test_coingecko():
    """Test CoinGecko API"""
    print("\n=== Testing CoinGecko ===")

    url = "https://api.coingecko.com/api/v3/simple/price"
    params = {
        'ids': 'bitcoin',
        'vs_currencies': 'usd'
    }

    try:
        response = requests.get(url, params=params)
        response.raise_for_status()  # Raise error for bad status
        data = response.json()

        btc_price = data['bitcoin']['usd']
        print(f"✓ Bitcoin: ${btc_price:,.2f}")

    except requests.exceptions.RequestException as e:
        print(f"✗ Error: {e}")

def test_yfinance():
    """Test yfinance"""
    print("\n=== Testing yfinance ===")

    try:
        import yfinance as yf
        ticker = yf.Ticker("NVDA")
        data = ticker.history(period="1d")

        if not data.empty:
            price = data['Close'].iloc[-1]
            print(f"✓ NVDA: ${price:.2f}")
        else:
            print("✗ No data returned")

    except Exception as e:
        print(f"✗ Error: {e}")

if __name__ == "__main__":
    print("Testing Free Market Data APIs...")
    test_coingecko()
    test_yfinance()
    print("\nAll tests complete!")
```

### Step 3: Run It

```bash
python api_tester.py
```

---

## 📝 Project Challenges

**Challenge 1: Basic API Test**
- Test at least 2 different APIs
- Print the results in a clean format
- Handle errors without crashing

**Challenge 2: Multi-Asset Dashboard**
- Fetch prices for 5+ assets (mix of stocks and crypto)
- Display in a table format
- Show timestamp of data

**Challenge 3: Save Results**
- Fetch data from multiple APIs
- Save results to a JSON file
- Load and display saved data

**Challenge 4: API Comparison**
- Fetch the same data (e.g., BTC price) from 2 different APIs
- Compare the results
- Calculate any price differences

---

## 💡 Code Templates

### Error Handling Template

```python
try:
    response = requests.get(url, params=params, timeout=10)
    response.raise_for_status()
    data = response.json()
    # Process data here

except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
except json.JSONDecodeError:
    print("Could not parse JSON response")
```

### Pretty Printing JSON

```python
import json

# Pretty print JSON
print(json.dumps(data, indent=2))
```

### Environment Variables (for API keys)

Create `.env` file:
```
ALPHA_VANTAGE_KEY=your_key_here
CRYPTOCOMPARE_KEY=your_key_here
```

Load in Python:
```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv('ALPHA_VANTAGE_KEY')
```

---

## ✅ Success Criteria

You've completed this project when you can:

- [ ] Successfully call at least 2 free APIs
- [ ] Parse JSON responses
- [ ] Display data in a readable format
- [ ] Handle common errors gracefully
- [ ] Understand what each part of the code does

---

## 🎓 What You're Learning

**Technical Skills:**
- HTTP requests with `requests` library
- JSON parsing
- Error handling
- Working with external libraries

**Market Data:**
- Different API providers
- Data formats and structures
- Rate limits and free tiers
- Real-time vs. delayed data

---

## 🆘 Common Issues

**"ModuleNotFoundError: No module named 'requests'"**
```bash
pip install requests
```

**"Connection Error"**
- Check your internet connection
- Try a different API
- Check if the API is down (visit their status page)

**"JSON Decode Error"**
- Print the raw response: `print(response.text)`
- Check if the API returned an error message
- Verify your parameters are correct

**Rate Limiting**
- Free APIs have limits (e.g., 5 calls/minute)
- Add delays between requests: `time.sleep(1)`
- Cache responses when possible

---

## 🚀 Going Further

Once you're comfortable:

1. **Create a price comparison tool** - Compare prices across APIs
2. **Build a crypto portfolio viewer** - Show your holdings' current value
3. **Add notifications** - Alert when a price hits a target
4. **Historical data** - Fetch and save historical price data
5. **Web dashboard** - Create a simple web page to display data

---

## 📚 API Documentation Links

- **CoinGecko:** https://www.coingecko.com/en/api/documentation
- **CryptoCompare:** https://min-api.cryptocompare.com/documentation
- **Alpha Vantage:** https://www.alphavantage.co/documentation/
- **yfinance:** https://pypi.org/project/yfinance/

---

**Remember:** Free APIs are your best friend as a beginner. Start here, learn the patterns, then expand to more sophisticated tools!
