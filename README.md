# 🐍 Python Virtual Environment (venv) — Notes

> Understanding and using Python virtual environments to manage project dependencies cleanly and avoid conflicts.

---

## 📋 Table of Contents

- [What is venv?](#-what-is-venv)
- [Why use venv?](#-why-use-venv)
- [Complete Workflow](#-complete-workflow)
- [Day to Day Usage](#-day-to-day-usage)
- [Quick Reference](#-quick-reference)

---

## 🤔 What is venv?

**venv** (Virtual Environment) is an isolated Python environment for a specific project. Every project gets its own separate space for installing packages — completely independent from your system's global Python.

Think of it like this:

```
Your Kali Linux (Global Python)
│
├── Project A/
│   └── venv/          ← Project A's own isolated space
│       └── requests 2.0
│
└── Project B/
    └── venv/          ← Project B's own isolated space
        └── requests 3.0
```

The two projects don't interfere with each other at all.

---

## ❓ Why use venv?

Without venv, all packages install globally. This causes problems:

```
pip install requests==2.0   ✅ Project A works
pip install requests==3.0   ❌ Overwrites 2.0 — Project A breaks!
```

With venv, each project has its own packages — **no conflicts, ever.**

| Without venv | With venv |
|---|---|
| All packages go global | Packages stay inside the project |
| Version conflicts happen | No conflicts |
| Hard to share project | Easy to share via `requirements.txt` |
| Messes up system Python | System Python stays clean |

---

## 🔄 Complete Workflow

### Step 1 — Create the venv (only once per project)

```bash
python3 -m venv myenv
```

This creates a folder called `myenv` in your current directory:

```
myenv/
├── bin/          ← activate script lives here
├── lib/
└── include/
```

---

### Step 2 — Activate the venv

```bash
source myenv/bin/activate
```

**What is `source` doing?**
Inside `myenv/bin/` there is a script called `activate`. The `source` command runs that script, which tells the terminal to use this isolated Python environment instead of the global one.

**How to confirm it's activated:**

Your terminal prompt will change — `(myenv)` appears at the start:

```bash
# Before activation:
user@kali:~$

# After activation:
(myenv) user@kali:~$
```

As long as `(myenv)` is visible, you are inside the environment ✅

---

### Step 3 — Install tools/packages

Now anything you install stays only inside this venv — global Python is untouched:

```bash
pip install holehe
pip install sherlock-project
pip install requests
```

---

### Step 4 — Do your work

```bash
holehe target@email.com
sherlock username
python3 script.py
```

---

### Step 5 — Deactivate when done

```bash
deactivate
```

The `(myenv)` prefix disappears and your terminal returns to normal:

```bash
# After deactivation:
user@kali:~$
```

---

## 📅 Day to Day Usage

You only create the venv **once**. After that, just activate it whenever you want to work:

```bash
source myenv/bin/activate   # enter the environment
# ... do your work ...
deactivate                  # leave when done
```

---

## 📦 Sharing Your Project (requirements.txt)

If you want to share your project or set it up on another machine:

**Save all installed packages to a file:**
```bash
pip freeze > requirements.txt
```

**On the other machine, install everything from that file:**
```bash
pip install -r requirements.txt
```

---

## ⚡ Quick Reference

```bash
# Create venv
python3 -m venv myenv

# Activate (Kali/Linux/Mac)
source myenv/bin/activate

# Activate (Windows)
myenv\Scripts\activate

# Install a package (while inside venv)
pip install package-name

# See all installed packages
pip list

# Save packages to file
pip freeze > requirements.txt

# Install from requirements file
pip install -r requirements.txt

# Deactivate
deactivate
```

---

## 🔁 Full Flow at a Glance

```
python3 -m venv myenv          →  Create the isolated environment (once)
        ↓
source myenv/bin/activate      →  Enter the environment
        ↓
pip install holehe              →  Install tools inside the environment
        ↓
holehe target@email.com        →  Do your work
        ↓
deactivate                     →  Exit the environment
```

