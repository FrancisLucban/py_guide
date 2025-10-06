# 🔍 `glob` — Pattern Matching in File Paths

## 📘 Purpose

`glob` finds **files or folders matching wildcard patterns** (`*`, `?`, etc.).
It’s simpler than manually looping with `os.listdir()`.

---

## 🔧 Basic Usage

```py
import glob

glob.glob("*.txt")            # All .txt files in current folder
glob.glob("folder/*.py")      # All Python files in a folder
glob.glob("**/*.txt", recursive=True)  # All .txt files (recursive)
```

## 🧩 Wildcards

| Pattern | Matches                  |
| ------- | ------------------------ |
| `*`     | any number of characters |
| `?`     | any single character     |
| `[abc]` | any of a, b, or c        |
| `[0-9]` | any single digit         |


Example:

```py
glob.glob("data_?.csv")     # → data_1.csv, data_2.csv
```

## 📁 Practical Example

Organize all `.jpg` files found recursively:

```py
import glob, shutil, os

for img in glob.glob("**/*.jpg", recursive=True):
    shutil.move(img, "Images/")
```

## 🧩 Combined Usage Example

```py
import os, shutil, glob

src = "Downloads"
dest = "Documents/PDFs"

os.makedirs(dest, exist_ok=True)

for file in glob.glob(f"{src}/*.pdf"):
    shutil.move(file, dest)

print("All PDFs moved successfully!")
```

[Go Back](/py_automation.md)