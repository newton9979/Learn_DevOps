# 08. Git Show

## What is Git Show?

`git show` is used to display detailed information about Git objects such as:

* Commits
* Tags
* Branch references
* File changes

It combines information from commands like:

```bash
git log
git diff
```

and provides a detailed view of a specific commit, including the changes made.

### Syntax

```bash
git show
```

or

```bash
git show <commit-id>
```

Example:

```bash
git show a1b2c3d
```

---

# Why Git Show is Important?

Developers use `git show` to:

* Review commit details
* Inspect code changes
* Verify commit history
* Troubleshoot issues
* Understand who changed what and when

Think of `git show` as a **commit inspection tool**.

---

# What Does Git Show Display?

When executed:

```bash
git show
```

Git displays:

1. Commit ID
2. Author Information
3. Commit Date
4. Commit Message
5. File Differences (Diff)

Example:

```text
commit a1b2c3d4e5f67890123456789abcdef12345678
Author: Newton Babu Nandru <newton@example.com>
Date: Tue Jun 23 10:00:00 2026 +0530

    Added login functionality

diff --git a/app.py b/app.py
index 123abc..456def 100644

-print("Hello")
+print("Hello Git")
```

---

# Git Show Workflow

```text
                Git Repository
                       |
                       v
                  git show
                       |
                       v
              Display Commit Info
                       |
                       v
             Show Code Differences
```

---

# Basic Usage

## Show Latest Commit

```bash
git show
```

Displays:

* Latest commit
* Commit message
* Author details
* File changes

---

## Show Specific Commit

```bash
git show <commit-id>
```

Example:

```bash
git show a1b2c3d
```

Output:

```text
commit a1b2c3d

Added README file
```

---

# Show Commit in One Line

```bash
git show --oneline
```

Example:

```text
a1b2c3d Added README file
```

---

# Show Commit Statistics

```bash
git show --stat
```

Example:

```text
 README.md | 10 ++++++++++
 app.py    | 20 ++++++++++++++++++++

 2 files changed, 30 insertions(+)
```

Useful for quickly understanding the impact of a commit.

---

# Show Only Commit Information

```bash
git show --no-patch
```

or

```bash
git show -s
```

Example:

```text
commit a1b2c3d
Author: Newton
Date: Tue Jun 23

    Initial Commit
```

No file changes are displayed.

---

# Show Specific File from a Commit

Syntax:

```bash
git show <commit-id>:<file-name>
```

Example:

```bash
git show a1b2c3d:README.md
```

Output:

```text
# Project Documentation
```

Displays the file contents as they existed in that commit.

---

# Real-World Example

## Step 1: Create Repository

```bash
mkdir git-show-demo
cd git-show-demo

git init
```

---

## Step 2: Create File

```bash
echo "Version 1" > app.py
```

---

## Step 3: Commit File

```bash
git add app.py

git commit -m "Initial version"
```

---

## Step 4: Modify File

```bash
echo "Version 2" > app.py
```

---

## Step 5: Commit Changes

```bash
git add app.py

git commit -m "Update app version"
```

---

## Step 6: View Latest Commit

```bash
git show
```

Output:

```diff
commit xyz123

Update app version

-Version 1
+Version 2
```

---

# Understanding Git Show Output

Example:

```diff
commit a1b2c3d
Author: Newton
Date: Tue Jun 23

    Update README

diff --git a/README.md b/README.md

-Old Content
+New Content
```

### Components

| Section | Description         |
| ------- | ------------------- |
| Commit  | Unique commit hash  |
| Author  | Commit creator      |
| Date    | Commit timestamp    |
| Message | Commit description  |
| Diff    | Actual code changes |

---

# Git Show vs Git Log

| Feature                | git show | git log      |
| ---------------------- | -------- | ------------ |
| Shows Commit History   | Limited  | Yes          |
| Shows File Changes     | Yes      | No (default) |
| Displays Latest Commit | Yes      | Yes          |
| Detailed Commit View   | Yes      | No           |

