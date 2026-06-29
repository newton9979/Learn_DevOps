# Git Reflog

## 📖 Introduction

`git reflog` (Reference Log) is one of Git's most powerful recovery tools. It records every change made to the **HEAD** and branch references, allowing you to recover commits that may appear to be lost.

Even if a commit is no longer visible in `git log`, it can often be recovered using `git reflog`.

> **Note:** Think of `git reflog` as Git's "recovery history" or "undo history." It helps you recover from accidental resets, rebases, branch deletions, and other mistakes.

---

# Why Use Git Reflog?

You can use `git reflog` to:

- Recover deleted commits.
- Recover from an accidental `git reset --hard`.
- Recover lost commits after a rebase.
- Restore accidentally deleted branches.
- Find previous HEAD positions.
- Undo mistakes safely.

---

# How Git Reflog Works

Unlike `git log`, which shows commit history, `git reflog` records **every movement of HEAD**.

```
Commit History

A ---- B ---- C ---- D (HEAD)

git reset --hard B

Commit History

A ---- B (HEAD)

Git Log

A ---- B

Git Reflog

HEAD@{0} reset to B
HEAD@{1} commit D
HEAD@{2} commit C
HEAD@{3} commit B
HEAD@{4} commit A
```

Although commits **C** and **D** are no longer visible in `git log`, they can still be recovered using `git reflog`.

---

# Basic Syntax

```bash
git reflog
```

Example Output

```
9c7d4f2 HEAD@{0}: reset: moving to HEAD~2
5b8a1d9 HEAD@{1}: commit: Added Login Feature
4a7c6d2 HEAD@{2}: commit: Updated README
```

Each entry records an action performed on the repository.

---

# View Reflog History

```bash
git reflog
```

Example

```
HEAD@{0}: checkout: moving from main to feature
HEAD@{1}: commit: Added Dockerfile
HEAD@{2}: commit: Updated README
HEAD@{3}: reset: moving to HEAD~1
```

---

# Recover After a Hard Reset

Suppose you accidentally run:

```bash
git reset --hard HEAD~2
```

Your recent commits disappear.

View the reflog:

```bash
git reflog
```

Example

```
HEAD@{0}: reset: moving to HEAD~2
HEAD@{1}: commit: Added Login
HEAD@{2}: commit: Added Dashboard
```

Recover the lost commit:

```bash
git reset --hard HEAD@{1}
```

or

```bash
git reset --hard <commit-id>
```

Your commits are restored.

---

# Recover a Deleted Commit

View the reflog:

