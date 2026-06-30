# 🔍 Git Bisect

## 📖 Introduction

As software projects grow, identifying the exact commit that introduced a bug becomes increasingly difficult. Imagine a scenario where your application worked perfectly last week, but after hundreds of commits, a critical issue appears. Manually checking each commit can be time-consuming and frustrating.

**Git Bisect** is a powerful debugging tool that helps you quickly locate the commit that introduced a bug. It uses the **Binary Search** algorithm, allowing Git to efficiently narrow down the search by repeatedly checking the middle commit between a known **good** commit and a known **bad** commit.

Instead of examining every commit one by one, Git Bisect dramatically reduces the number of tests required, making it an essential tool for developers, DevOps engineers, and production support teams.

---

# 🎯 Learning Objectives

After completing this topic, you will understand:

* What Git Bisect is
* Why Git Bisect is useful
* How Binary Search works in Git
* How to start and stop a bisect session
* How to identify the first bad commit
* Automatic testing with Git Bisect
* Real-world use cases
* Best practices
* Common mistakes

---

# 🤔 Why Do We Need Git Bisect?

Imagine the following situation:

* Your application was working correctly on Monday.
* During the week, your team pushed **200 commits**.
* On Friday, users report that the application crashes.

Now you need to answer one important question:

> **Which commit introduced the bug?**

Checking every commit manually is inefficient.

```
Commit 1 ✅
Commit 2 ✅
Commit 3 ✅
...
Commit 198 ❌
Commit 199 ❌
Commit 200 ❌
```

This process could take hours.

Git Bisect solves this problem using **Binary Search**, reducing the number of tests dramatically.

For example:

| Total Commits |    Manual Search |     Git Bisect |
| ------------: | ---------------: | -------------: |
|           100 |  Up to 100 tests |  About 7 tests |
|           500 |  Up to 500 tests |  About 9 tests |
|          1000 | Up to 1000 tests | About 10 tests |

This makes Git Bisect one of the most efficient debugging features available in Git.

---

# 🔍 What is Git Bisect?

Git Bisect is a Git command used to find the first commit that introduced a bug.

It works by:

1. Starting a bisect session.
2. Marking the current (broken) commit as **bad**.
3. Marking a previously working commit as **good**.
4. Automatically checking out the middle commit.
5. Asking you whether that commit is **good** or **bad**.
6. Repeating the process until the first bad commit is identified.

Because Git uses Binary Search, the search becomes significantly faster than checking commits one by one.

---

# 🧠 Understanding Binary Search

Binary Search repeatedly divides a search space into two halves until the target is found.

Suppose your commit history looks like this:

```text
A ── B ── C ── D ── E ── F ── G ── H ── I
```

* Commit **A** is known to be good.
* Commit **I** is known to be bad.

Instead of testing every commit, Git first checks the middle commit.

```text
A ── B ── C ── D ── E ── F ── G ── H ── I
                  ▲
             Test this first
```

If **E** is good, Git searches only the right half.

```text
F ── G ── H ── I
```

If **E** is bad, Git searches only the left half.

This continues until Git identifies the exact commit that introduced the issue.

---

# 📊 Git Bisect Workflow

The following diagram illustrates how Git Bisect narrows down the search using Binary Search.

![Git Bisect Workflow](assets/git-bisect-workflow.png)

### Workflow

```text
Bug Detected
      │
      ▼
git bisect start
      │
      ▼
Mark Current Commit as Bad
      │
      ▼
Mark Known Good Commit
      │
      ▼
Git Checks Middle Commit
      │
      ▼
Test the Application
      │
 ┌────┴────┐
 │         │
Good      Bad
 │         │
 ▼         ▼
Continue Binary Search
      │
      ▼
First Bad Commit Found
      │
      ▼
git bisect reset
```

---

# ⚙️ How Git Bisect Works

Git Bisect follows a simple but effective process:

### Step 1 – Start the bisect session

```bash
git bisect start
```

Git enters bisect mode and prepares to search through the commit history.

