# 🥣 BeautifulSoup Cheatsheet (Python)

## 📦 Import & Setup

```py
from bs4 import BeautifulSoup

# Load HTML
soup = BeautifulSoup(html_content, 'html.parser')
# You can also use 'lxml' or 'html5lib' as parsers
```

---

## 🔍 Basic Navigation

| Action               | Syntax                               | Description                       |
| -------------------- | ------------------------------------ | --------------------------------- |
| Get the first tag    | `soup.tagname`                       | e.g., `soup.title`                |
| Get text inside tag  | `soup.tagname.text` or `.get_text()` | Returns the inner text            |
| Find tag by name     | `soup.find('tag')`                   | Returns the **first** match       |
| Find all tags        | `soup.find_all('tag')`               | Returns a list of matches         |
| Access tag attribute | `tag['attr']`                        | e.g., `link['href']`              |
| Get all attributes   | `tag.attrs`                          | Returns a dict of attributes      |
| Get parent tag       | `tag.parent`                         | Access parent element             |
| Get children         | `tag.children`                       | Returns an iterator of child tags |

---

## 🎯 Searching with Attributes

```py
soup.find('div', id='main')
soup.find_all('a', class_='link')
soup.find_all('img', {'src': True})
```

## 💬 CSS Selectors (Shortcut)

```py
soup.select('div.classname')          # By class
soup.select('#idname')                # By ID
soup.select('div > p')                # Direct child
soup.select('a[href^="https"]')       # Attribute starts with
Returns a list — access first match with [0].
```

## 🧹 Extracting & Modifying

```py
tag.decompose()      # Remove tag completely
tag.extract()        # Remove but keep content
tag['attr'] = 'new'  # Modify attribute
tag.string = "Hello" # Change text
```

## 🧾 Example

```py
html = '<html><body><h1>Hello</h1><p class="desc">World</p></body></html>'
soup = BeautifulSoup(html, 'html.parser')

print(soup.h1.text)                 # Hello
print(soup.find('p', class_='desc').text)  # World
```

## ⚙️ Common Parsers

| Parser          | Install                | Notes                   |
| --------------- | ---------------------- | ----------------------- |
| `'html.parser'` | built-in               | Fast, decent            |
| `'lxml'`        | `pip install lxml`     | Fastest, best structure |
| `'html5lib'`    | `pip install html5lib` | Most lenient, slowest   |

---

## 🕸️ Example: Scraping Titles and Links

```py
import requests
from bs4 import BeautifulSoup

# URL to scrape
url = "https://example.com"

# Fetch the page content
response = requests.get(url)
html = response.text

# Parse with BeautifulSoup
soup = BeautifulSoup(html, "html.parser")

# Find all <a> tags
links = soup.find_all("a")

# Print titles and links
for link in links:
    title = link.text.strip()
    href = link.get("href")

    if href:  # Ensure it has an href attribute
        print(f"Title: {title if title else 'No text'}")
        print(f"Link: {href}")
        print("-" * 40)
```

### 🧠 What’s Happening

1. `requests.get(url)` → downloads the webpage’s HTML.
2. `BeautifulSoup(html, 'html.parser')` → converts it into a navigable structure.
3. `soup.find_all("a")` → grabs all anchor (`<a>`) elements.
4. Loops through each link to get:
    - `link.text` → the clickable text.
    - `link.get('href')` → the URL.

### 🧩 Optional Filtering Example

You can filter links or titles easily:

```py
# Only show links containing 'blog'
for link in soup.find_all('a', href=True):
    if 'blog' in link['href']:
        print(link['href'])
```

[Go Back](/py_automation.md)
