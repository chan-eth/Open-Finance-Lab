# Portfolio Tracker

Build a CLI tool to track a mock portfolio across stocks and crypto, calculate current values, and compute PnL.

---

## 🎯 Project Goals

- [ ] Define a portfolio with multiple positions
- [ ] Fetch current prices for all holdings
- [ ] Calculate current portfolio value
- [ ] Calculate PnL (Profit and Loss) for each position
- [ ] Display portfolio summary with key metrics
- [ ] Save/load portfolio from file

---

## 🎨 Example Output

```
╔══════════════════════════════════════════════════════════╗
║              Portfolio Tracker v1.0                       ║
║              As of: 2024-01-15 10:30:45                  ║
╚══════════════════════════════════════════════════════════╝

Portfolio Summary:
├─ Total Value: $52,450.00
├─ Total Cost: $50,000.00
├─ Total PnL: +$2,450.00 (+4.90%)
└─ Number of Positions: 7

┌──────────────────────────────────────────────────────────┐
│ STOCKS                                                    │
├─────────┬─────────┬─────────┬───────────┬───────────────┤
│ Symbol  │ Shares  │ Avg Cost│ Cur Price │ PnL           │
├─────────┼─────────┼─────────┼───────────┼───────────────┤
│ NVDA    │  20     │ $450.00 │ $505.48   │ +$1,109.60    │
│         │         │         │           │ (+12.34%)     │
├─────────┼─────────┼─────────┼───────────┼───────────────┤
│ AMD     │  50     │ $150.00 │ $165.23   │ +$761.50      │
│         │         │         │           │ (+10.15%)     │
├─────────┼─────────┼─────────┼───────────┼───────────────┤
│ TSLA    │  10     │ $225.00 │ $207.83   │ -$171.70      │
│         │         │         │           │ (-7.63%)      │
└─────────┴─────────┴─────────┴───────────┴───────────────┘

┌──────────────────────────────────────────────────────────┐
│ CRYPTO                                                    │
├─────────┬─────────┬─────────┬───────────┬───────────────┤
│ Symbol  │ Amount  │ Avg Cost│ Cur Price │ PnL           │
├─────────┼─────────┼─────────┼───────────┼───────────────┤
│ BTC     │  0.5    │ $38,000 │ $42,150   │ +$2,075.00    │
│         │         │         │           │ (+10.92%)     │
├─────────┼─────────┼─────────┼───────────┼───────────────┤
│ SOL     │  100    │ $85.00  │ $98.45    │ +$1,345.00    │
│         │         │         │           │ (+15.82%)     │
└─────────┴─────────┴─────────┴───────────┴───────────────┘
```

---

## 📁 Suggested Structure

```
portfolio-tracker/
├── src/
│   ├── __init__.py
│   ├── portfolio.py         # Portfolio class
│   ├── position.py          # Position class
│   ├── price_fetcher.py     # Reuse from price-watcher
│   └── main.py              # Main application
├── data/
│   └── portfolio.json       # Portfolio holdings
├── requirements.txt
└── README.md
```

---

## 🚀 Implementation Guide

### Step 1: Data Model

**Portfolio Data Structure (portfolio.json):**
```json
{
  "portfolio_name": "My First Portfolio",
  "created_date": "2024-01-01",
  "positions": [
    {
      "symbol": "NVDA",
      "asset_type": "stock",
      "quantity": 20,
      "avg_cost": 450.00,
      "purchase_date": "2024-01-01"
    },
    {
      "symbol": "BTC",
      "asset_type": "crypto",
      "quantity": 0.5,
      "avg_cost": 38000.00,
      "purchase_date": "2024-01-05"
    }
  ]
}
```

### Step 2: Position Class

**src/position.py:**
```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class Position:
    """Represents a single position in the portfolio"""
    symbol: str
    asset_type: str  # 'stock' or 'crypto'
    quantity: float
    avg_cost: float
    purchase_date: str
    current_price: Optional[float] = None

    @property
    def cost_basis(self) -> float:
        """Total amount paid for this position"""
        return self.quantity * self.avg_cost

    @property
    def current_value(self) -> float:
        """Current market value of position"""
        if self.current_price is None:
            return 0
        return self.quantity * self.current_price

    @property
    def pnl_dollars(self) -> float:
        """Profit/loss in dollars"""
        return self.current_value - self.cost_basis

    @property
    def pnl_percent(self) -> float:
        """Profit/loss as percentage"""
        if self.cost_basis == 0:
            return 0
        return (self.pnl_dollars / self.cost_basis) * 100

    def update_price(self, price: float):
        """Update current market price"""
        self.current_price = price

    def __str__(self) -> str:
        return f"{self.symbol}: {self.quantity} @ ${self.avg_cost:.2f}"
```

