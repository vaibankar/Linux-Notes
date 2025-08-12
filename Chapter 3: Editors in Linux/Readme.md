# ✏️ Text Editors in Linux

Text editors are essential tools for working in a Linux environment. They are used for editing configuration files, writing scripts, coding programs, and general text processing.

This document provides a comprehensive overview of **command-line** and **GUI-based editors** available in Linux.

---

## 📂 Types of Editors in Linux

### 1. 📟 Command-Line Editors
These editors work inside the terminal and are ideal for server environments or when working over SSH.

### 2. 🖥️ Graphical Editors
These editors require a desktop environment and provide a graphical user interface (GUI) with menus, buttons, and mouse interaction.

---

## 📟 Common Command-Line Editors

### 🔹 1. `nano` – Simple and User-Friendly

- Easy to use for beginners
- Displays shortcuts at the bottom
- Great for quick edits

#### ✅ Basic Commands:
| Command | Action |
|--------|--------|
| `nano filename` | Open or create a file |
| `Ctrl + O` | Save file |
| `Ctrl + X` | Exit nano |
| `Ctrl + K` | Cut a line |
| `Ctrl + U` | Paste a line |

---

### 🔹 2. `vim` – Powerful and Advanced

- Modal editor: Normal, Insert, Visual, Command modes
- Preferred by power users and sysadmins
- Extensive plugin and configuration options

#### ✅ Modes:
- `Normal`: For navigating and commands (default)
- `Insert`: For editing text (`i`, `a`, etc.)
- `Visual`: For selecting text
- `Command`: For executing `:` commands

#### ✅ Basic Commands:
| Command | Action |
|--------|--------|
| `vim filename` | Open a file |
| `i` | Enter insert mode |
| `Esc` | Exit insert mode to normal mode |
| `:w` | Save file |
| `:q` | Quit |
| `:wq` | Save and quit |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |

> To install: `sudo apt install vim`

---

### 🔹 3. `vi` – The Original Visual Editor

- Lightweight and available on almost all Unix/Linux systems
- A precursor to `vim`, with more limited features

---

### 🔹 4. `ed`, `sed` – Line Editors and Stream Editors

- `ed`: Line-by-line editor (rarely used interactively today)
- `sed`: Used for stream editing (non-interactive), ideal in scripts

#### Example:
```bash
sed 's/old/new/g' file.txt > newfile.txt
