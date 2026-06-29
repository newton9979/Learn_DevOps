# Git Reset

## 📖 Introduction

`git reset` is used to move the current branch (HEAD) to a different commit. Depending on the option used, it can also modify the staging area (Index) and the working directory.

Unlike `git restore`, `git reset` can change Git history, making it a powerful but potentially dangerous command.

> **Note:** Be careful when using `git reset`, especially `--hard`, as it can permanently discard uncommitted work.

---

# Why Use Git Reset?

You can use `git reset` when:

- You want to undo the last commit.
- You accidentally staged files.
- You want to remove commits before pushing.
- You need to move your branch to an earlier commit.
- You want to clean up your local commit history.

---

# Git Reset Workflow

```
                Commit History

A ----- B ----- C ----- D (HEAD)

git reset --soft HEAD~1

A ----- B ----- C (HEAD)

```

The behavior of the staging area and working directory depends on the reset option used.

---

# Git Reset Modes

There are three commonly used reset modes:

| Mode | Commit History | Staging Area | Working Directory |
|------|----------------|--------------|-------------------|
| `--soft` | ✅ Changed | ❌ Preserved | ❌ Preserved |
| `--mixed` *(Default)* | ✅ Changed | ✅ Reset | ❌ Preserved |
| `--hard` | ✅ Changed | ✅ Reset | ✅ Reset |

---

# 1. Soft Reset

### Syntax

```bash
git reset --soft HEAD~1
```

### What It Does

- Removes the latest commit.
- Keeps all changes staged.
- Files remain unchanged.

### Example

```
Commit History

A → B → C (HEAD)

git reset --soft HEAD~1

A → B (HEAD)

Changes from C remain staged.
```

Check status:

```bash
git status
```

Output:

```
Changes to be committed:
```

---

# 2. Mixed Reset (Default)

### Syntax

```bash
git reset HEAD~1
```

or

```bash
git reset --mixed HEAD~1
```

### What It Does

- Removes the latest commit.
- Unstages the changes.
- Keeps the modified files.

Example:

Before:

```
Committed
```

After reset:

```
Modified but not staged
```

---

# 3. Hard Reset

### Syntax

```bash
git reset --hard HEAD~1
```

### What It Does

- Removes the latest commit.
- Removes staged changes.
- Removes working directory changes.

Everything after the target commit is deleted.

> ⚠️ Warning:
>
> `git reset --hard` permanently discards uncommitted work unless it can be recovered using `git reflog`.

---

# Reset to a Specific Commit

View commit history:

```bash
git log --oneline
```

Example:

```
a2b3c4d Fourth Commit
b3c4d5e Third Commit
c4d5e6f Second Commit
```

Reset to a specific commit:

```bash
git reset --hard b3c4d5e
```

HEAD now points to:

```
Third Commit
```

---

# Unstage Files

If you accidentally staged a file:

```bash
git add app.py
```

Remove it from staging:

```bash
git reset app.py
```

Status changes from:

```
Changes to be committed
```

to

```
Changes not staged for commit
```

---

# Practical Example

## Step 1

Create a file.

```bash
echo "Version 1" > demo.txt
```

---

## Step 2

Commit.

```bash
git add .
git commit -m "Version 1"
```

---

## Step 3

Modify the file.

```bash
echo "Version 2" >> demo.txt
```

Commit again.

```bash
git add .
git commit -m "Version 2"
```

---

## Step 4

Check history.

```bash
git log --oneline
```

Example:

```
9d2e5f2 Version 2
7b4c1d0 Version 1
```

---

## Step 5

Undo the latest commit.

```bash
git reset --soft HEAD~1
```

Result:

- Commit removed
- Changes still staged

---

## Step 6

Undo again using mixed reset.

```bash
git reset --mixed HEAD~1
```

Result:

- Commit removed
- Files modified
- Nothing staged

---

## Step 7

Hard reset.

```bash
git reset --hard HEAD
```

Result:

Working directory matches the latest commit.

---

# HEAD Explained

HEAD points to the current commit.

```
HEAD
 │
 ▼

A → B → C
```

Move back one commit:

```bash
git reset HEAD~1
```

```
HEAD
 │
 ▼

A → B
```

---

# Git Reset vs Git Restore

| Git Reset | Git Restore |
|------------|-------------|
| Changes commit history | Does not change commit history |
| Can move HEAD | Cannot move HEAD |
| Can remove commits | Cannot remove commits |
| Used for undoing commits | Used for restoring files |

---

# Git Reset vs Git Revert

| Git Reset | Git Revert |
|------------|------------|
| Removes commits | Creates a new commit |
| Rewrites history | Preserves history |
| Best for local branches | Best for shared branches |
| Riskier | Safer for teams |

---

# Best Practices

✅ Use `--soft` if you only want to edit the last commit.

✅ Use `--mixed` for unstaging files.

✅ Use `--hard` only when you are certain you no longer need the changes.

✅ Always check the commit history before resetting.

```bash
git log --oneline
```

✅ Create a backup branch before performing risky resets.

```bash
git branch backup-before-reset
```

---

# Common Mistakes

### Mistake 1

Using:

```bash
git reset --hard
```

without understanding its impact.

---

### Mistake 2

Resetting commits that have already been pushed to a shared repository.

---

### Mistake 3

Not checking commit history before resetting.

---

### Mistake 4

Confusing `git reset` with `git revert`.

---

# Summary

- `git reset` moves the HEAD pointer.
- It can modify commit history.
- `--soft` keeps changes staged.
- `--mixed` unstages changes.
- `--hard` removes commits and local changes.
- Avoid using `--hard` on important work unless you have a backup.

---

# Useful Commands

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git reset app.py
git log --oneline
git status
```

---

# Interview Questions

### What is git reset?

`git reset` moves the current branch (HEAD) to another commit and can also modify the staging area and working directory.

---

### What is the default mode of git reset?

`--mixed`

---

### What is the difference between soft, mixed, and hard reset?

- **Soft:** Removes commits, keeps staged changes.
- **Mixed:** Removes commits, unstages changes.
- **Hard:** Removes commits and discards all local changes.

---

### Is git reset safe on a shared branch?

Generally, **No**. It rewrites commit history and can cause problems for collaborators if the commits have already been pushed.

---

### When should you use git reset?

Use it to undo local commits, unstage files, or clean up local commit history before sharing changes with others.
