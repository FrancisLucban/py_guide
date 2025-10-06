# 🐍 Automation & Scripting with Python

## 📘 Overview

- **Automation** - letting a computer handle repetitive tasks for you.
- **Scripting** - writing short programs that automate simple processes (e.g., renaming files, scraping data, sending emails).

## 🧠 Core Concepts

### 1. Scripting Basics

Before diving into automation, understand:

- **File handling**: `open()`, reading/writing files.
- **OS operations**: using `os`, `shutil`, `pathlib` to move, rename, or delete files.
- **Subprocesses**: `subprocess` module to run terminal commands.
- **Error handling**: use `try-except` to prevent automation crashes.

## ⚙️ Task Scheduling Tools
### ⏱️ Task Scheduler (Windows)

- Built-in Windows tool to **automatically run scripts** at set times or events.
- Example: run a Python script every morning at 8 AM.
- Add your script path:

```py
python C:\path\to\script.py
```
- Use when automating on Windows systems.

Use when automating on Windows systems.

### 🐧 Crontab (Linux/macOS)

- Linux/macOS equivalent of Task Scheduler.
- Uses cron jobs to execute scripts periodically.
- Syntax:

```py
* * * * * /usr/bin/python3 /home/user/script.py
```
- Each * represents: minute, hour, day, month, weekday.
- Example: run every day at midnight:

```py
0 0 * * * /usr/bin/python3 /home/user/script.py
```

## 🌐 Web Automation & Scraping
### 🧩 Requests

- Sends HTTP requests (GET, POST, etc.) to websites.
- Used for fetching web page data (HTML, JSON, etc.).
- Example:
```py
import requests
res = requests.get("https://example.com")
print(res.text)
```
- Good for **API calls** or **static website scraping**

### 🍜 BeautifulSoup (bs4)

- Parses HTML or XML from a webpage fetched via requests.
- Extracts specific data using HTML tags and attributes.
- Example:

```py
from bs4 import BeautifulSoup
soup = BeautifulSoup(res.text, "html.parser")
titles = [t.text for t in soup.find_all("h2")]
```
- Used for **web scraping static pages**.

### 🧠 Selenium

- Automates web browsers — simulates clicks, typing, form submissions, etc.
- Useful for dynamic sites (JavaScript-heavy) where requests can’t get the rendered data.
- Example:
```py
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("https://example.com")
driver.find_element("name", "q").send_keys("Python\n")
```
- Used in **UI testing**, **data scraping**, or **repetitive web tasks**.

## ⏰ Task Automation in Python
### 📅 schedule

- Runs Python functions periodically within your script (no OS scheduler needed).
- Example:
```py
import schedule, time

def job():
    print("Running task...")

schedule.every(10).seconds.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)
```

- Great for **lightweight background automation**.

## 🖱️ Desktop & GUI Automation
### 💻 PyAutoGUI

- Controls **mouse and keyboard** programmatically.
- Can click buttons, type text, take screenshots, etc.
- Example:
```py
import pyautogui
pyautogui.moveTo(100, 200)
pyautogui.click()
pyautogui.typewrite("Hello world!")
```

- Ideal for desktop automation, repetitive GUI tasks, or testing.

## 🧩 Combining Tools

| Goal                               | Tools to Use                            |
| ---------------------------------- | --------------------------------------- |
| Automate web login and scrape data | `selenium`, `requests`, `BeautifulSoup` |
| Schedule periodic scripts          | `schedule`, Task Scheduler, `crontab`   |
| Automate mouse/keyboard actions    | `pyautogui`                             |
| Fetch API data                     | `requests`                              |
| Parse HTML pages                   | `BeautifulSoup`                         |
| Run system commands                | `os`, `subprocess`                      |

## 🧱 Best Practices

- Always handle exceptions to prevent script crashes.
- Use virtual environments for dependency management.
- Log script output using the logging module.
- Test your automation with dummy data first.
- Respect website robots.txt and avoid unethical scraping.

## 📚 Summary

Automation with Python revolves around:
- Scheduling (Task Scheduler, `crontab`, `schedule`)
- Web automation (Selenium, BeautifulSoup, Requests)
- GUI automation (`pyautogui`)
- OS-level scripting (`os`, `subprocess`)

Python acts as your digital assistant — handling everything from browser clicks to file management and scheduled jobs.

> [!NOTE]
> [Click Here for Project Examples!](automation_additional/mini_projects.md)
> [Click Here for more info on RPA!](automation_additional/rpa.md)