# Hello Python CLI

Your first Python program! This project gets you comfortable with:
- Creating Python files
- Running scripts from the command line
- Basic input/output
- Variables and string formatting

---

## 🎯 Project Goals

- [ ] Create a Python script that runs from the terminal
- [ ] Accept user input
- [ ] Display formatted output
- [ ] Use variables and basic operations

---

## 📝 Requirements

**Level 1 (Basic):**
```python
# Create: hello.py
# Print a welcome message
# Ask for the user's name
# Greet them by name
```

**Expected output:**
```
Welcome to Open Finance Lab!
What's your name? John
Hello, John! Let's learn to code!
```

**Level 2 (Intermediate):**
Add:
- Ask for their favorite asset (stock, crypto, or option)
- Ask for a ticker symbol
- Display a personalized message

**Level 3 (Advanced):**
Add:
- Calculate something simple (e.g., "If you invested $1000, how many shares could you buy at $X per share?")
- Format numbers nicely

---

## 🚀 Getting Started

1. Create a new file called `hello.py`
2. Start with:
```python
# hello.py

print("Welcome to Open Finance Lab!")
```
3. Run it:
```bash
python hello.py
```
4. Expand from there!

---

## 💡 Hints

**Getting user input:**
```python
name = input("What's your name? ")
print(f"Hello, {name}!")
```

**Basic math:**
```python
price = 150.50
capital = 1000
shares = capital / price
print(f"You can buy {shares:.2f} shares")
```

---

## ✅ Success Criteria

You've completed this project when:
- Your script runs without errors
- It accepts input from the user
- It displays formatted output
- You understand what each line does

---

## 🎓 What You're Learning

- Python syntax basics
- Variables and data types
- String formatting (f-strings)
- User input with `input()`
- Print statements
- Running Python from command line

---

## 🆘 Getting Stuck?

**Error: "python: command not found"**
- Try `python3` instead
- Make sure Python is installed

**Syntax errors?**
- Check for missing quotes or parentheses
- Make sure indentation is correct

**Want to do more?**
- Add colors to your output (research `colorama` library)
- Create a menu with multiple options
- Save user preferences to a file

---

**Remember:** Every expert started with "Hello, World!" Take your time and enjoy the process!