---

### Step 2 – Mark the current commit as bad

```bash
git bisect bad
```

This tells Git that the current commit contains the bug.

---

### Step 3 – Mark a previously working commit as good

```bash
git bisect good <commit-hash>
```

Example:

```bash
git bisect good a4f9c3d
```

Git now has both ends of the search range and begins the Binary Search process automatically.

---

### Step 4 – Test the checked-out commit

Git checks out a commit roughly halfway between the good and bad commits.

Run your application or tests.

If the bug exists:

```bash
git bisect bad
```

If the bug does not exist:

```bash
git bisect good
```

Git continues narrowing the search until only one commit remains.

---

# 💡 Key Advantages

* Faster than manual debugging.
* Uses an efficient Binary Search algorithm.
* Saves significant debugging time.
* Ideal for large repositories.
* Can be automated with test scripts.
* Frequently used in open-source and enterprise projects.

---

# 🛠️ Git Bisect Commands

Git Bisect provides a set of commands to help identify the commit that introduced a bug.

| Command                    | Description                                   |
| -------------------------- | --------------------------------------------- |
| `git bisect start`         | Start a bisect session                        |
| `git bisect bad`           | Mark the current commit as bad                |
| `git bisect good <commit>` | Mark a known good commit                      |
| `git bisect good`          | Mark the currently checked-out commit as good |
| `git bisect log`           | Display the bisect log                        |
| `git bisect visualize`     | Open the commits in Git Log                   |
| `git bisect reset`         | Exit bisect mode                              |
| `git bisect run <script>`  | Automate testing using a script               |

---

# 📊 Git Bisect Commands Workflow

The following diagram illustrates the commands executed during a typical Git Bisect session.

![Git Bisect Commands](assets/git-bisect-commands.png)

---

# 🚀 Step-by-Step Hands-on Example

Suppose your commit history looks like this:

```text
A ── B ── C ── D ── E ── F ── G ── H ── I
```

* Commit **A** works correctly.
* Commit **I** contains a bug.

Our goal is to identify the first bad commit.

---

## Step 1 – Start Git Bisect

```bash
git bisect start
```

Output:

```text
status: waiting for both good and bad commits
```

---

## Step 2 – Mark the Current Commit as Bad

Since the latest commit contains the bug:

```bash
git bisect bad
```

Git records the latest commit as the bad commit.

---

## Step 3 – Mark a Known Good Commit

Suppose Commit A is known to work correctly.

```bash
git bisect good a1b2c3d
```

Git now begins its Binary Search.

---

## Step 4 – Git Automatically Checks Out the Middle Commit

Git might display:

```text
Bisecting: 4 revisions left to test after this
```

Git checks out Commit **E**.

Test your application.

---

### If the bug exists

```bash
git bisect bad
```

Git continues searching between:

```text
E  →  I
```

---

### If the bug does not exist

```bash
git bisect good
```

Git continues searching between:

```text
A  →  E
```

---

## Step 5 – Continue Testing

Git keeps selecting the middle commit.

Example:

```
Test F
↓

Test G
↓

Test H
```

Each time you simply answer:

```bash
git bisect good
```

or

```bash
git bisect bad
```

Git automatically narrows the search.

---

## Step 6 – Git Finds the First Bad Commit

Eventually Git reports:

```text
4d5f8a1 is the first bad commit
```

Git also displays:

* Commit ID
* Author
* Commit Message
* Changed files

Now you know exactly which commit introduced the bug.

---

## Step 7 – Exit Bisect Mode

Always reset Git after completing the search.

```bash
git bisect reset
```

Git returns to your original branch.

---

# 🤖 Automatic Git Bisect

Testing manually is practical for small projects.

For large repositories, Git can automate the process.

Example script:

```bash
#!/bin/bash

mvn test
```

Save as:

```text
test.sh
```

Make it executable.

```bash
chmod +x test.sh
```

Run Git Bisect automatically.

```bash
git bisect run ./test.sh
```

