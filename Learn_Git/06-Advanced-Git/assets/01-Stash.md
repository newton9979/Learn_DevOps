# 📘 Git Stash

## 📖 Introduction

While working on a project, there are times when you need to switch branches or work on another task before your current changes are complete. However, Git does not allow you to switch branches if your uncommitted changes would be overwritten.

**Git Stash** provides a temporary storage area for your uncommitted changes. It saves your work, restores your working directory to a clean state, and allows you to continue working elsewhere. Later, you can reapply your saved changes whenever you are ready.

Git Stash is one of the most frequently used features by developers, DevOps engineers, and production support teams because it helps manage interruptions without creating unnecessary commits.

---

# 🎯 Learning Objectives

After completing this topic, you will understand:

* What Git Stash is
* Why Git Stash is useful
* How Git Stash works
* Common Git Stash commands
* Real-world use cases
* Best practices
* Common mistakes

---

# 🤔 Why Do We Need Git Stash?

Imagine you're working on a new feature.

```
Feature A (50% completed)
```

Suddenly, production reports a critical bug.

You need to:

* Switch to the production branch
* Fix the bug
* Commit the fix
* Return to your feature

Your feature isn't ready for a commit yet.

Instead of making a temporary commit, you can simply stash your changes.

```
Current Work
      │
      ▼
git stash
      │
Working Directory Clean
      │
Fix Production Issue
      │
Switch Back
      │
git stash pop
      │
Continue Development
```

---

# ⚙️ How Git Stash Works

Git Stash temporarily stores:

* Modified tracked files
* Staged changes

By default, it does **not** stash:

* Untracked files
* Ignored files

These can be included using additional options.

---

# 📊 Git Stash Workflow

```
Developer Changes Files
          │
          ▼
git status
          │
          ▼
git stash
          │
          ▼
Working Directory Becomes Clean
          │
          ▼
Switch Branch
          │
          ▼
Complete Another Task
          │
          ▼
Return to Original Branch
          │
          ▼
git stash pop
          │
          ▼
Continue Working
```

---

# 🛠️ Common Git Stash Commands

## Save Changes

```bash
git stash
```

Temporarily stores your changes.

---

## View All Stashes

```bash
git stash list
```

Example:

```text
stash@{0}: WIP on main: 8d5f34a Added login page
stash@{1}: WIP on dev: 2e6ab43 Updated README
```

---

## Apply Latest Stash

```bash
git stash apply
```

Applies the latest stash but keeps it in the stash list.

---

## Apply Specific Stash

```bash
git stash apply stash@{1}
```

---

## Apply and Remove Stash

```bash
git stash pop
```

This is the most commonly used command.

---

## Delete a Stash

```bash
git stash drop stash@{0}
```

---

## Remove All Stashes

```bash
git stash clear
```

---

## Stash Including Untracked Files

```bash
git stash -u
```

or

```bash
git stash --include-untracked
```

---

## Stash Everything Including Ignored Files

```bash
git stash -a
```

---

# 💻 Example

Current status:

```bash
git status
```

Output:

```text
modified: app.py
modified: README.md
```

Save changes:

```bash
git stash
```

Verify:

```bash
git status
```

Output:

```text
nothing to commit, working tree clean
```

Restore:

```bash
git stash pop
```

Your changes return exactly as they were.

---

# 🌍 Real-World Use Cases

### Production Support

A critical issue occurs while you're developing a feature.

Instead of committing incomplete work:

```bash
git stash
git checkout production
```

Fix the issue, then return and restore your work.

---

### Code Review

Your manager requests a quick review.

```bash
git stash
```

Review the code and return later.

---

### Branch Switching

Need to move to another branch quickly?

```bash
git stash
git checkout feature-payment
```

---

# ✅ Best Practices

* Use stash only for temporary work.
* Give meaningful names to stashes.

```bash
git stash push -m "Working on login API"
```

* Clean unused stashes regularly.
* Prefer proper commits for completed work.
# 📊 Git Stash Workflow

The following diagram illustrates how Git Stash temporarily saves your work, allows you to switch tasks, and restores your changes when you're ready.

![Git Stash Workflow](assets/git-stash-workflow.png)

```
Modify Files
      │
      ▼
git stash
      │
      ▼
Clean Working Directory
      │
      ▼
Switch Branch
      │
      ▼
Complete Another Task
      │
      ▼
Return to Original Branch
      │
      ▼
git stash pop
      │
      ▼
Continue Development
```* Verify your working tree before switching branches.

---

# ❌ Common Mistakes

### Forgetting Existing Stashes

```bash
git stash list
```

Always check before creating new ones.

---

### Using Stash as Permanent Storage

Stash is temporary.

Use commits for long-term work.

---

### Accidentally Clearing All Stashes

```bash
git stash clear
```

This permanently removes every stash.

---

# 📌 Useful Commands Summary

| Command           | Description                  |
| ----------------- | ---------------------------- |
| `git stash`       | Save current changes         |
| `git stash list`  | Show saved stashes           |
| `git stash apply` | Apply stash without deleting |
| `git stash pop`   | Apply and delete stash       |
| `git stash drop`  | Delete one stash             |
| `git stash clear` | Delete all stashes           |
| `git stash -u`    | Include untracked files      |
| `git stash -a`    | Include ignored files        |

---

# 🎤 Interview Questions

### What is Git Stash?

Git Stash temporarily saves uncommitted changes so you can work on something else without committing incomplete work.

---

### What is the difference between `git stash apply` and `git stash pop`?

* `apply` restores the stash and keeps it.
* `pop` restores the stash and removes it from the stash list.

---

### How do you view saved stashes?

```bash
git stash list
```

---

### Can Git Stash save untracked files?

Yes.

```bash
git stash -u
```

---

### How do you delete a specific stash?

```bash
git stash drop stash@{0}
```

---
# 📊 Git Stash Workflow

The following diagram illustrates how Git Stash temporarily saves your work, allows you to switch tasks, and restores your changes when you're ready.

![Git Stash Workflow](assets/git-stash-workflow.png)

```
Modify Files
      │
      ▼
git stash
      │
      ▼
Clean Working Directory
      │
      ▼
Switch Branch
      │
      ▼
Complete Another Task
      │
      ▼
Return to Original Branch
      │
      ▼
git stash pop
      │
      ▼
Continue Development
```
# 📝 Summary

Git Stash is an essential Git feature for temporarily saving uncommitted changes without creating unnecessary commits. It enables developers to switch tasks, fix urgent issues, or change branches while preserving ongoing work. Understanding Git Stash improves productivity and helps maintain a clean commit history.

