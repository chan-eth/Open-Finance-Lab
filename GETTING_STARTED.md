# Getting Started with Open Finance Lab

Welcome! This guide will help you begin your journey toward financial independence through coding and trading.

---

## 🎯 Who This Is For

- **Complete beginners** with no coding experience
- **Career changers** interested in fintech/quant trading
- **Self-learners** who prefer hands-on projects
- **AI-assisted learners** comfortable using AI coding tools
- **Anyone** wanting to understand markets systematically

---

## 🚀 Quick Start (5 minutes)

### 1. Check Prerequisites

You need:
- A computer (Mac, Windows, or Linux)
- Internet connection
- A GitHub account (free)
- Text editor or IDE (we'll set this up)

### 2. Clone This Repository

```bash
# If git is installed:
git clone https://github.com/your-username/Open-Finance-Lab.git
cd Open-Finance-Lab

# If git is not installed, download as ZIP from GitHub
```

### 3. Start with Phase 0

```bash
cd lessons/phase0
# Read the README.md
```

### 4. Set Up Your Development Log

```bash
cd log
# Open phase0-dev-log.md
# Start tracking your progress!
```

---

## 📚 Learning Path Overview

```
Phase 0 (2-4 weeks)
└─> Setup & Foundations
    └─> Python, Git, Terminal, APIs

Phase 1 (4-6 weeks)
└─> Beginner Fintech & Market Data
    └─> HTTP requests, JSON, Market basics

Phase 2 (6-10 weeks)
└─> Strategies & Backtesting
    └─> Indicators, Strategy design, Testing

Phase 3 (4-8 weeks)
└─> API Integration & Live Trading
    └─> Public API, Hyperliquid, Safety systems

Phase 4 (8-12 weeks)
└─> Advanced Architecture
    └─> Microservices, Databases, Dashboards

Phase 5 (Ongoing)
└─> Agentic Systems
    └─> Multi-agent, LLMs, Autonomy
```

**Total estimated time:** 6-12 months to reach Phase 5
**Realistic pace:** Take your time, build solid foundations

---

## 🛠 Initial Setup

### Step 1: Install Python

**Mac/Linux:**
```bash
# Check if Python is installed
python3 --version

# If not installed, use homebrew (Mac) or package manager (Linux)
brew install python3  # Mac
```

**Windows:**
- Download from [python.org](https://www.python.org/downloads/)
- Install, checking "Add Python to PATH"
- Verify: `python --version`

### Step 2: Choose a Code Editor

**Option 1: VS Code (Free, Popular)**
- Download: [code.visualstudio.com](https://code.visualstudio.com/)
- Install Python extension

**Option 2: Cursor (AI-powered, Great for beginners)**
- Download: [cursor.sh](https://cursor.sh/)
- Built-in AI assistance

**Option 3: PyCharm Community (Free, Full-featured)**
- Download: [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/)

### Step 3: Install Git

**Mac:**
```bash
brew install git
```

**Linux:**
```bash
sudo apt-get install git  # Ubuntu/Debian
```

**Windows:**
- Download from [git-scm.com](https://git-scm.com/)

### Step 4: Set Up API Keys

1. Copy the template:
```bash
cp config/api-keys.template.env config/.env
```

2. Sign up for free APIs:
   - [CoinGecko](https://www.coingecko.com/en/api) - No key needed for basic!
   - [Alpha Vantage](https://www.alphavantage.co/support/#api-key) - Free tier
   - [NewsAPI](https://newsapi.org/) - Free tier (optional)

3. Add your keys to `config/.env`

4. **NEVER commit .env to git** (already in .gitignore)

---

## 📖 How to Use This Repository

### Directory Structure

```
Open-Finance-Lab/
├── README.md              ← Overview & philosophy
├── GETTING_STARTED.md     ← You are here!
├── lessons/               ← Learning content by phase
│   ├── phase0/
│   ├── phase1/
│   └── ...
├── projects/              ← Hands-on projects
│   ├── phase0/
│   ├── phase1/
│   └── ...
├── notebooks/             ← Jupyter notebooks for analysis
├── config/                ← Configuration files
├── scripts/               ← Utility scripts
└── log/                   ← Your development journal
```

### Learning Flow

For each phase:

1. **Read** `lessons/phaseN/README.md`
2. **Build** projects in `projects/phaseN/`
3. **Track** progress in `log/phaseN-dev-log.md`
4. **Review** weekly using `log/weekly-reviews/`

---

## 🎯 Your First Week

### Day 1: Environment Setup
- [ ] Install Python
- [ ] Install code editor
- [ ] Install Git
- [ ] Clone this repository
- [ ] Run your first Python script

**Test it:**
```bash
python -c "print('Hello, Open Finance Lab!')"
```

### Day 2: Git Basics
- [ ] Configure git
- [ ] Create a new branch
- [ ] Make a commit
- [ ] Push to GitHub

**Commands to learn:**
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git status
git add .
git commit -m "message"
git push
```

### Day 3: Python Basics
- [ ] Variables and data types
- [ ] Print statements
- [ ] Basic operations
- [ ] Comments

**First script** (`test.py`):
```python
# My first Python script
name = "Finance Lab"
age = 0  # Just starting!

print(f"Welcome to {name}")
print(f"Age: {age} days")
```

### Day 4: First API Call
- [ ] Install requests library
- [ ] Make API call to CoinGecko
- [ ] Print Bitcoin price

**Script:**
```python
import requests

url = "https://api.coingecko.com/api/v3/simple/price"
params = {'ids': 'bitcoin', 'vs_currencies': 'usd'}

response = requests.get(url, params=params)
data = response.json()

print(f"Bitcoin price: ${data['bitcoin']['usd']:,.2f}")
```

### Day 5: Phase 0 Project
- [ ] Start `hello-python-cli` project
- [ ] Follow the project README
- [ ] Get it working!

### Day 6: API Testing
- [ ] Start `free-api-tester` project
- [ ] Test 2-3 different APIs
- [ ] Save results

### Day 7: Review & Plan
- [ ] Review week's progress
- [ ] Complete weekly review template
- [ ] Plan next week
- [ ] Celebrate progress! 🎉

---

## 💡 Learning Tips

### How to Use AI Assistants Effectively

**Good prompts:**
- "Explain what this code does line by line"
- "I'm getting this error: [paste error]. What does it mean?"
- "Show me how to [specific task] in Python"
- "What's wrong with this code? [paste code]"

**Less helpful prompts:**
- "Write me a trading bot" (too broad)
- "Fix this" (without context)
- "Make it better" (unclear goal)

### When to Ask AI vs. Google

**Ask AI when:**
- Explaining code concepts
- Debugging your specific code
- Suggesting approaches
- Code review and improvements

**Google when:**
- API documentation
- Official tutorials
- Community discussions
- Error messages (to see if others had it)

### How to Avoid Tutorial Hell

1. **Build, don't just watch**
   - Every concept = one project
   - Type the code yourself
   - Break things intentionally

2. **Focus on understanding**
   - Ask "why" not just "how"
   - Explain code in your own words
   - Teach concepts to yourself

3. **Embrace struggle**
   - Being stuck is learning
   - Errors are feedback
   - Each bug teaches

---

## 🚫 Common Beginner Mistakes

### 1. Jumping Ahead Too Fast
❌ "Phase 0 is boring, I'll skip to trading"
✅ Build foundations properly

### 2. Not Tracking Progress
❌ No logs, forget what you learned
✅ Update dev logs daily

### 3. Copy-Paste Without Understanding
❌ Code works but you don't know why
✅ Type code yourself, understand each line

### 4. Perfectionism
❌ "I need to master Phase 0 completely"
✅ Good enough, then iterate

### 5. Lone Wolf Syndrome
❌ Never ask for help
✅ Use AI, forums, communities

---

## 📊 How to Track Your Progress

### Daily (5 minutes)
- Update dev log with what you did
- Note challenges and solutions
- Plan tomorrow's focus

### Weekly (30 minutes)
- Complete weekly review
- Review code from the week
- Set next week's goals
- Celebrate wins!

### Monthly (1 hour)
- Review phase progress
- Update README with learnings
- Refactor old code
- Plan next month

---

## 🎯 Success Criteria

### Phase 0 Complete When:
- [ ] Can run Python scripts
- [ ] Made successful API call
- [ ] Committed code to GitHub
- [ ] Used AI assistant effectively
- [ ] Comfortable with terminal

### Phase 1 Complete When:
- [ ] Fetch stock and crypto prices
- [ ] Calculate PnL
- [ ] Save data to CSV
- [ ] Handle errors gracefully
- [ ] Understand market data structure

### Ready for Live Trading When:
- [ ] Completed Phases 0-2
- [ ] Backtested strategies
- [ ] Paper traded successfully
- [ ] Built safety systems
- [ ] Comfortable losing (paper) money
- [ ] Understand risk management

---

## 🆘 Getting Help

### When Stuck:

1. **Check the error message**
   - Read it carefully
   - Google the exact error
   - Ask AI to explain it

2. **Review the lesson**
   - Re-read the README
   - Check example code
   - Look at project structure

3. **Break the problem down**
   - What specifically isn't working?
   - What did you expect?
   - What actually happened?

4. **Ask for help**
   - Open a GitHub issue
   - Include error messages
   - Show what you tried
   - Paste relevant code

---

## 🎓 Recommended Resources

### Free Courses:
- **Python:** Codecademy, freeCodeCamp
- **Git:** GitHub Learning Lab
- **Markets:** Khan Academy (Finance)
- **Command Line:** Linux Journey

### Books (Optional):
- "Python Crash Course" - Eric Matthes
- "Automate the Boring Stuff" - Al Sweigart
- "Quantitative Trading" - Ernest Chan

### YouTube Channels:
- Corey Schafer (Python)
- Tech With Tim (Python projects)
- Part Time Larry (Algo trading)
- QuantPy (Backtesting)

---

## 🌟 Your Journey Starts Now

Remember:

✨ **Everyone starts as a beginner**
✨ **Progress compounds over time**
✨ **Small daily efforts > big occasional pushes**
✨ **It's okay to be confused**
✨ **Asking questions is strength, not weakness**
✨ **The best time to start was yesterday; second best is now**

---

## 📝 Next Steps

1. ✅ You've read this guide
2. ➡️ Go to `lessons/phase0/README.md`
3. ➡️ Start `projects/phase0/hello-python-cli/`
4. ➡️ Begin your dev log
5. ➡️ Make your first commit!

---

**Ready? Let's build toward financial independence, one line of code at a time.** 🚀

Got questions? Open an issue or check the lessons!

*Last updated: 2024*