### Step 3: Portfolio Class

**src/portfolio.py:**
```python
from typing import List
from position import Position
import json

class Portfolio:
    """Manages a collection of positions"""

    def __init__(self, name: str = "My Portfolio"):
        self.name = name
        self.positions: List[Position] = []

    def add_position(self, position: Position):
        """Add a position to the portfolio"""
        self.positions.append(position)

    def remove_position(self, symbol: str):
        """Remove a position by symbol"""
        self.positions = [p for p in self.positions if p.symbol != symbol]

    @property
    def total_value(self) -> float:
        """Total current value of all positions"""
        return sum(p.current_value for p in self.positions)

    @property
    def total_cost(self) -> float:
        """Total cost basis of all positions"""
        return sum(p.cost_basis for p in self.positions)

    @property
    def total_pnl_dollars(self) -> float:
        """Total PnL in dollars"""
        return self.total_value - self.total_cost

    @property
    def total_pnl_percent(self) -> float:
        """Total PnL as percentage"""
        if self.total_cost == 0:
            return 0
        return (self.total_pnl_dollars / self.total_cost) * 100

    def get_positions_by_type(self, asset_type: str) -> List[Position]:
        """Get all positions of a specific type"""
        return [p for p in self.positions if p.asset_type == asset_type]

    def save_to_file(self, filepath: str):
        """Save portfolio to JSON file"""
        data = {
            'portfolio_name': self.name,
            'positions': [
                {
                    'symbol': p.symbol,
                    'asset_type': p.asset_type,
                    'quantity': p.quantity,
                    'avg_cost': p.avg_cost,
                    'purchase_date': p.purchase_date
                }
                for p in self.positions
            ]
        }
        with open(filepath, 'w') as f:
            json.dump(data, f, indent=2)

    @classmethod
    def load_from_file(cls, filepath: str) -> 'Portfolio':
        """Load portfolio from JSON file"""
        with open(filepath, 'r') as f:
            data = json.load(f)

        portfolio = cls(data['portfolio_name'])
        for pos_data in data['positions']:
            position = Position(**pos_data)
            portfolio.add_position(position)

        return portfolio
```

### Step 4: Main Application

**src/main.py:**
```python
from portfolio import Portfolio
from price_fetcher import fetch_stock_price, fetch_crypto_prices
from datetime import datetime

def update_portfolio_prices(portfolio: Portfolio):
    """Fetch current prices and update all positions"""

    # Separate stocks and crypto
    stocks = portfolio.get_positions_by_type('stock')
    crypto = portfolio.get_positions_by_type('crypto')

    # Fetch stock prices
    for position in stocks:
        print(f"Fetching {position.symbol}...")
        price_data = fetch_stock_price(position.symbol)
        if price_data:
            position.update_price(price_data['price'])

    # Fetch crypto prices
    if crypto:
        crypto_symbols = [p.symbol for p in crypto]
        prices = fetch_crypto_prices(crypto_symbols)

        for position in crypto:
            # Map symbol to price from API response
            # (implementation depends on your API structure)
            pass

def display_portfolio(portfolio: Portfolio):
    """Display portfolio summary and positions"""

    print("\n" + "="*60)
    print(f"  {portfolio.name}")
    print(f"  As of: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print("="*60)

    print(f"\nPortfolio Summary:")
    print(f"  Total Value: ${portfolio.total_value:,.2f}")
    print(f"  Total Cost:  ${portfolio.total_cost:,.2f}")

    pnl_sign = "+" if portfolio.total_pnl_dollars >= 0 else ""
    print(f"  Total PnL:   {pnl_sign}${portfolio.total_pnl_dollars:,.2f}")
    print(f"               ({pnl_sign}{portfolio.total_pnl_percent:.2f}%)")

    # Display stocks
    stocks = portfolio.get_positions_by_type('stock')
    if stocks:
        print("\n" + "-"*60)
        print("STOCKS")
        print("-"*60)
        for pos in stocks:
            display_position(pos)

    # Display crypto
    crypto = portfolio.get_positions_by_type('crypto')
    if crypto:
        print("\n" + "-"*60)
        print("CRYPTO")
        print("-"*60)
        for pos in crypto:
            display_position(pos)

def display_position(position: Position):
    """Display a single position"""
    pnl_sign = "+" if position.pnl_dollars >= 0 else ""
    print(f"\n{position.symbol}")
    print(f"  Quantity:    {position.quantity}")
    print(f"  Avg Cost:    ${position.avg_cost:.2f}")
    print(f"  Current:     ${position.current_price:.2f}")
    print(f"  Value:       ${position.current_value:,.2f}")
    print(f"  PnL:         {pnl_sign}${position.pnl_dollars:,.2f} ({pnl_sign}{position.pnl_percent:.2f}%)")

def main():
    # Load or create portfolio
    try:
        portfolio = Portfolio.load_from_file('data/portfolio.json')
    except FileNotFoundError:
        print("Creating new portfolio...")
        portfolio = Portfolio("My First Portfolio")
        # Add some example positions
        # (In real use, you'd add these via CLI or UI)

    # Update prices
    print("Fetching current prices...")
    update_portfolio_prices(portfolio)

    # Display results
    display_portfolio(portfolio)

    # Save updated portfolio
    portfolio.save_to_file('data/portfolio.json')

if __name__ == "__main__":
    main()
```

