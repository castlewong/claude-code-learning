# Terminal Basics

> The terminal (also called "command line" or "shell") is a text window where you control your computer by typing commands instead of clicking.

---

## Why Learn the Terminal?

- Most coding tools (including Claude Code) run in the terminal
- Faster than clicking through folders for many tasks
- Required for installing software, running code, using git

---

## Opening the Terminal

| System | How to open |
|--------|------------|
| Mac | Press `Cmd + Space`, type "Terminal", press Enter |
| Windows | Press `Win`, type "cmd" or "PowerShell", press Enter |

---

## Essential Commands

### Navigation

```bash
pwd              # Print Working Directory — shows where you are
ls               # List files in current folder
ls -la           # List files with details (size, date, hidden files)
cd folder-name   # Change Directory — go into a folder
cd ..            # Go up one folder (back)
cd ~             # Go to your home folder
```

### Files and Folders

```bash
mkdir my-folder          # Make a new folder
touch my-file.txt        # Create an empty file
cp file.txt copy.txt     # Copy a file
mv file.txt new-name.txt # Move or rename a file
rm file.txt              # Delete a file (careful — no trash!)
rm -rf folder-name       # Delete a folder and everything in it (very careful!)
```

### Reading Files

```bash
cat file.txt    # Print file contents to screen
open file.txt   # Open file in default app (Mac)
```

### Useful Shortcuts

| Shortcut | What it does |
|----------|-------------|
| `Tab` | Auto-complete file/folder names |
| `↑ / ↓` arrow keys | Go through previous commands |
| `Ctrl + C` | Stop a running command |
| `Ctrl + L` | Clear the screen |
| `Ctrl + A` | Go to start of line |

---

## Understanding File Paths

A **path** is the address of a file or folder.

```
/Users/wilburwong/Documents/my-project/index.html
│      │           │          │          └─ file name
│      │           │          └─ folder
│      │           └─ folder
│      └─ your username
└─ root (the very top)
```

- **Absolute path**: starts from root `/` — works from anywhere
- **Relative path**: starts from where you are now — `./notes/file.md`

---

## Git Commands (for saving and sharing code)

```bash
git status              # See what files changed
git add file.txt        # Stage a file for saving
git add .               # Stage all changed files
git commit -m "message" # Save changes with a description
git push                # Upload changes to GitHub
git pull                # Download latest changes from GitHub
git log --oneline       # See recent saves (commits)
```

---

## Installing Things

```bash
# Node.js packages
npm install package-name     # Install locally
npm install -g package-name  # Install globally (available everywhere)

# Check if something is installed
node --version
npm --version
git --version
```
