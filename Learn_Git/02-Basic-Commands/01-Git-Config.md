# 01. Git Config

## What is Git Config?

`git config` is used to configure Git settings for your system, user account, or a specific repository.

Git stores configuration settings such as:

* User name
* Email address
* Default editor
* Default branch name
* Merge and pull behavior
* Aliases

These settings help Git identify who is making changes and how Git should behave.

---

## Why Git Config is Important?

Before making commits, Git needs to know:

* Who you are
* Your email address

Every commit contains metadata like:

```text
Author: Newton Babu Nandru
Email : newton@example.com
```

Without configuring Git, commits may fail or show incorrect author information.

---

## Git Configuration Levels

Git supports three configuration levels.

```text
+----------------------+
|   System Level       |
|  (/etc/gitconfig)    |
+----------+-----------+
           |
           v
+----------------------+
|    Global Level      |
| (~/.gitconfig)       |
+----------+-----------+
           |
           v
+----------------------+
| Repository Level     |
| (.git/config)        |
+----------------------+
```

### 1. System Level

Applies to all users on the machine.

```bash
git config --system user.name "Newton"
```

### 2. Global Level

Applies to the current user.

```bash
git config --global user.name "Newton Babu"
git config --global user.email "newton@example.com"
```

Stored in:

```bash
~/.gitconfig
```

### 3. Local (Repository) Level

Applies only to a specific Git repository.

```bash
git config --local user.name "Project User"
git config --local user.email "project@example.com"
```

Stored in:

```bash
.git/config
```

---

## Configuration Priority

```text
Local Repository Config
          ↑
Global Config
          ↑
System Config
```

The local configuration overrides global, and global overrides system.

Example:

```bash
# Global
git config --global user.name "Newton"

# Local Repository
git config --local user.name "DevOps Engineer"
```

Inside that repository:

```text
Author = DevOps Engineer
```

---

## Configure Username

```bash
git config --global user.name "Newton Babu Nandru"
```

Verify:

```bash
git config --global user.name
```

Output:

```text
Newton Babu Nandru
```

---

## Configure Email

```bash
git config --global user.email "newton@example.com"
```

Verify:

```bash
git config --global user.email
```

Output:

```text
newton@example.com
```

---

## View All Configurations

```bash
git config --list
```

Example Output:

```text
user.name=Newton Babu Nandru
user.email=newton@example.com
core.editor=vim
init.defaultBranch=main
```

---

## Check Specific Configuration

```bash
git config user.name
```

```bash
git config user.email
```

---

## Show Configuration Source

Useful for troubleshooting.

```bash
git config --list --show-origin
```

Example:

```text
file:/home/ubuntu/.gitconfig user.name=Newton
file:/home/ubuntu/.gitconfig user.email=newton@example.com
```

---

## Configure Default Branch Name

Modern repositories use `main` instead of `master`.

```bash
git config --global init.defaultBranch main
```

Verify:

```bash
git config --global init.defaultBranch
```

Output:

```text
main
```

---

## Configure Default Editor

### VS Code

```bash
git config --global core.editor "code --wait"
```

### Vim

```bash
git config --global core.editor "vim"
```

### Nano

```bash
git config --global core.editor "nano"
```

Verify:

```bash
git config --global core.editor
```

---

## Configure Credential Storage

### Linux

```bash
git config --global credential.helper store
```

### Cache Credentials

```bash
git config --global credential.helper cache
```

Cache for 1 hour:

```bash
git config --global credential.helper 'cache --timeout=3600'
```

---

## Create Git Aliases

### Alias for Status

```bash
git config --global alias.st status
```

Usage:

```bash
git st
```

### Alias for Log

```bash
git config --global alias.lg log
```

Usage:

```bash
git lg
```

### Alias for Checkout

```bash
git config --global alias.co checkout
```

Usage:

```bash
git co main
```

---

## Real-World Example

### Initial Git Setup on a New Machine

```bash
git config --global user.name "Newton Babu Nandru"

git config --global user.email "newton@example.com"

git config --global init.defaultBranch main

git config --global core.editor "code --wait"

git config --list
```

Expected Output:

```text
user.name=Newton Babu Nandru
user.email=newton@example.com
init.defaultBranch=main
core.editor=code --wait
```

---

## Hands-On Lab

### Step 1: Check Existing Config

```bash
git config --list
```

### Step 2: Set Username

```bash
git config --global user.name "Newton Babu Nandru"
```

### Step 3: Set Email

```bash
git config --global user.email "newton@example.com"
```

### Step 4: Verify Settings

```bash
git config --list
```

### Step 5: Check Individual Values

```bash
git config user.name
git config user.email
```

---

## Git Config Workflow Diagram

```text
                Git Configuration

                        |
        +---------------+---------------+
        |                               |
        v                               v

 System Config                    Global Config
 (/etc/gitconfig)                 (~/.gitconfig)
        |                               |
        +---------------+---------------+
                        |
                        v

                Local Repository
                  (.git/config)

                        |
                        v

                 Git Commands
                        |
                        v

              Commits & Repository
```

---

## Common Interview Questions

### Q1. What does `git config` do?

**Answer:**
It configures Git settings such as username, email, editor, aliases, and repository behavior.

### Q2. What are the three Git configuration levels?

**Answer:**

1. System
2. Global
3. Local (Repository)

### Q3. Which configuration has the highest priority?

**Answer:**

```text
Local > Global > System
```

### Q4. How do you see all Git configurations?

```bash
git config --list
```

### Q5. How do you check where a configuration came from?

```bash
git config --list --show-origin
```

---

# Key Takeaways

✅ `git config` manages Git settings.

✅ Configure username and email before making commits.

✅ Three levels of configuration:

```text
System → Global → Local
```

✅ Local configuration overrides global settings.

✅ Use `git config --list` to view all settings.

✅ Use aliases to simplify Git commands.

✅ Set the default branch to `main`.

---

## Quick Reference

```bash
# Set username
git config --global user.name "Newton Babu Nandru"

# Set email
git config --global user.email "newton@example.com"

# View all configs
git config --list

# Show config source
git config --list --show-origin

# Set default branch
git config --global init.defaultBranch main

# Set editor
git config --global core.editor "code --wait"

# Create alias
git config --global alias.st status
```

