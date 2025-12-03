# Open Finance Lab 🧪📈

_A public, beginner‑to‑advanced journey toward financial independence by building fintech tools and autonomous trading systems across **stocks, options, and crypto** — all guided by AI coding assistants and free APIs._

---

## 🚀 What This Repo Is

This repository tracks my end‑to‑end learning journey:

- Starting from **zero coding experience**
- Learning core **Python + fintech + trading concepts**
- Building an evolving stack of **tools, bots, and analytics**
- All the way to **autonomous, agentic trading systems** for both traditional markets and crypto

**Trading Venues:**

- **Public Brokerage API** – stocks & options (HPC/AI, robotics, Mag7)
- **Hyperliquid** – crypto (HYPE, SOL, BTC, ZEC) + Mag7 trading

**Focus Areas:**

- **Stocks:** HPC/AI and robotics sectors (NVDA, AMD, TSLA, etc.)
- **Options:** Strategies on high-conviction tech names
- **Crypto:** HYPE, SOL, BTC, ZEC (on Hyperliquid)
- **Mag7:** Trading the "Magnificent 7" tech giants across both platforms

**Core Philosophy:**

- **Low barrier to entry** – Use free APIs wherever possible
- **Learn by building** – Every concept paired with a real project
- **AI-first workflow** – AI assistants as coding teammates
- **Public accountability** – All progress shared openly

Everything here is built in public so anyone can follow along and see that **you don't need to be an expert to start** your journey toward financial independence.

> ⚠️ **Disclaimer:**
> Nothing in this repo is financial advice. All code and ideas are for educational purposes only. Use at your own risk and preferably on paper/demo accounts first.

---

## 🧠 Learning Philosophy

1. **Build to learn** – Every concept is paired with a project.
2. **AI‑first workflow** – Use AI coding tools as teammates, not crutches.
3. **Repetition & iteration** – Early projects will be refactored as I learn more.
4. **Public accountability** – I'll record and share my progress regularly.
5. **Real markets, realistic constraints** – Focus on free/low-cost APIs and assets I'm bullish on.
6. **Financial independence mindset** – Learn skills that compound over time.

---

## 🛠 AI Coding Assistants

Throughout this repo I'll actively use:

- **Claude Code**
- **Cursor** (AI pair programming editor)
- **OpenAI Codex–style tooling / ChatGPT**
- **Google Gemini**
- (And any other AI assistant that helps)

In each lesson/project I'll note:

- What I wrote myself
- What AI generated
- Prompts or strategies that worked well

---

## 🎯 Endgame: Multi-Platform Autonomous Trading Systems

The long‑term objective:

> **Build modular, autonomous, agentic trading systems across both traditional markets and crypto**
> that trade stocks, options, and crypto using:
> - Shared utilities and tools from earlier lessons
> - Strategy modules (trend, mean reversion, options spreads, funding arbitrage, etc.)
> - **Locally hosted APIs** (e.g., local LLM / decision server, feature generators)
> - **Server‑based APIs** (e.g., market data, execution gateways, dashboards)

**Target Platforms:**

- **Public Brokerage** – for HPC/AI stocks, robotics stocks, and options strategies
- **Hyperliquid** – for crypto perpetuals and Mag7 exposure

High‑level components we'll eventually build:

- 🧩 **Data Layer** – market data fetchers (free APIs), OHLCV store, factor builders
- 🧠 **Signal Engine** – strategies & ML/LLM‑assisted decision logic
- 🎯 **Execution Engine** – order routing to Public/Hyperliquid, slippage controls
- 🛡 **Risk & Limits** – per‑asset caps, daily loss limits, circuit breakers
- 📊 **Monitoring & Dashboard** – PnL, exposure, health across all venues
- 🤖 **Agentic Loop** – system that observes, decides, executes, and reviews

---

## 🆓 Free API Resources

To keep this accessible, we'll leverage free APIs wherever possible:

**Market Data (Stocks/Options):**
- **Alpha Vantage** – free tier for stocks, crypto, forex
- **Polygon.io** – free tier for stocks & options data
- **Yahoo Finance (unofficial)** – via `yfinance` Python library
- **EODHD** – free tier for historical data
- **Tradier Developer** – free delayed market data

**Crypto Data:**
- **CoinGecko** – free API for crypto prices & market data
- **CryptoCompare** – free tier for OHLCV and real-time data
- **Hyperliquid Public APIs** – native market data (free)

**Economic Data:**
- **FRED (Federal Reserve Economic Data)** – completely free
- **World Bank API** – free economic indicators

**News & Sentiment:**
- **NewsAPI** – free tier for headlines
- **Reddit API** – free access to r/wallstreetbets, r/stocks, etc.

**Execution:**
- **Public Brokerage API** – commission-free trading
- **Hyperliquid** – low fees, no API costs