---

## 🎯 Challenges & Extensions

### Challenge 1: Add Position
Create a function to add new positions via CLI:
```python
def add_position_cli():
    symbol = input("Symbol: ")
    asset_type = input("Type (stock/crypto): ")
    quantity = float(input("Quantity: "))
    avg_cost = float(input("Average cost: "))
    # Add to portfolio
```

### Challenge 2: Performance Chart
Use matplotlib to visualize portfolio performance:
```python
import matplotlib.pyplot as plt

def plot_portfolio_allocation(portfolio):
    # Pie chart of positions by value
    pass
```

### Challenge 3: Historical Tracking
Save portfolio snapshots daily to track performance over time:
```python
{
  "date": "2024-01-15",
  "total_value": 52450.00,
  "total_pnl": 2450.00
}
```

### Challenge 4: Asset Allocation
Show breakdown by asset type, sector, or risk level:
```
Asset Allocation:
├─ Stocks: 60% ($31,000)
└─ Crypto: 40% ($21,450)

Sector Allocation (Stocks):
├─ HPC/AI: 70%
└─ Robotics: 30%
```

### Challenge 5: Rebalancing Suggestions
Calculate how to rebalance to target allocations:
```python
def suggest_rebalancing(portfolio, target_allocations):
    # Compare current vs. target
    # Suggest trades to rebalance
    pass
```

---

## ✅ Success Criteria

- [ ] Can load portfolio from file
- [ ] Fetches current prices for all positions
- [ ] Calculates PnL correctly for each position
- [ ] Displays clear portfolio summary
- [ ] Saves portfolio data
- [ ] Handles both stocks and crypto
- [ ] Code is well-organized and commented

---

## 🎓 What You're Learning

- Object-oriented programming (classes)
- Data modeling and persistence (JSON)
- Financial calculations (PnL, returns)
- Working with mixed asset types
- Code organization patterns
- Real-world application structure

---

## 🆘 Troubleshooting

**"PnL calculations look wrong"**
- Double-check: PnL = (Current Price - Avg Cost) × Quantity
- Verify current prices are fetching correctly
- Check for currency mismatches

**"Can't load portfolio file"**
- Create data/ directory first
- Check JSON formatting
- Provide better error messages

**"Prices not updating"**
- Print raw API responses to debug
- Check for API rate limits
- Add retry logic for failed fetches

---

## 📚 Next Steps

- Add dividend/interest tracking
- Support for multiple portfolios
- Tax lot tracking (FIFO, LIFO)
- Options positions (more complex P&L)
- Integration with brokerage APIs for live data
- Web dashboard with historical charts

---

**This project teaches you the fundamentals of portfolio management - skills you'll use throughout your trading journey!**