Git executes the script for every checked-out commit.

If the script returns:

```
0
```

Git marks the commit as **Good**.

If the script returns:

```
1
```

Git marks the commit as **Bad**.

Git continues until it finds the first faulty commit.

---

# 📊 Binary Search Visualization

The following diagram explains how Git repeatedly halves the search range.

![Git Bisect Binary Search](assets/git-bisect-binary-search.png)

Example:

```text
Good                           Bad

A──B──C──D──E──F──G──H──I──J

First Test
      │
      ▼
      E

Second Test
          │
          ▼
          H

Third Test
       │
       ▼
       G

Fourth Test
         │
         ▼
         F

First Bad Commit Found
```

Instead of testing every commit, Git intelligently reduces the search space using Binary Search.

---

# 💻 Real Terminal Example

```bash
git bisect start

git bisect bad

git bisect good a1b2c3d
```

Git responds:

```text
Bisecting: 6 revisions left to test after this
```

Test the application.

If it fails:

```bash
git bisect bad
```

Git checks another commit.

Continue until Git reports:

```text
First bad commit:

5e8b2d1
```

Reset Git.

```bash
git bisect reset
```

---

# 🌍 Real-World Use Cases

## Production Support

A production application crashes after a recent deployment.

Instead of reviewing hundreds of commits manually, use Git Bisect to quickly identify the faulty commit.

---

## DevOps CI/CD

A deployment pipeline suddenly starts failing.

Git Bisect can identify the commit that introduced the issue.

---

## Open Source Projects

Large projects such as the Linux kernel frequently use Git Bisect to isolate regressions across thousands of commits.

---

## Debugging Performance Issues

When application performance gradually degrades, Git Bisect can help identify the exact change responsible.

---

# ✅ Best Practices

Following these best practices will help you use Git Bisect effectively and avoid common debugging mistakes.

## 1. Choose a Reliable Good Commit

Always select a commit that is known to work correctly.

```bash
git bisect good a1b2c3d
```

Choosing the wrong "good" commit may lead to incorrect results.

---

## 2. Verify Each Commit Carefully

Whenever Git checks out a commit:

* Build the project.
* Run all required tests.
* Verify the bug completely.

Avoid making assumptions.

---

## 3. Use Automated Tests Whenever Possible

For large projects, manual testing becomes slow.

Instead, create a test script.

Example:

```bash
#!/bin/bash

./run-tests.sh
```

Run it automatically:

```bash
git bisect run ./run-tests.sh
```

Automation reduces human error and speeds up debugging.

---

## 4. Always Reset After Finishing

After Git identifies the faulty commit:

```bash
git bisect reset
```

This restores your repository to its original branch.

---

## 5. Keep Your Working Directory Clean

Before starting Git Bisect:

```bash
git status
```

Output should be:

```text
nothing to commit, working tree clean
```

Avoid debugging with uncommitted changes.

---

# 💡 Tips & Tricks

### View Bisect History

```bash
git bisect log
```

Displays all decisions made during the bisect session.

---

### Visualize Commits

```bash
git bisect visualize
```

Opens Git Log (or Git GUI) showing the remaining commits.

---

### Skip Untestable Commits

Sometimes a commit cannot be built or tested.

Skip it instead of marking it good or bad.

```bash
git bisect skip
```

Git automatically selects another commit.

---

### Save the Bisect Log

```bash
git bisect log > bisect-log.txt
```

Useful for documentation or sharing with teammates.

---

# ❌ Common Mistakes

## Forgetting to Reset

Many beginners finish debugging but forget:

```bash
git bisect reset
```

Git remains in bisect mode until reset.

---

## Choosing the Wrong Good Commit

Incorrect:

```bash
git bisect good
```

when the selected commit actually contains the bug.

Always verify your known good commit before starting.

---

## Testing Incorrectly

If you don't fully test the application, Git receives incorrect information and may identify the wrong commit.

Always run the complete test suite.

---

## Starting with Uncommitted Changes

Never begin bisecting while your working directory contains changes.