---

## 📚 Learning Roadmap

This repo is organized into **phased tracks**. Each phase has:

- Lessons (`/lessons`)
- Projects (`/projects`)
- Reflections & recordings (`/log`)

### Phase 0 – Setup & Foundations

**Goal:** Go from "I've never coded" to "I can run simple Python scripts and use an API."

**Topics:**

- Installing Python and a dev environment (Cursor, VS Code, etc.)
- Git + GitHub basics (cloning, committing, pushing)
- Command line basics
- How to effectively prompt AI coding tools

**Planned Projects:**

- `projects/phase0/hello-python-cli/` – simple CLI script
- `projects/phase0/free-api-tester/` – test connections to free market data APIs
- `log/phase0-dev-log.md` – daily/weekly progress log
- First recorded video: walking through repo and goals

---

### Phase 1 – Beginner Fintech & Market Data

**Goal:** Get comfortable with Python, APIs, and basic market concepts using real assets.

**Topics:**

- Python basics (variables, loops, functions, modules)
- Working with JSON, HTTP requests, environment variables
- Simple price data fetching for stocks and crypto
- Basic trading vocabulary (candles, OHLCV, PnL, orders, options Greeks)

**Example Projects:**

- `projects/phase1/multi-asset-price-watcher/`
  - CLI tool to fetch and print latest prices for:
    - Stocks (NVDA, AMD, TSLA, etc.)
    - Crypto (HYPE, SOL, BTC, ZEC)
    - Options chains for select tickers
- `projects/phase1/portfolio-tracker/`
  - Track a mock portfolio across stocks + crypto
  - Calculate current value and simple PnL
- `projects/phase1/ohlcv-downloader/`
  - Save historical candles for stocks & crypto to CSV using free APIs

**AI Use:**
Heavy prompting for boilerplate, but I'll focus on understanding:

- What each line of code does
- How to read error messages
- How to modify AI‑generated code

---

### Phase 2 – Intermediate: Strategies & Backtesting

**Goal:** Turn raw data into **strategies** and test ideas on past data.

**Topics:**

- Time series basics (returns, moving averages, volatility)
- Stock strategies: moving average crossover, momentum, sector rotation
- Options strategies: covered calls, cash-secured puts, spreads
- Crypto strategies: funding arbitrage, trend following
- Backtesting basics (entry/exit rules, fees, slippage)
- Intro to risk management: position sizing, stop losses

**Example Projects:**

- `projects/phase2/strategy-lab/`
  - Notebooks to prototype indicators & strategies by asset class
- `projects/phase2/backtester-v1/`
  - Simple event‑based backtester supporting:
    - Stock strategies (long/short)
    - Options strategies (basic P&L modeling)
    - Crypto strategies (perpetuals/spot)
    - Per‑asset performance metrics
- `projects/phase2/paper-trader/`
  - Simulated trading using live prices but no real orders
  - Support for both Public and Hyperliquid paper accounts

**AI Use:**
Use AI to:

- Explain math/finance concepts in plain language
- Suggest strategy ideas based on market regimes
- Improve code readability and performance

---

### Phase 3 – API Integration & Live Trading (Controlled)

**Goal:** Connect to **Public Brokerage** and **Hyperliquid**, place small test orders, and structure bots as real systems.

**Topics:**

- Public Brokerage API (auth, account data, order placement)
- Hyperliquid APIs (REST/WebSocket, auth, rate limits)
- Reading positions, balances, open orders across platforms
- Building unified order execution wrappers
- Config files, secrets management, basic security hygiene

**Example Projects:**

- `projects/phase3/public-api-wrapper/`
  - Reusable Python client for Public Brokerage:
    - Getting account info & positions
    - Fetching stock/options quotes
    - Placing/cancelling orders
- `projects/phase3/hyperliquid-api-wrapper/`
  - Reusable Python client for Hyperliquid:
    - Getting markets & prices
    - Checking balances
    - Placing/cancelling perpetual orders
- `projects/phase3/unified-execution-layer/`
  - Abstraction layer that routes orders to correct platform
- `projects/phase3/sandbox-bots/`
  - **Single‑strategy** live bots for testing:
    - Stock bot (e.g., NVDA momentum)
    - Options bot (e.g., TSLA weekly puts)
    - Crypto bot (e.g., BTC trend following)
  - Only runs with small or paper size
  - Includes logging & simple risk checks

**AI Use:**
Have AI help:

- Review API usage for common mistakes
- Generate tests for crucial functions
- Help design a safe "kill switch" or panic behavior

---

### Phase 4 – Advanced: Locally Hosted & Server‑Based APIs

**Goal:** Upgrade to a **modular, distributed system** with local + server APIs.

**Topics:**

