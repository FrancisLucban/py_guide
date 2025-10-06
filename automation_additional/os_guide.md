# 🧱 `os` — Operating System Interface

## 📘 Purpose

The `os` module lets you **interact with the operating system** — handling file paths, directories, environment variables, and executing commands.

---

## 📁 Directory & File Operations

```py
import os

os.getcwd()               # Get current working directory
os.chdir("path/to/dir")   # Change directory
os.listdir()              # List files in current directory
os.mkdir("new_folder")    # Create a single directory
os.makedirs("a/b/c")      # Create nested directories
os.rmdir("folder")        # Remove empty directory
os.remove("file.txt")     # Delete a file
os.rename("old.txt", "new.txt")  # Rename or move file
os.path.exists("file.txt")       # Check if file/folder exists
```

## 📂 Path Manipulation

Use os.path utilities to safely handle paths.

```py
from os import path

path.join("folder", "file.txt")  # Combine paths safely
path.basename("/home/user/file.txt")  # → 'file.txt'
path.dirname("/home/user/file.txt")   # → '/home/user'
path.splitext("file.txt")             # → ('file', '.txt')
path.getsize("file.txt")              # → returns size in bytes
path.abspath("file.txt")              # → full path
```

## ⚙️ Running System Commands

```py
os.system("echo Hello World")     # Run shell commands (simple)
```

For safer, advanced command execution → use `subprocess` module.

## 🌍 Environment Variables

```py
os.environ["PATH"]        # Access environment variables
os.getenv("USERNAME")     # Safer way to get env variable
```

## 🧭 Walking Through Directories

Iterate through all subdirectories and files.

```py
for root, dirs, files in os.walk("myfolder"):
    print(root, dirs, files)
```

[Go Back](/py_automation.md)