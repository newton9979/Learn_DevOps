# 02. Git Init

## What is Git Init?

`git init` is the command used to create a new Git repository.

It initializes an empty Git repository by creating a hidden `.git` directory that stores all Git metadata, commit history, branches, configuration, and objects.

### Syntax

```bash
git init
```

---

## Why Do We Need Git Init?

Before Git can track files, a repository must be initialized.

Without running `git init`, Git commands such as:

```bash
git status
git add
git commit
```

will not work because Git doesn't know that the directory should be treated as a repository.

---

## What Happens When You Run Git Init?

When you execute:

```bash
git init
```

Git creates a hidden `.git` directory.

Example:

```bash
mkdir my-project
cd my-project
git init
```

Output:

```text
Initialized empty Git repository in /home/user/my-project/.git/
```

---

## Repository Structure

Before `git init`:

```text
my-project/
│
├── app.py
├── README.md
└── config.yaml
```

After `git init`:

```text
my-project/
│
├── .git/
├── app.py
├── README.md
└── config.yaml
```

---

## Inside the .git Directory

The `.git` directory contains all repository information.

```text
.git/
│
├── HEAD
├── config
├── description
├── hooks/
├── info/
├── objects/
└── refs/
```

### Important Components

| Component | Purpose                         |
| --------- | ------------------------------- |
| HEAD      | Points to the current branch    |
| config    | Repository configuration        |
| objects   | Stores commits and files        |
| refs      | Stores branches and tags        |
| hooks     | Scripts triggered by Git events |

---

# Basic Usage

## Initialize a New Repository

```bash
mkdir my-project
cd my-project

git init
```

Output:

```text
Initialized empty Git repository
```

---

## Verify Repository Initialization

Run:

```bash
ls -la
```

Linux/macOS Output:

```text
drwxr-xr-x .git
```

Or:

```bash
git status
```

Output:

```text
On branch main

No commits yet

nothing to commit
```

---

# Initialize with Custom Branch Name

By default, modern Git versions use `main`.

You can explicitly define the default branch:

```bash
git init -b main
```

Example:

```bash
mkdir demo
cd demo

git init -b main
```

Output:

```text
Initialized empty Git repository
```

---

# Reinitialize an Existing Repository

If a repository already exists:

```bash
git init
```

Output:

```text
Reinitialized existing Git repository
```

This does not delete commits or history.

---

# Real-World Example

### Create a New DevOps Project

Step 1: Create Project Directory

```bash
mkdir aws-devops-project
cd aws-devops-project
```

Step 2: Initialize Git

```bash
git init
```

Step 3: Create Files

```bash
touch README.md

mkdir terraform

mkdir scripts
```

Step 4: Verify Status

```bash
git status
```

Output:

```text
Untracked files:
README.md
terraform/
scripts/
```

Git is now ready to track files.

---

# Git Init Workflow Diagram

```text
                Create Project Folder
                          |
                          v
                  mkdir my-project
                          |
                          v
                     cd my-project
                          |
                          v
                       git init
                          |
                          v
                .git Directory Created
                          |
                          v
                 Git Repository Ready
                          |
                          v
               Add → Commit → Push
```

---

# Visual Repository Lifecycle

```text
+----------------+
| Project Folder |
+--------+-------+
         |
         v

+----------------+
|   git init     |
+--------+-------+
         |
         v

+----------------+
| .git Created   |
+--------+-------+
         |
         v

+----------------+
| Git Tracking   |
+--------+-------+
         |
         v

+----------------+
| Add & Commit   |
+----------------+
```

---

# Common Errors

## Error 1

```bash
git status
```

Output:

```text
fatal: not a git repository
```

Reason:

You have not initialized Git.

Solution:

```bash
git init
```

---

## Error 2

Running Git commands from the wrong directory.

Check current directory:

```bash
pwd
```

Move into repository:

```bash
cd my-project
```

---

# Hands-On Lab

## Lab 1: Create Your First Repository

### Step 1

Create a folder:

```bash
mkdir git-lab
```

### Step 2

Move into folder:

```bash
cd git-lab
```

### Step 3

Initialize Git:

```bash
git init
```

### Step 4

Verify:

```bash
git status
```

Expected Output:

```text
On branch main

No commits yet
```

### Step 5

Create a file:

```bash
touch README.md
```

### Step 6

Check status:

```bash
git status
```

Output:

```text
Untracked files:
README.md
```

---

# Git Init vs Git Clone

| Feature                    | git init | git clone |
| -------------------------- | -------- | --------- |
| Creates Repository         | Yes      | Yes       |
| Downloads Existing Code    | No       | Yes       |
| Creates .git Folder        | Yes      | Yes       |
| Used for New Projects      | Yes      | No        |
| Used for Existing Projects | No       | Yes       |

Example:

Create new repository:

```bash
git init
```

Download existing repository:

```bash
git clone https://github.com/user/project.git
```

---

# Common Interview Questions

## Q1. What is the purpose of `git init`?

**Answer:**

It creates a new Git repository by generating a hidden `.git` directory.

---

## Q2. What does the `.git` folder contain?

**Answer:**

Repository metadata, commit history, branches, tags, configuration files, and Git objects.

---

## Q3. Can `git init` be executed multiple times?

**Answer:**

Yes.

Running it again reinitializes the repository without affecting existing commits.

---

## Q4. How do you create a repository with `main` as the default branch?

```bash
git init -b main
```

---

## Q5. How do you verify a Git repository exists?

```bash
git status
```

or

```bash
ls -la
```

Look for the `.git` directory.

---

# Key Takeaways

✅ `git init` creates a new Git repository.

✅ Creates a hidden `.git` directory.

✅ Enables Git tracking and version control.

✅ Must be run before using `git add`, `git commit`, or `git push`.

✅ Can safely reinitialize an existing repository.

✅ `git init` is used for new projects.

✅ `git clone` is used for existing remote repositories.

---

# Quick Reference

```bash
# Initialize repository
git init

# Initialize with main branch
git init -b main

# Check repository status
git status

# View hidden files
ls -la

# Verify current location
pwd
```

