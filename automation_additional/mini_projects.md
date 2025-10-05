# 🧪 Mini Project Examples

## 📨 1. Auto Email Sender

**Goal:** Automatically send daily or weekly reports.

**Libraries:** `smtplib`, `email`, `schedule` (or Task Scheduler/Crontab).

**Key Steps:**

```py
import smtplib
from email.mime.text import MIMEText

msg = MIMEText("Hello, this is your daily report.")
msg["Subject"] = "Daily Report"
msg["From"] = "you@example.com"
msg["To"] = "target@example.com"

with smtplib.SMTP("smtp.gmail.com", 587) as server:
    server.starttls()
    server.login("you@example.com", "yourpassword")
    server.send_message(msg)
```
Automate it daily using `schedule` or an OS scheduler.

## 🌐 2. Website Data Scraper

**Goal:** Collect titles or prices from an e-commerce page.

**Libraries:** `requests`, `BeautifulSoup`

**Key Steps:**

```py
import requests
from bs4 import BeautifulSoup

res = requests.get("https://example.com/products")
soup = BeautifulSoup(res.text, "html.parser")

for item in soup.select(".product"):
    print(item.select_one(".title").text, "-", item.select_one(".price").text)
```

Export results to CSV for analysis.

## 🤖 3. Auto Website Login & Form Filler

**Goal:** Log in and submit a form automatically.

**Libraries:** `selenium`

**Key Steps:**

```py
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://example.com/login")

driver.find_element("name", "username").send_keys("myuser")
driver.find_element("name", "password").send_keys("mypass")
driver.find_element("id", "login").click()
```
Can be extended to scrape or download data after login.

## 🗂️ 4. Automatic File Organizer

**Goal:** Sort downloaded files by extension.

**Libraries:** `os`, `shutil`

**Key Steps:**

```py
import os, shutil

src = "C:/Users/Me/Downloads"
dest_map = {
    ".jpg": "Images",
    ".pdf": "Documents",
    ".mp3": "Music"
}

for f in os.listdir(src):
    ext = os.path.splitext(f)[1]
    if ext in dest_map:
        shutil.move(f"{src}/{f}", f"{src}/{dest_map[ext]}/{f}")
```
Schedule it to run daily using Task Scheduler or crontab.

## 🖱️ 5. Desktop Repetitive Task Bot

**Goal:** Automate GUI actions like clicking a button or typing text.

**Libraries:** `pyautogui`

**Key Steps:**

```py
import pyautogui, time

time.sleep(3)  # Wait before automation starts
pyautogui.moveTo(100, 200)
pyautogui.click()
pyautogui.typewrite("Automated message!")
```
Can be used for repetitive desktop inputs or app testing.

## 📅 6. Automated Script Runner

**Goal:** Run a task periodically within the script.

**Libraries:** `schedule`, `time`

**Key Steps:**

```py
import schedule, time

def task():
    print("Running scheduled task...")

schedule.every(10).minutes.do(task)

while True:
    schedule.run_pending()
    time.sleep(1)
```
Alternative to using Task Scheduler or crontab.

## 📂 7. System Maintenance Script

**Goal:** Clean temp folders, backup logs, and free up disk space.

**Libraries:** `os`, `shutil`, `datetime`

**Key Steps:**

```py
import os, shutil, datetime

backup_dir = f"backup_{datetime.date.today()}"
os.makedirs(backup_dir, exist_ok=True)

for f in os.listdir("logs"):
    shutil.move(f"logs/{f}", f"{backup_dir}/{f}")

shutil.rmtree("temp")  # Delete temp folder
```
Useful for automating system hygiene tasks.

## 🧩 Practice Flow

1. Start with **file automation** (organizing files).
2. Move to **web scraping and APIs**.
3. Then try **browser automation** with Selenium.
4. Finally, integrate **scheduling** to make your scripts fully automatic.