Example:

```bash
git log --oneline
```

Output:

```text
abc123 Update README
def456 Initial commit
```

---

```bash
git show abc123
```

Output:

```diff
-Old Line
+New Line
```

---

# Git Show vs Git Diff

| Feature                 | git show | git diff |
| ----------------------- | -------- | -------- |
| Shows Commit Details    | Yes      | No       |
| Shows Differences       | Yes      | Yes      |
| Displays Author Info    | Yes      | No       |
| Displays Commit Message | Yes      | No       |

---

# Useful Git Show Commands

## Latest Commit

```bash
git show
```

---

## Specific Commit

```bash
git show <commit-id>
```

---

## Statistics Only

```bash
git show --stat
```

---

## Commit Metadata Only

```bash
git show --no-patch
```

---

## One-Line Output

```bash
git show --oneline
```

---

## Show File from Commit

```bash
git show <commit-id>:README.md
```

---

# Git Show Diagram

```text
                    Repository
                         |
                         v
                    git show
                         |
        --------------------------------
        |              |              |
        v              v              v

     Commit ID      Metadata       Diff Output
        |              |              |
        --------------------------------
                         |
                         v

                  Detailed View
```

---

# Hands-On Lab

## Lab 1: Inspect a Commit

### Step 1

Create repository:

```bash
mkdir show-lab
cd show-lab

git init
```

### Step 2

Create file:

```bash
echo "Git Version 1" > notes.txt
```

### Step 3

Commit file:

```bash
git add notes.txt

git commit -m "Version 1"
```

### Step 4

Modify file:

```bash
echo "Git Version 2" > notes.txt
```

### Step 5

Commit changes:

```bash
git add notes.txt

git commit -m "Version 2"
```

### Step 6

View latest commit:

```bash
git show
```

### Step 7

View statistics:

```bash
git show --stat
```

### Step 8

View metadata only:

```bash
git show -s
```

---

# Common Errors

## Error 1: Invalid Commit ID

Command:

```bash
git show abcxyz
```

Output:

```text
fatal: ambiguous argument 'abcxyz'
```

Solution:

View available commits:

```bash
git log --oneline
```

Use a valid commit ID.

---

## Error 2: Not a Git Repository

Command:

```bash
git show
```

Output:

```text
fatal: not a git repository
```

Solution:

```bash
git init
```

or move into an existing repository.

---

# Common Use Cases

### Review Last Commit

```bash
git show
```

---

### Verify Code Changes

```bash
git show <commit-id>
```

---

### Audit Team Contributions

```bash
git show
```

Check:

* Author
* Date
* Changes

---

### Troubleshoot Bugs

```bash
git show commit-id
```

Inspect changes that introduced a problem.

---

# Common Interview Questions

## Q1. What does `git show` do?

**Answer:**

Displays detailed information about a commit, including metadata and code changes.

---

## Q2. How do you display the latest commit?

```bash
git show
```

---

## Q3. How do you display only commit metadata?

```bash
git show --no-patch
```

or

```bash
git show -s
```

---

## Q4. How do you display statistics for a commit?

```bash
git show --stat
```

---

## Q5. How do you display a file from a specific commit?

```bash
git show <commit-id>:<file-name>
```

Example:

```bash
git show a1b2c3d:README.md
```

---

# Key Takeaways

✅ `git show` displays detailed commit information.

✅ Combines commit metadata and file differences.

✅ Useful for reviewing commits and troubleshooting issues.

✅ Supports viewing specific commits, files, and statistics.

✅ `git show -s` displays metadata only.

✅ `git show --stat` displays file-level change statistics.

---

# Quick Reference

```bash
# Show latest commit
git show

# Show specific commit
git show <commit-id>

# Show commit statistics
git show --stat

# Show metadata only
git show -s

# One-line output
git show --oneline

# Show file from commit
git show <commit-id>:<file-name>
```