- Building a **local API service** (e.g., FastAPI/Flask) for:
  - Feature generation (indicators, signals)
  - Local decision engines (could later use local LLMs)
- Deploying **server‑based APIs** for:
  - Data collection and aggregation
  - Dashboards and monitoring (web UI)
- Message queues / task scheduling basics
- State & persistence (DB or lightweight storage)
- Multi-venue aggregation

**Example Projects:**

- `projects/phase4/local-feature-service/`
  - Locally hosted API to:
    - Receive raw price data (stocks, options, crypto)
    - Return computed indicators / signals
    - Support custom strategy logic
- `projects/phase4/unified-execution-service/`
  - Server‑hosted API that:
    - Accepts high‑level "trade intents"
    - Routes to Public or Hyperliquid
    - Logs all actions centrally
- `projects/phase4/monitoring-dashboard/`
  - Simple web UI to see:
    - Positions across all platforms
    - PnL by asset class
    - Recent trades
    - Risk warnings and limits

**AI Use:**
Use AI to:

- Sketch microservice diagrams
- Draft API contracts and OpenAPI specs
- Suggest refactoring from monolith → services

---

### Phase 5 – Agentic Trading System

**Goal:** Assemble everything into **agentic systems** that can:

- Observe markets across stocks, options, and crypto
- Generate hypotheses & strategies
- Execute trades on appropriate platforms
- Learn from results (at least via rules/heuristics at first)

**Core Modules:**

- `agents/market-watcher/` – monitors Public + Hyperliquid streams
- `agents/signal-agent/` – calls local/remote APIs for signals
- `agents/risk-agent/` – approves or vetoes trade ideas
- `agents/execution-agent/` – sends orders via unified execution service
- `agents/review-agent/` – analyzes performance and suggests changes

**Specialization by Asset Class:**

- **HPC/AI Stocks** – momentum, earnings plays, sector rotation
- **Robotics Stocks** – thematic baskets, trend following
- **Options** – volatility strategies, spreads, earnings plays
- **Crypto (HYPE, SOL, BTC, ZEC)** – funding arb, perp strategies
- **Mag7** – cross-platform opportunities (stocks on Public, perps on Hyperliquid)

**AI Use:**
Heavy use of AI to:

- Act as a "research assistant" generating strategy tweaks
- Write and refactor agent code
- Analyze logs and performance patterns
- Suggest optimizations based on market conditions

---

## 📁 Suggested Repo Structure

This is the **target** structure; early on, not everything will exist yet.

```text
.
├── README.md
├── lessons/
│   ├── phase0/
│   ├── phase1/
│   ├── phase2/
│   ├── phase3/
│   ├── phase4/
│   └── phase5/
├── projects/
│   ├── phase0/
│   ├── phase1/
│   ├── phase2/
│   ├── phase3/
│   ├── phase4/
│   └── phase5/
├── agents/
│   ├── market-watcher/
│   ├── signal-agent/
│   ├── risk-agent/
│   ├── execution-agent/
│   └── review-agent/
├── notebooks/
│   ├── stocks/
│   ├── options/
│   └── crypto/
├── config/
│   ├── api-keys.template.env
│   ├── strategies/
│   └── risk-limits/
├── scripts/
│   ├── setup/
│   └── utilities/
└── log/
    ├── phase0-dev-log.md
    ├── phase1-dev-log.md
    └── weekly-reviews/
```

---

## 🌟 Why This Approach Works

**For Financial Independence:**
- Build real skills that compound over time
- Learn to use professional-grade tools (APIs, cloud services)
- Develop systematic thinking about markets and risk
- Create reusable systems that can scale

**For Learning:**
- Start with free tools (no financial barrier)
- AI assistants accelerate the learning curve
- Public accountability keeps you motivated
- Real market data makes it immediately practical

**For Career Growth:**
- Skills transfer to fintech, quant finance, or tech roles
- Portfolio of real projects to show employers
- Deep understanding of modern development practices
- Experience with AI-assisted development workflows

---

## 🤝 Contributing & Community

This is primarily a personal learning journey, but:

- **Questions?** Open an issue
- **Found a bug?** Submit a PR
- **Want to follow along?** Star/watch the repo
- **Building something similar?** Fork it and share your progress!

---

## 📜 License

MIT License – feel free to use this code for your own learning.

---

## 🚦 Getting Started

1. **Clone this repo**
   ```bash
   git clone https://github.com/your-username/Open-Finance-Lab.git
   cd Open-Finance-Lab
   ```

2. **Check out the first lesson**
   ```bash
   cd lessons/phase0/
   ```

3. **Follow along** with `log/phase0-dev-log.md`

4. **Set up your free API keys** (we'll cover this in Phase 0)

5. **Start building!**

---

**Let's build toward financial independence, one commit at a time. 🚀**