Check first:

```bash
git status
```

If necessary:

```bash
git stash
```

---

## Ignoring Build Errors

Some commits may fail to build.

Instead of marking them bad:

```bash
git bisect skip
```

---

# 🌍 Real-World Scenario

Imagine you're working on an e-commerce application.

```
Monday    Everything Works
Tuesday   New Feature Added
Wednesday Payment Changes
Thursday  UI Improvements
Friday    Customers Cannot Place Orders
```

During the week, the repository received **350 commits**.

Without Git Bisect:

* Review hundreds of commits manually.
* Spend hours identifying the problem.

With Git Bisect:

```
Known Good Commit
        │
        ▼
Binary Search
        │
        ▼
~9 Tests
        │
        ▼
First Bad Commit Found
```

A process that could take hours is reduced to just a few minutes.

---

# 📊 Git Bisect Best Practice Workflow

The following diagram summarizes the recommended Git Bisect workflow.

![Git Bisect Best Practices](assets/git-bisect-best-practices.png)

Example Flow:

```text
Clean Working Directory
        │
        ▼
Start Bisect
        │
        ▼
Mark Good Commit
        │
        ▼
Mark Bad Commit
        │
        ▼
Test Each Commit Carefully
        │
        ▼
Use git bisect skip (if needed)
        │
        ▼
First Bad Commit Found
        │
        ▼
git bisect reset
```

---

# 📌 Command Summary

| Command                    | Description                 |
| -------------------------- | ---------------------------- |
| `git bisect start`         | Start a bisect session      |
| `git bisect bad`           | Mark current commit as bad  |
| `git bisect good <commit>` | Mark a known good commit    |
| `git bisect good`          | Mark current commit as good |
| `git bisect skip`          | Skip an untestable commit   |
| `git bisect log`           | Show bisect history         |
| `git bisect visualize`     | View remaining commits      |
| `git bisect run <script>`  | Automate testing            |
| `git bisect reset`         | Exit bisect mode            |

---

# 🎤 Interview Questions

## 1. What is Git Bisect?

Git Bisect is a debugging tool that uses the Binary Search algorithm to identify the first commit that introduced a bug.

---

## 2. Why is Git Bisect faster than manual debugging?

Because it repeatedly halves the search range using Binary Search, reducing the number of commits that need to be tested.

---

## 3. Which algorithm does Git Bisect use?

**Binary Search**

---

## 4. What is the purpose of `git bisect reset`?

It ends the bisect session and restores your repository to its original branch.

```bash
git bisect reset
```

---

## 5. How can Git Bisect be automated?

By using:

```bash
git bisect run <script>
```

Git executes the script for each checked-out commit and determines whether it is good or bad based on the script's exit status.

---

## 6. What should you do if a commit cannot be tested?

Use:

```bash
git bisect skip
```

Git skips the commit and continues the search.

---

## 7. Can Git Bisect work with automated CI/CD tests?

Yes. It integrates well with automated test scripts, making it highly effective for continuous integration and large projects.

---

# 📝 Summary

Git Bisect is one of Git's most powerful debugging tools. By using the Binary Search algorithm, it efficiently locates the commit that introduced a bug, saving significant time compared to manual investigation.

Key takeaways:

* Identify bugs quickly using Binary Search.
* Reduce debugging time dramatically.
* Automate testing with `git bisect run`.
* Skip untestable commits with `git bisect skip`.
* Always finish with `git bisect reset`.
* Ideal for large repositories and enterprise software projects.

Mastering Git Bisect is an essential skill for developers, DevOps engineers, and production support professionals because it enables faster root-cause analysis and more efficient troubleshooting.

---

# 🎯 What's Next?

➡️ **04-Hooks.md**

In the next chapter, you'll learn:

* What Git Hooks are
* Client-side vs Server-side Hooks
* Common Hook Types
* Creating Custom Hooks
* Automating Code Quality Checks
* Real-world DevOps Use Cases
* Best Practices
* Interview Questions
