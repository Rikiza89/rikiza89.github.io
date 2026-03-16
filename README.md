# GIT_DOC

# The Complete Git & GitHub Guide
### From Zero to Professional Developer

---

## Table of Contents

1. [Quick Start (Your First 5 Minutes with Git)](#quick-start-your-first-5-minutes-with-git)
2. [Introduction](#introduction)
3. [Installing & Setting Up Git](#installing--setting-up-git)
4. [Git Fundamentals](#git-fundamentals)
5. [Creating & Managing Repositories](#creating--managing-repositories)
6. [Basic Git Commands](#basic-git-commands)
7. [Understanding Commits](#understanding-commits)
8. [Branching](#branching)
9. [Merging & Rebasing](#merging--rebasing)
10. [Merge Conflicts](#merge-conflicts)
11. [Undoing Changes](#undoing-changes)
12. [Working With Remote Repositories](#working-with-remote-repositories)
13. [GitHub Essentials](#github-essentials)
14. [Pull Requests](#pull-requests)
15. [.gitignore](#gitignore)
16. [Tags & Releases](#tags--releases)
17. [Stashing](#stashing)
18. [Collaboration Workflows](#collaboration-workflows)
19. [Real-World Workflows: Easy, Intermediate & Expert](#real-world-workflows-easy-intermediate--expert)
20. [Best Practices & Daily Workflow](#best-practices--daily-workflow)
21. [Common Mistakes & How to Fix Them](#common-mistakes--how-to-fix-them)
22. [Git Cheat Sheet](#git-cheat-sheet)
23. [Learning & Growth](#learning--growth)

---

## Quick Start (Your First 5 Minutes with Git)

> **New to Git?** Start here. You can read the rest of this guide later. These are the only commands you need to get going.

### Step 1: Install Git

```bash
# macOS
brew install git

# Ubuntu/Debian
sudo apt install git

# Windows: Download from https://git-scm.com
```

### Step 2: Tell Git who you are

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 3: Create your first project

```bash
mkdir my-first-project
cd my-first-project
git init
```

### Step 4: Save your work (you'll do this every day)

```bash
# Create a file
echo "Hello, World!" > hello.txt

# Tell Git to track it
git add hello.txt

# Save a snapshot (a "commit")
git commit -m "Add my first file"
```

### Step 5: Put it on GitHub

1. Go to [github.com](https://github.com) and create a new repository
2. Then run:

```bash
git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git
git push -u origin main
```

**That's it!** You just used Git and GitHub. Now read on to understand what each step does and learn more powerful features.

> **Think of it this way:**
> - `git add` = Put items in your shopping cart
> - `git commit` = Buy them (save permanently)
> - `git push` = Ship them to the warehouse (upload to GitHub)

---

## Introduction

### What is Git?

Git is a **distributed version control system** created by Linus Torvalds in 2005. Think of it as a time machine for your code. It tracks every change you make to your files, who made the change, and when it happened.

**Why does this matter?**

- You can experiment freely without fear of breaking things
- You can return to any previous version of your code
- Multiple people can work on the same project simultaneously
- You have a complete history of your project's evolution

Git runs **locally on your computer**. You don't need internet to use Git itself.

### What is GitHub?

GitHub is a **cloud platform** that hosts Git repositories online. It's like Google Drive or Dropbox, but specifically designed for code and Git repositories.

**GitHub provides:**

- Cloud storage for your Git repositories
- Collaboration tools (pull requests, code reviews)
- Project management features (issues, projects)
- A portfolio to showcase your work
- Social coding (following developers, starring projects)

**Important:** GitHub is just one of many platforms. Others include GitLab, Bitbucket, and Gitea.

### Git vs GitHub: Clear Comparison

| Aspect | Git | GitHub |
|--------|-----|--------|
| **What it is** | Version control software | Cloud hosting platform |
| **Runs on** | Your local computer | The internet (cloud) |
| **Created by** | Linus Torvalds (2005) | Microsoft (acquired 2018) |
| **Purpose** | Track file changes, manage versions | Host repositories, enable collaboration |
| **Requires internet?** | No | Yes |
| **Cost** | Free and open-source | Free for public repos, paid for private features |
| **Alternatives** | Mercurial, SVN | GitLab, Bitbucket, Gitea |

**Analogy:** Git is like Microsoft Word (the software), and GitHub is like OneDrive (the cloud storage).

### Why Version Control Matters

Imagine you're writing a research paper:

**Without version control:**
```
final_paper.docx
final_paper_v2.docx
final_paper_v2_ACTUAL.docx
final_paper_v2_ACTUAL_reviewed.docx
final_paper_USE_THIS_ONE.docx
```

**With version control:**
```
paper.docx (with complete history of every change)
```

Version control gives you:

1. **History:** See what changed, when, and why
2. **Collaboration:** Multiple people can work simultaneously
3. **Branching:** Try new ideas without affecting the main work
4. **Safety:** Never lose work, always recoverable
5. **Professionalism:** Industry standard for software development

---

## Installing & Setting Up Git

### Install Git

#### Windows

1. Download from [git-scm.com](https://git-scm.com/download/win)
2. Run the installer
3. Use default settings (recommended for beginners)
4. Open **Git Bash** (installed with Git)

#### macOS

**Option 1: Homebrew (recommended)**
```bash
brew install git
```

**Option 2: Xcode Command Line Tools**
```bash
xcode-select --install
```

**Option 3: Download installer from git-scm.com**

#### Linux

**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install git
```

**Fedora:**
```bash
sudo dnf install git
```

**Arch:**
```bash
sudo pacman -S git
```

### Verify Installation

After installing, verify Git is working:

```bash
git --version
```

You should see output like:
```
git version 2.40.0
```

### Configure Username and Email

**Critical step:** Git needs to know who you are. Every commit you make will include this information.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Why this matters:**
- Your name and email appear in every commit
- GitHub uses this email to link commits to your account
- Teams need to know who made which changes

**Check your configuration:**
```bash
git config --global --list
```

### Basic Git Configuration

**Set your default text editor:**

```bash
# Use VS Code
git config --global core.editor "code --wait"

# Use Nano (simple terminal editor)
git config --global core.editor "nano"

# Use Vim
git config --global core.editor "vim"
```

**Set default branch name to `main`:**

```bash
git config --global init.defaultBranch main
```

**Enable colored output:**

```bash
git config --global color.ui auto
```

**View all configuration:**

```bash
git config --list
```

---

## Git Fundamentals

Before diving into commands, you need to understand how Git thinks about your files.

### Repository (Repo)

A **repository** is a project tracked by Git. It's a folder that contains:
- Your project files
- A hidden `.git` folder (Git's internal database)

The `.git` folder contains the entire history of your project. **Never delete it** unless you want to remove Git tracking entirely.

### The Three States of Git

Git has three main states where your files can reside:

#### 1. Working Directory

This is your actual project folder where you edit files. Changes here are **not tracked** until you tell Git about them.

#### 2. Staging Area (Index)

This is a "preparation zone" where you gather changes before committing. Think of it as a shopping cart before checkout.

**Why does this exist?**
- You can commit only specific changes, not everything
- You can review what you're about to commit
- You can build logical, atomic commits

#### 3. Repository (Committed)

Once committed, changes are permanently saved in Git's history.

### Git Workflow Diagram

```
Working Directory  →  Staging Area  →  Repository
     (edit)         (git add)       (git commit)
    
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   file.txt  │    │   file.txt  │    │   file.txt  │
│  (modified) │───→│   (staged)  │───→│ (committed) │
└─────────────┘    └─────────────┘    └─────────────┘
```

**Example workflow:**

1. You edit `app.py` (working directory)
2. You run `git add app.py` (staging area)
3. You run `git commit -m "Add login feature"` (repository)

### HEAD

`HEAD` is a pointer to your current location in the repository. Usually, it points to the latest commit on your current branch.

Think of it as "you are here" on a map.

### Commit

A **commit** is a snapshot of your project at a specific point in time. Each commit includes:

- The changes made
- Who made them
- When they were made
- A message describing the changes
- A unique identifier (hash)

**Example commit:**
```
commit a1b2c3d4e5f6g7h8i9j0
Author: Jane Doe <jane@example.com>
Date:   Mon Jan 27 14:32:10 2025 -0500

    Add user authentication feature
```

---

## Creating & Managing Repositories

### Creating a New Repository: `git init`

To start tracking a project with Git:

```bash
# Navigate to your project folder
cd my-project

# Initialize Git
git init
```

**What happens:**
- Git creates a hidden `.git` folder
- Your folder is now a Git repository
- No files are tracked yet (you need to add and commit them)

**Example:**

```bash
mkdir my-app
cd my-app
git init
# Output: Initialized empty Git repository in /path/to/my-app/.git/
```

### Cloning an Existing Repository

To download a repository from GitHub (or elsewhere):

```bash
git clone <repository-url>
```

**Example:**

```bash
git clone https://github.com/username/project-name.git
```

**What happens:**
- Git downloads the entire repository
- Creates a folder with the project name
- Sets up connection to the original repository (called "origin")
- Checks out the default branch

**Clone a specific branch:**

```bash
git clone -b branch-name https://github.com/username/project.git
```

### Repository Structure

After `git init` or `git clone`, your folder looks like:

```
my-project/
├── .git/              # Git's internal database (NEVER EDIT MANUALLY)
│   ├── objects/       # All commits, files, and history
│   ├── refs/          # Branches and tags
│   ├── HEAD           # Points to current branch
│   └── config         # Repository configuration
├── .gitignore         # Files to ignore (you create this)
├── README.md          # Project documentation (you create this)
└── (your project files)
```

**Important:** The `.git` folder is hidden. To see it:

```bash
# Linux/macOS
ls -la

# Windows (Git Bash)
ls -la

# Windows (PowerShell)
Get-ChildItem -Force
```

---

## Basic Git Commands

These are the commands you'll use every single day.

### `git status`

Shows the current state of your repository.

```bash
git status
```

**Example output:**

```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   app.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

**What this tells you:**
- Current branch: `main`
- Modified files not yet staged: `app.py`
- New files not tracked: `new_file.txt`

**Best practice:** Run `git status` constantly. It's your compass.

### `git add`

Adds files to the staging area.

```bash
# Add a specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.py file3.css

# Add all files in current directory
git add .

# Add all files in the repository
git add -A
```

**Example:**

```bash
# You edited app.py
git status
# Shows: modified: app.py

git add app.py
git status
# Shows: Changes to be committed: modified: app.py
```

**Interactive staging (advanced):**

```bash
# Choose which changes to stage interactively
git add -p
```

**Warning:** Be careful with `git add .` — make sure you're not adding unwanted files.

### `git commit`

Saves staged changes to the repository.

```bash
# Commit with a message
git commit -m "Your commit message"

# Commit and open editor for longer message
git commit

# Add all tracked files and commit (skip staging)
git commit -a -m "Your message"
```

**Example:**

```bash
git add app.py
git commit -m "Add login validation"
```

**Output:**
```
[main a1b2c3d] Add login validation
 1 file changed, 15 insertions(+), 3 deletions(-)
```

**Multi-line commit messages:**

```bash
git commit -m "Add user authentication" -m "This includes login, logout, and session management."
```

### `git log`

Shows commit history.

```bash
# Full log
git log

# Compact one-line format
git log --oneline

# Show last 5 commits
git log -5

# Show commits with file changes
git log --stat

# Show commits with actual changes
git log -p
```

**Example output (`git log --oneline`):**

```
a1b2c3d Add login validation
e4f5g6h Fix navbar styling
i7j8k9l Initial commit
```

**Useful log variations:**

```bash
# Pretty format with graph
git log --oneline --graph --all

# Show commits by specific author
git log --author="Jane Doe"

# Show commits in date range
git log --since="2 weeks ago"

# Search commits by message
git log --grep="login"
```

### `git diff`

Shows changes between different states.

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare two commits
git diff commit1 commit2

# Compare branches
git diff main feature-branch
```

**Example:**

```bash
# You edited app.py
git diff
```

**Output:**
```diff
diff --git a/app.py b/app.py
index a1b2c3d..e4f5g6h 100644
--- a/app.py
+++ b/app.py
@@ -10,7 +10,7 @@ def login(username, password):
-    if username == "admin":
+    if username == "admin" and password:
         return True
```

**Reading diff output:**
- `-` shows removed lines (red)
- `+` shows added lines (green)

### `git show`

Shows details of a specific commit.

```bash
# Show the last commit
git show

# Show a specific commit
git show a1b2c3d

# Show a specific file in a commit
git show a1b2c3d:app.py
```

---

## Understanding Commits

Commits are the heart of Git. Understanding what makes a good commit is crucial for professional development.

### What Makes a Good Commit

**Good commits are:**

1. **Atomic:** One logical change per commit
2. **Complete:** The code works after the commit
3. **Descriptive:** Clear message explaining what and why
4. **Focused:** Don't mix unrelated changes

**Bad commit example:**

```bash
git commit -m "Fixed stuff"
```

Problems:
- What was fixed?
- Why was it fixed?
- Impossible to understand later

**Good commit example:**

```bash
git commit -m "Fix null pointer exception in user login

The login function didn't check for null email addresses,
causing crashes when users left the field empty.
Added validation to prevent this."
```

### Writing Good Commit Messages

**The anatomy of a great commit message:**

```
<type>: <subject line (50 chars or less)>

<body: explain what and why, not how (72 chars per line)>

<footer: references to issues, breaking changes>
```

**Subject line best practices:**

✅ **Good:**
- `Add email validation to signup form`
- `Fix memory leak in image processing`
- `Update README with installation instructions`

❌ **Bad:**
- `fixed bug`
- `updates`
- `changes`
- `asdfasdf`

**Commit message types (conventional commits):**

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Formatting, missing semicolons, etc.
- `refactor:` Code restructuring without behavior change
- `test:` Adding or updating tests
- `chore:` Maintenance tasks

**Examples:**

```bash
git commit -m "feat: Add password reset functionality"

git commit -m "fix: Correct calculation in tax module"

git commit -m "docs: Update API documentation for auth endpoint"

git commit -m "refactor: Extract validation logic into separate module"
```

**Multi-line message (opens editor):**

```bash
git commit
```

Then write:
```
feat: Add user profile photo upload

Users can now upload profile photos up to 5MB. Photos are
automatically resized to 500x500px and stored in S3. This
implements the feature requested in issue #42.

- Added image validation
- Integrated with AWS S3
- Updated user model with photo URL field

Closes #42
```

### Atomic Commits

**Atomic commits** mean each commit contains one logical change.

**Bad (non-atomic):**

```bash
# One commit with multiple unrelated changes
git add .
git commit -m "Add login feature, fix navbar, update docs, refactor database"
```

**Good (atomic):**

```bash
# Four separate commits, each with one purpose
git add login.py
git commit -m "feat: Add user login functionality"

git add navbar.css
git commit -m "fix: Correct navbar alignment on mobile"

git add README.md
git commit -m "docs: Add setup instructions"

git add database.py
git commit -m "refactor: Optimize database query performance"
```

**Why atomic commits matter:**

1. **Easier to understand:** Each commit has one clear purpose
2. **Easier to revert:** Can undo one change without affecting others
3. **Easier to review:** Code reviewers can follow your logic
4. **Better history:** Git log tells a clear story

**How to create atomic commits:**

```bash
# Stage only specific files
git add feature.py
git commit -m "Add new feature"

git add test_feature.py
git commit -m "Add tests for new feature"

# Or use interactive staging
git add -p  # Choose which changes to stage
```

---

## Branching

Branching is one of Git's most powerful features. Master this, and you'll understand why Git is the industry standard.

### What is a Branch?

A **branch** is an independent line of development. Think of it as a parallel universe for your code.

**Analogy:** Imagine writing a book:
- `main` branch: The published version
- `chapter-5-rewrite` branch: Experimenting with a new plot twist
- `fix-typos` branch: Correcting errors

You can work on each branch independently, then merge the good changes back into `main`.

### Why Branches Are Used

**In professional development, branches let you:**

1. **Experiment safely:** Try new features without breaking the main code
2. **Work in parallel:** Multiple developers work on different features simultaneously
3. **Organize work:** Each feature/bug fix gets its own branch
4. **Code review:** Branches enable pull requests and code reviews
5. **Stability:** Keep `main` branch stable and deployable at all times

**Real-world example:**

```
main branch (production-ready code)
├── feature/user-authentication (new login system)
├── feature/payment-integration (new payment feature)
├── bugfix/navbar-mobile (fix mobile navigation)
└── hotfix/security-patch (urgent security fix)
```

### `git branch`

List, create, rename, and delete branches.

```bash
# List all local branches
git branch

# List all branches (including remote)
git branch -a

# Create a new branch
git branch feature-login

# Create and switch to a new branch
git checkout -b feature-login
# or (newer syntax)
git switch -c feature-login

# Rename current branch
git branch -m new-branch-name

# Rename a specific branch
git branch -m old-name new-name

# Delete a branch (safe - prevents deleting unmerged work)
git branch -d branch-name

# Force delete a branch (dangerous)
git branch -D branch-name

# Show branches with last commit
git branch -v
```

### `git checkout` vs `git switch`

**Old way (still works):**

```bash
git checkout branch-name      # Switch branches
git checkout -b new-branch    # Create and switch
```

**New way (clearer):**

```bash
git switch branch-name        # Switch branches
git switch -c new-branch      # Create and switch
```

**Why `git switch` exists:**
- `git checkout` does too many things (confusing for beginners)
- `git switch` is specifically for switching branches
- `git restore` is now used for restoring files

**I recommend using `git switch`** for clarity, but you'll see `git checkout` in older tutorials.

### Creating, Listing, Renaming, Deleting Branches

**Complete example workflow:**

```bash
# See current branches
git branch
# Output:
# * main

# Create a new branch
git branch feature-login

# List branches again
git branch
# Output:
# * main
#   feature-login

# Switch to the new branch
git switch feature-login
# Output: Switched to branch 'feature-login'

# Verify current branch
git branch
# Output:
#   main
# * feature-login

# Do some work...
git add login.py
git commit -m "feat: Add login form"

# Switch back to main
git switch main

# Merge the feature (we'll cover this next section)
git merge feature-login

# Delete the feature branch (after merging)
git branch -d feature-login
```

**Renaming a branch:**

```bash
# Rename current branch
git branch -m better-name

# Rename a different branch
git branch -m old-name new-name
```

**Deleting branches:**

```bash
# Safe delete (only if merged)
git branch -d feature-login
# Output: Deleted branch feature-login (was a1b2c3d).

# Force delete (even if not merged)
git branch -D experimental-feature
# Warning: This DELETES UNMERGED WORK permanently
```

### Feature Branch Workflow

This is the most common professional workflow.

**The pattern:**

1. Create a branch for each feature/bug fix
2. Work on that branch
3. Merge back to `main` when done
4. Delete the feature branch

**Example:**

```bash
# Starting from main
git switch main
git pull  # Get latest changes

# Create feature branch
git switch -c feature/add-dark-mode

# Do your work
git add styles.css
git commit -m "feat: Add dark mode toggle"

git add app.js
git commit -m "feat: Implement dark mode state management"

# Switch back to main
git switch main

# Merge feature
git merge feature/add-dark-mode

# Delete feature branch
git branch -d feature/add-dark-mode

# Push to remote
git push
```

**Branch naming conventions:**

```bash
feature/user-authentication
feature/payment-integration
bugfix/navbar-alignment
bugfix/login-validation
hotfix/security-vulnerability
docs/api-documentation
refactor/database-optimization
```

**Benefits of this workflow:**

- `main` is always stable
- Features are isolated
- Easy to abandon failed experiments
- Clear separation of concerns
- Enables code review (pull requests)

---

## Merging & Rebasing

After working on a branch, you need to integrate changes back into `main`. There are two main ways: merging and rebasing.

### What is Merging?

**Merging** combines two branches by creating a new commit that joins their histories.

**Visual:**

```
Before merge:
      A---B---C  main
           \
            D---E  feature

After merge:
      A---B---C---F  main
           \     /
            D---E  feature
            
F is the "merge commit"
```

### Fast-Forward vs Non-Fast-Forward Merges

#### Fast-Forward Merge

Happens when the target branch hasn't changed since the feature branch was created.

```bash
# main hasn't changed
git switch main
git merge feature-login
```

**Visual:**

```
Before:
      A---B  main
           \
            C---D  feature-login

After (fast-forward):
      A---B---C---D  main, feature-login
```

No merge commit is created; `main` simply moves forward.

#### Non-Fast-Forward Merge

Happens when both branches have new commits.

```bash
git switch main
git merge feature-login
```

**Visual:**

```
Before:
      A---B---C  main
           \
            D---E  feature-login

After (merge commit):
      A---B---C---F  main
           \     /
            D---E  feature-login
```

A merge commit `F` is created to join the histories.

### `git merge`

```bash
# Merge a branch into current branch
git merge branch-name

# Merge and create a merge commit (even if fast-forward possible)
git merge --no-ff branch-name

# Abort a merge in progress
git merge --abort
```

**Example:**

```bash
# You're on main, want to merge feature-login
git switch main
git merge feature-login

# If successful:
# Output: Updating a1b2c3d..e4f5g6h
#         Fast-forward
#          login.py | 45 ++++++++++++++++++++++
#          1 file changed, 45 insertions(+)

# If there's a merge commit:
# Output: Merge made by the 'recursive' strategy.
#          login.py | 45 ++++++++++++++++++++++
#          1 file changed, 45 insertions(+)
```

### Introduction to `git rebase`

**Rebasing** rewrites history by moving commits to a new base.

```bash
git rebase main
```

**Visual:**

```
Before rebase:
      A---B---C  main
           \
            D---E  feature

After rebase:
      A---B---C  main
               \
                D'---E'  feature
```

Notice `D` and `E` become `D'` and `E'` — they're new commits with the same changes.

**Basic rebase workflow:**

```bash
# You're on feature branch
git switch feature-login

# Rebase onto main
git rebase main

# If conflicts occur, fix them, then:
git add .
git rebase --continue

# Or abort the rebase:
git rebase --abort
```

### When to Merge vs Rebase (Best Practices)

**Use `git merge` when:**

✅ You want to preserve complete history
✅ Working on a public/shared branch
✅ You're merging into `main` from a feature branch
✅ You want to see when branches were integrated

**Use `git rebase` when:**

✅ You want a clean, linear history
✅ Working on a private feature branch
✅ Updating your feature branch with latest `main`
✅ Cleaning up commits before merging

**Golden Rule of Rebasing:**

> **NEVER rebase commits that have been pushed to a shared/public branch.**

Why? Rebasing rewrites history. If others have based work on your commits, rebasing breaks their work.

**Safe rebase example:**

```bash
# You're working on a feature branch alone
git switch feature-login

# Update with latest main changes
git fetch origin
git rebase origin/main

# Continue working
```

**Professional workflow:**

```bash
# 1. Create feature branch
git switch -c feature/new-feature

# 2. Work and commit
git add .
git commit -m "feat: Add feature"

# 3. Before finishing, update with latest main
git fetch origin
git rebase origin/main  # Get latest changes cleanly

# 4. Fix any conflicts, then push
git push

# 5. Create pull request
# 6. Merge via pull request (which creates a merge commit)
```

**Summary:**

| Scenario | Use |
|----------|-----|
| Integrating feature → main | **Merge** |
| Updating feature branch with latest main | **Rebase** |
| Public/shared branches | **Merge** |
| Private feature branches | **Rebase** |
| Want to preserve history | **Merge** |
| Want clean linear history | **Rebase** |

---

## Merge Conflicts

Merge conflicts happen when Git can't automatically combine changes. This is normal and fixable.

### What Causes Merge Conflicts

Conflicts occur when:

1. Two branches modify the **same lines** in the same file
2. One branch deletes a file while another modifies it
3. Both branches add a file with the same name

**Example scenario:**

```
main branch changes line 5:  username = "admin"
feature branch changes line 5:  username = "user"

When merging → Git doesn't know which to keep → CONFLICT
```

### How to Read Conflict Markers

When a conflict occurs, Git adds markers to the file:

```python
def login(username):
<<<<<<< HEAD
    if username == "admin":
        return True
=======
    if username == "user" and is_authenticated:
        return True
>>>>>>> feature-login
    return False
```

**What the markers mean:**

- `<<<<<<< HEAD` — Start of your current branch's version
- `=======` — Separator between versions
- `>>>>>>> feature-login` — End of the incoming branch's version

**Everything between `<<<<<<<` and `=======` is YOUR version.**
**Everything between `=======` and `>>>>>>>` is THEIR version.**

### Step-by-Step Conflict Resolution

**1. Attempt the merge:**

```bash
git merge feature-login
# Output: Auto-merging app.py
#         CONFLICT (content): Merge conflict in app.py
#         Automatic merge failed; fix conflicts and then commit the result.
```

**2. See which files have conflicts:**

```bash
git status
# Output: Unmerged paths:
#           both modified:   app.py
```

**3. Open the conflicted file:**

```bash
code app.py  # Or your preferred editor
```

**4. Find the conflict markers:**

```python
def login(username):
<<<<<<< HEAD
    if username == "admin":
        return True
=======
    if username == "user" and is_authenticated:
        return True
>>>>>>> feature-login
    return False
```

**5. Decide what to keep:**

Option A: Keep HEAD version (current branch)
Option B: Keep incoming version (feature branch)
Option C: Keep both (merge the logic)
Option D: Write something completely new

**6. Edit the file to resolve:**

```python
def login(username):
    # Combined logic from both branches
    if username in ["admin", "user"] and is_authenticated:
        return True
    return False
```

**Remove all conflict markers** (`<<<<<<<`, `=======`, `>>>>>>>`).

**7. Mark as resolved:**

```bash
git add app.py
```

**8. Complete the merge:**

```bash
git commit
# Git will open editor with default merge message
# You can edit it or just save and close
```

Or provide a message directly:

```bash
git commit -m "Merge feature-login, resolve authentication conflict"
```

**9. Verify the merge:**

```bash
git log --oneline --graph
```

### Complete Conflict Resolution Example

```bash
# Attempt merge
git switch main
git merge feature-auth

# Output:
# Auto-merging auth.py
# CONFLICT (content): Merge conflict in auth.py
# Automatic merge failed; fix conflicts and then commit the result.

# Check status
git status
# Output:
# Unmerged paths:
#   both modified:   auth.py

# Open and fix the file
code auth.py

# Before (in auth.py):
<<<<<<< HEAD
def authenticate(user):
    return user.password == "admin123"
=======
def authenticate(user):
    return check_password_hash(user.password_hash, user.password)
>>>>>>> feature-auth

# After (your resolution):
def authenticate(user):
    # Use secure password hashing (from feature-auth)
    return check_password_hash(user.password_hash, user.password)

# Stage the resolution
git add auth.py

# Complete the merge
git commit -m "Merge feature-auth, adopt secure password hashing"

# Verify
git log --oneline --graph -5
```

### Best Practices to Avoid Conflicts

**1. Pull frequently:**

```bash
git pull origin main
```

Staying up-to-date reduces the chance of conflicts.

**2. Communicate with your team:**

Don't work on the same files simultaneously if possible.

**3. Make small, frequent commits:**

Smaller changes are easier to merge.

**4. Use feature branches:**

Isolate work, reducing conflicts on `main`.

**5. Rebase your feature branch regularly:**

```bash
git switch feature-branch
git fetch origin
git rebase origin/main
```

This keeps your branch up-to-date with `main`.

**6. When conflicts do occur:**

- Don't panic
- Read the conflict carefully
- Ask teammates if you're unsure whose changes to keep
- Test the code after resolving
- Commit with a clear message

---

## Undoing Changes

Git provides multiple ways to undo changes. Understanding the differences is critical.

### Overview of Undo Commands

| Command | What it does | Affects history? | Danger level |
|---------|--------------|------------------|--------------|
| `git restore` | Discard working directory changes | No | Low |
| `git reset --soft` | Move HEAD, keep changes staged | Yes (local) | Medium |
| `git reset --mixed` | Move HEAD, unstage changes | Yes (local) | Medium |
| `git reset --hard` | Move HEAD, discard all changes | Yes (local) | **HIGH** |
| `git revert` | Create new commit undoing changes | No | Low |

### `git restore`

Discard changes in the working directory or unstage files.

**Discard unstaged changes in a file:**

```bash
git restore filename.txt
```

**Warning:** This **permanently deletes** uncommitted changes.

**Unstage a file (but keep changes):**

```bash
git restore --staged filename.txt
```

**Example:**

```bash
# You edited app.py but want to discard changes
git status
# Output: modified: app.py

git restore app.py

git status
# Output: nothing to commit, working tree clean
```

**Discard all unstaged changes:**

```bash
git restore .
```

**Unstage all files:**

```bash
git restore --staged .
```

### `git reset`

Moves the `HEAD` pointer and optionally changes the staging area and working directory.

**Three modes:**

#### 1. `git reset --soft`

Moves `HEAD`, keeps changes **staged**.

```bash
git reset --soft HEAD~1
```

**Use case:** Undo the last commit but keep all changes staged for re-committing.

**Example:**

```bash
git log --oneline
# a1b2c3d Add feature
# e4f5g6h Previous commit

git reset --soft HEAD~1

git status
# Changes staged, ready to re-commit

git log --oneline
# e4f5g6h Previous commit (a1b2c3d is gone)
```

#### 2. `git reset --mixed` (default)

Moves `HEAD`, **unstages** changes, but keeps them in working directory.

```bash
git reset HEAD~1
# Same as: git reset --mixed HEAD~1
```

**Use case:** Undo commits, make changes, recommit differently.

**Example:**

```bash
git reset HEAD~1

git status
# Changes unstaged, but still present in files
```

#### 3. `git reset --hard`

Moves `HEAD` and **discards all changes**.

```bash
git reset --hard HEAD~1
```

**⚠️ DANGER:** This **permanently deletes** uncommitted work.

**Use case:** Completely abandon recent work.

**Example:**

```bash
git reset --hard HEAD~1
# Last commit and all changes are GONE
```

**Understanding `HEAD~1`:**

- `HEAD~1` = one commit before HEAD
- `HEAD~2` = two commits before HEAD
- `HEAD~3` = three commits before HEAD

**Reset to a specific commit:**

```bash
git reset --hard a1b2c3d
```

### `git revert`

Creates a **new commit** that undoes a previous commit. Doesn't rewrite history.

```bash
git revert commit-hash
```

**Example:**

```bash
git log --oneline
# a1b2c3d Add buggy feature
# e4f5g6h Previous work

git revert a1b2c3d
# Opens editor for revert commit message

git log --oneline
# f7g8h9i Revert "Add buggy feature"
# a1b2c3d Add buggy feature
# e4f5g6h Previous work
```

**Why `git revert` is safer:**

- Doesn't rewrite history
- Safe for public branches
- Creates an audit trail

### When to Use Each Safely

**Use `git restore` when:**

✅ You want to discard **uncommitted** changes
✅ You want to unstage files

**Use `git reset --soft` when:**

✅ You want to undo the last commit but keep changes
✅ You want to combine multiple commits into one

**Use `git reset --mixed` when:**

✅ You want to undo commits and re-stage changes differently

**Use `git reset --hard` when:**

✅ You want to completely abandon recent work
✅ **Only on unpushed/private branches**

**Use `git revert` when:**

✅ You want to undo a commit on a **public branch**
✅ You want to preserve history
✅ Working with teammates

**Professional safety rules:**

1. **Never use `git reset --hard` on pushed commits** (breaks others' work)
2. **Use `git revert` for public branches**
3. **Always verify with `git status` and `git log` before resetting**
4. **Create a backup branch before dangerous operations:**

```bash
git branch backup-before-reset
git reset --hard HEAD~3
# If something goes wrong:
git reset --hard backup-before-reset
```

**Common scenarios:**

**Scenario: Undo last commit, keep changes**

```bash
git reset --soft HEAD~1
# Edit files
git add .
git commit -m "Better commit message"
```

**Scenario: Discard last commit completely**

```bash
git reset --hard HEAD~1
```

**Scenario: Undo a pushed commit**

```bash
git revert commit-hash
git push
```

---

## Working With Remote Repositories

Remote repositories (like GitHub) enable collaboration and backup.

### What is a Remote?

A **remote** is a version of your repository hosted elsewhere (GitHub, GitLab, etc.).

**Key concepts:**

- `origin` — The default name for your main remote repository
- `upstream` — Often used for the original repository when you've forked
- You can have multiple remotes

### `git remote`

Manage remote repositories.

```bash
# List remotes
git remote

# List remotes with URLs
git remote -v

# Add a remote
git remote add <name> <url>

# Remove a remote
git remote remove <name>

# Rename a remote
git remote rename old-name new-name

# Show remote details
git remote show origin
```

**Example:**

```bash
git remote -v
# Output:
# origin  https://github.com/username/project.git (fetch)
# origin  https://github.com/username/project.git (push)
```

### `git push`

Upload your local commits to a remote repository.

```bash
# Push current branch to remote
git push

# Push and set upstream (first time)
git push -u origin branch-name

# Push specific branch
git push origin branch-name

# Push all branches
git push --all

# Push tags
git push --tags

# Force push (DANGEROUS)
git push --force
```

**Example (first push):**

```bash
# You created a new branch
git switch -c feature-login

# Made commits
git commit -m "feat: Add login"

# Push to remote and set upstream
git push -u origin feature-login
# Output: Branch 'feature-login' set up to track remote branch 'feature-login' from 'origin'.
```

**After setting upstream, just:**

```bash
git push
```

**⚠️ Warning about `git push --force`:**

Force push **overwrites** remote history. Only use when:
- Working alone on a feature branch
- You've rebased and need to update remote
- **NEVER on `main` or shared branches**

**Safer alternative:**

```bash
git push --force-with-lease
```

This prevents overwriting others' work.

### `git pull`

Download and integrate changes from a remote repository.

```bash
# Pull current branch
git pull

# Pull specific branch
git pull origin main

# Pull with rebase instead of merge
git pull --rebase
```

**What `git pull` actually does:**

```bash
git pull = git fetch + git merge
```

**Example:**

```bash
git pull origin main
# Output: Updating a1b2c3d..e4f5g6h
#         Fast-forward
#          app.py | 10 +++++++++-
#          1 file changed, 9 insertions(+), 1 deletion(-)
```

### `git fetch`

Download changes from remote **without integrating** them.

```bash
# Fetch all remotes
git fetch

# Fetch specific remote
git fetch origin

# Fetch specific branch
git fetch origin main
```

**Difference between `fetch` and `pull`:**

- `git fetch` — Downloads changes, doesn't modify your working directory
- `git pull` — Downloads changes AND merges them

**Example workflow:**

```bash
# See what's new on remote without affecting your work
git fetch origin

# Compare your branch with remote
git log origin/main

# If safe, merge
git merge origin/main

# Or do both at once
git pull
```

**Professional pattern:**

```bash
# Fetch to see what's new
git fetch origin

# Review changes
git log HEAD..origin/main

# If good, merge
git merge origin/main
```

### Upstream Branches

An **upstream branch** is the remote branch your local branch tracks.

**Set upstream:**

```bash
git push -u origin branch-name
```

**After setting upstream:**

```bash
# Just use:
git push
git pull

# Instead of:
git push origin branch-name
git pull origin branch-name
```

**Check upstream:**

```bash
git branch -vv
# Output:
# * main                a1b2c3d [origin/main] Latest commit
#   feature-login       e4f5g6h [origin/feature-login: ahead 2] Add login
```

**Set upstream for existing branch:**

```bash
git branch --set-upstream-to=origin/branch-name
```

---

## GitHub Essentials

GitHub is the most popular platform for hosting Git repositories.

### Creating a GitHub Repository

**Two ways to start:**

#### 1. Create on GitHub first, then clone

**On GitHub:**
1. Click "New Repository"
2. Enter repository name
3. Choose public/private
4. Optionally add README, .gitignore, license
5. Click "Create repository"

**On your computer:**
```bash
git clone https://github.com/username/repository-name.git
cd repository-name
# Start working
```

#### 2. Create locally, then push to GitHub

**On your computer:**
```bash
mkdir my-project
cd my-project
git init
git add .
git commit -m "Initial commit"
```

**On GitHub:**
1. Create a new empty repository (don't add README, .gitignore)

**On your computer:**
```bash
git remote add origin https://github.com/username/repository-name.git
git branch -M main
git push -u origin main
```

### HTTPS vs SSH

Two ways to connect to GitHub:

#### HTTPS

**Format:**
```
https://github.com/username/repository.git
```

**Pros:**
- Easier to set up
- Works everywhere
- No extra configuration

**Cons:**
- Requires entering password/token each time (unless cached)

**Example:**
```bash
git clone https://github.com/username/project.git
```

#### SSH

**Format:**
```
git@github.com:username/repository.git
```

**Pros:**
- No password needed after setup
- More secure
- Faster for frequent pushes

**Cons:**
- Requires SSH key setup

**Setup SSH (one-time):**

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key
cat ~/.ssh/id_ed25519.pub
# Copy the output

# Add to GitHub:
# GitHub → Settings → SSH and GPG keys → New SSH key
# Paste the key, save
```

**Example:**
```bash
git clone git@github.com:username/project.git
```

**Switch existing repo from HTTPS to SSH:**

```bash
git remote set-url origin git@github.com:username/repository.git
```

### Connecting Local Repo to GitHub

**Scenario:** You have a local repository and want to push it to GitHub.

**Steps:**

1. Create empty repository on GitHub (don't initialize with README)

2. Connect local repo:

```bash
# Add remote
git remote add origin https://github.com/username/repository.git

# Verify
git remote -v

# Push
git branch -M main  # Rename branch to main if needed
git push -u origin main
```

**Troubleshooting:**

**Error: "remote origin already exists"**
```bash
git remote remove origin
git remote add origin https://github.com/username/repository.git
```

**Error: "failed to push some refs"**
```bash
# Pull first, then push
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### README.md Best Practices

A `README.md` is the first thing people see on your repository.

**Essential sections:**

```markdown
# Project Name

Brief description of what this project does.

## Features

- Feature 1
- Feature 2
- Feature 3

## Installation

```bash
git clone https://github.com/username/project.git
cd project
pip install -r requirements.txt
```

## Usage

```python
from myproject import main

main.run()
```

## Contributing

Contributions welcome! Please read CONTRIBUTING.md first.

## License

MIT License - see LICENSE file for details.

## Contact

Your Name - your.email@example.com
```

**README best practices:**

✅ **Do:**
- Include clear installation instructions
- Show example usage
- Explain what problem the project solves
- Add badges (build status, license, etc.)
- Use screenshots/GIFs for visual projects
- Keep it concise but informative

❌ **Don't:**
- Write a novel
- Assume prior knowledge
- Forget to update when project changes
- Leave placeholder text

**Example professional README:**

```markdown
# TaskMaster API

A RESTful API for task management built with Python and FastAPI.

![Build Status](https://img.shields.io/github/workflow/status/username/taskmaster/CI)
![License](https://img.shields.io/github/license/username/taskmaster)

## Quick Start

```bash
# Clone the repository
git clone https://github.com/username/taskmaster.git
cd taskmaster

# Install dependencies
pip install -r requirements.txt

# Run the server
uvicorn main:app --reload
```

## Features

- ✅ Create, read, update, delete tasks
- ✅ User authentication with JWT
- ✅ PostgreSQL database
- ✅ OpenAPI documentation
- ✅ Comprehensive test suite

## API Documentation

Once running, visit `http://localhost:8000/docs` for interactive API documentation.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.
```

---

## Pull Requests

Pull requests (PRs) are how teams review and merge code changes.

### What is a Pull Request?

A **pull request** is a request to merge your branch into another branch (usually `main`).

**Why pull requests exist:**

1. **Code review:** Others can review your changes before merging
2. **Discussion:** Team can discuss the changes
3. **Quality control:** Catch bugs before they reach production
4. **Continuous Integration:** Automated tests run on your code
5. **Documentation:** PRs create a record of why changes were made

**Analogy:** A pull request is like submitting a draft paper to your professor for feedback before final submission.

### Why PRs Are Important

**In professional development:**

- **No code reaches `main` without review**
- PRs enable mentorship (senior devs review junior code)
- PRs catch bugs early
- PRs ensure code meets standards
- PRs facilitate knowledge sharing

**Real-world example:**

Without PRs:
```bash
git switch main
git merge feature-payment
git push
# Broken code is now in production 🔥
```

With PRs:
```bash
git push origin feature-payment
# Create PR on GitHub
# Team reviews
# Tests run automatically
# Bugs caught
# Code approved
# THEN merged to main
```

### Creating a Pull Request (Step-by-Step)

**1. Create and push your feature branch:**

```bash
git switch -c feature/add-user-profile
# Make changes
git add .
git commit -m "feat: Add user profile page"
git push -u origin feature/add-user-profile
```

**2. On GitHub:**

- Go to your repository
- You'll see: "feature/add-user-profile had recent pushes"
- Click **"Compare & pull request"**

**3. Fill out the PR form:**

**Title:** Clear, descriptive
```
feat: Add user profile page
```

**Description:** Explain what and why
```markdown
## What
Adds a user profile page where users can view and edit their information.

## Why
Implements feature requested in issue #42.

## Changes
- Created profile component
- Added profile route
- Integrated with user API
- Added profile tests

## Screenshots
[attach screenshot]

## Testing
- [ ] Unit tests pass
- [ ] Manual testing completed
- [ ] Works on mobile

Closes #42
```

**4. Reviewers & Labels:**

- Assign reviewers (teammates who'll review your code)
- Add labels (`feature`, `bug`, `documentation`)
- Link related issues

**5. Create pull request**

**6. Address review feedback:**

Reviewers might request changes:

```bash
# Make requested changes locally
git add .
git commit -m "Address review feedback"
git push
# PR automatically updates
```

**7. Merge:**

Once approved:
- Click **"Merge pull request"**
- Choose merge type (usually "Create a merge commit")
- Delete the feature branch (GitHub offers this option)

### Reviewing Pull Requests

**As a reviewer:**

1. **Read the description:** Understand what's being changed and why

2. **Review the code:**
   - Does it solve the problem?
   - Is it readable?
   - Are there tests?
   - Any security issues?
   - Performance concerns?

3. **Leave feedback:**

**Types of comments:**

✅ **Approve:** Code looks good
💬 **Comment:** Suggestion, not blocking
🚫 **Request changes:** Must be fixed before merging

**Good review comments:**

✅ **Constructive:**
```
Consider extracting this logic into a separate function for better testability.
```

❌ **Not helpful:**
```
This is bad.
```

✅ **Specific:**
```
Line 42: This could cause a null pointer exception if user.email is None. 
Consider adding a check.
```

✅ **Positive:**
```
Nice solution! This is much cleaner than the previous approach.
```

4. **Approve or request changes**

### Best Practices for Pull Requests

**Creating PRs:**

✅ **Do:**
- Keep PRs small (< 400 lines changed)
- One feature/fix per PR
- Write clear descriptions
- Include tests
- Update documentation
- Self-review before requesting review
- Respond to feedback promptly

❌ **Don't:**
- Create massive PRs (hard to review)
- Mix unrelated changes
- Leave vague descriptions
- Submit without testing
- Take feedback personally

**PR size guidelines:**

- **Tiny:** < 50 lines — Quick review
- **Small:** 50-200 lines — Ideal
- **Medium:** 200-400 lines — OK
- **Large:** 400-1000 lines — Too big, consider splitting
- **Huge:** > 1000 lines — Definitely split

**Reviewing PRs:**

✅ **Do:**
- Review promptly (within 24 hours)
- Be respectful and constructive
- Ask questions if unclear
- Praise good work
- Test the changes locally if needed
- Focus on important issues

❌ **Don't:**
- Nitpick minor style issues (use linters)
- Be dismissive or rude
- Approve without actually reviewing
- Request changes without explanation

**PR description template:**

```markdown
## Summary
Brief description of changes

## Type of change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Related issues
Closes #123

## Changes made
- Change 1
- Change 2
- Change 3

## Testing
- [ ] Unit tests added/updated
- [ ] Manual testing completed
- [ ] All tests pass

## Screenshots (if applicable)
[attach images]

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-reviewed code
- [ ] Commented complex code
- [ ] Updated documentation
- [ ] No new warnings
```

---

## .gitignore

`.gitignore` tells Git which files to ignore.

### What .gitignore Is

A `.gitignore` file contains patterns of files/folders that Git should **not track**.

**Example `.gitignore`:**

```
# Ignore all .log files
*.log

# Ignore the node_modules directory
node_modules/

# Ignore .env files
.env

# Ignore all files in build/ directory
build/
```

### Why It Matters

**You should ignore:**

1. **Secrets:** API keys, passwords, tokens
2. **Generated files:** Compiled code, build artifacts
3. **Dependencies:** `node_modules/`, `venv/`
4. **OS files:** `.DS_Store`, `Thumbs.db`
5. **IDE files:** `.vscode/`, `.idea/`
6. **Temporary files:** `*.tmp`, `*.cache`

**Why ignore these:**

- **Security:** Don't commit secrets to GitHub
- **Repository size:** Dependencies are huge
- **Noise:** Generated files clutter history
- **Conflicts:** OS/IDE files cause merge conflicts
- **Reproducibility:** Dependencies should be installed, not committed

### Common .gitignore Patterns

**Pattern syntax:**

```
# Comment

# Ignore specific file
secret.txt

# Ignore all files with extension
*.log

# Ignore directory
build/

# Ignore all txt files in docs/
docs/*.txt

# But don't ignore this specific file
!important.txt

# Ignore files anywhere in the tree
**/temp.txt

# Ignore only in root
/config.json
```

**Examples:**

```
# Ignore all .log files in any directory
*.log

# Ignore logs/ directory
logs/

# Ignore all .tmp files in any subdirectory
**/*.tmp

# Ignore .env but not .env.example
.env
!.env.example
```

### Language-Specific Examples

#### Python

```
# Byte-compiled / optimized files
__pycache__/
*.py[cod]
*$py.class

# Virtual environments
venv/
env/
ENV/

# Distribution / packaging
build/
dist/
*.egg-info/

# Unit test / coverage
.pytest_cache/
.coverage
htmlcov/

# Environment variables
.env

# IDE
.vscode/
.idea/
*.swp
```

#### JavaScript/Node.js

```
# Dependencies
node_modules/

# Build output
dist/
build/

# Environment variables
.env
.env.local

# Logs
*.log
npm-debug.log*

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
```

#### Java

```
# Compiled class files
*.class

# Package files
*.jar
*.war
*.ear

# Build directories
target/
build/

# IDE files
.idea/
*.iml
.eclipse/
```

#### C/C++

```
# Compiled object files
*.o
*.obj

# Executables
*.exe
*.out
a.out

# Libraries
*.a
*.so
*.dll

# Build directories
build/
cmake-build-*/
```

### Global .gitignore

Create a global `.gitignore` for files you never want to commit:

**1. Create the file:**

```bash
touch ~/.gitignore_global
```

**2. Add common ignores:**

```
# OS files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/
*.swp
*.swo

# Temp files
*.tmp
*.bak
*~
```

**3. Configure Git to use it:**

```bash
git config --global core.excludesfile ~/.gitignore_global
```

Now these files are ignored in **all** your repositories.

**Example workflow:**

```bash
# Create .gitignore
touch .gitignore

# Add patterns
echo "*.log" >> .gitignore
echo ".env" >> .gitignore
echo "node_modules/" >> .gitignore

# Commit .gitignore itself
git add .gitignore
git commit -m "Add .gitignore"
```

**What if you already committed a file?**

```bash
# Remove from Git but keep locally
git rm --cached filename

# Remove directory from Git but keep locally
git rm -r --cached directory/

# Commit the removal
git commit -m "Remove ignored files from repository"
```

**Check if a file is ignored:**

```bash
git check-ignore -v filename
```

**Resources:**

- [gitignore.io](https://gitignore.io) — Generate `.gitignore` for your stack
- [GitHub's gitignore templates](https://github.com/github/gitignore)

---

## Tags & Releases

Tags mark specific points in history, usually for releases.

### Git Tags (Lightweight vs Annotated)

**Two types of tags:**

#### 1. Lightweight Tags

Simple pointer to a commit.

```bash
git tag v1.0.0
```

**Use case:** Temporary markers or personal use.

#### 2. Annotated Tags

Full objects with metadata (recommended for releases).

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

**Includes:**
- Tagger name and email
- Date
- Message
- Can be signed (GPG)

**Recommended:** Use annotated tags for all releases.

### Creating Tags

```bash
# Create annotated tag
git tag -a v1.0.0 -m "Release 1.0.0: Initial public release"

# Create lightweight tag
git tag v1.0.0

# Tag a specific commit
git tag -a v0.9.0 a1b2c3d -m "Beta release"

# List tags
git tag

# List tags with pattern
git tag -l "v1.*"

# Show tag details
git show v1.0.0

# Delete a tag locally
git tag -d v1.0.0

# Delete a tag remotely
git push origin --delete v1.0.0
```

**Example:**

```bash
# Your project is ready for release
git tag -a v1.0.0 -m "Release 1.0.0

Features:
- User authentication
- Task management
- API documentation

This is the first stable release."

# Push tag to remote
git push origin v1.0.0

# Or push all tags
git push --tags
```

### GitHub Releases

GitHub Releases turn tags into formal releases with notes and files.

**Creating a release:**

**1. On GitHub:**

- Go to repository → Releases → "Create a new release"

**2. Fill out:**

- **Tag version:** `v1.0.0` (choose existing tag or create new)
- **Release title:** `Version 1.0.0 - Initial Release`
- **Description:**

```markdown
## Features
- User authentication with JWT
- RESTful API for tasks
- PostgreSQL database integration

## Bug Fixes
- Fixed login session timeout
- Corrected task sorting

## Breaking Changes
None

## Installation
Download the appropriate file for your platform below.
```

**3. Attach files (optional):**

- Compiled binaries
- Documentation PDFs
- Installer packages

**4. Publish release**

**From command line (using GitHub CLI):**

```bash
# Install GitHub CLI first
gh release create v1.0.0 --title "Version 1.0.0" --notes "Release notes here"
```

### Versioning Basics (SemVer)

**Semantic Versioning (SemVer):** `MAJOR.MINOR.PATCH`

**Format:** `1.4.2`

- **MAJOR (1):** Breaking changes (incompatible API changes)
- **MINOR (4):** New features (backward-compatible)
- **PATCH (2):** Bug fixes (backward-compatible)

**Examples:**

- `1.0.0` → `1.0.1` — Bug fix
- `1.0.1` → `1.1.0` — New feature added
- `1.1.0` → `2.0.0` — Breaking change

**Pre-release versions:**

- `1.0.0-alpha` — Alpha version
- `1.0.0-beta.1` — Beta version 1
- `1.0.0-rc.2` — Release candidate 2

**Example release workflow:**

```bash
# Start with 0.1.0 (initial development)
git tag -a v0.1.0 -m "Initial development release"

# Add features
git tag -a v0.2.0 -m "Added user authentication"

# First stable release
git tag -a v1.0.0 -m "First stable release"

# Bug fix
git tag -a v1.0.1 -m "Fixed login bug"

# New feature
git tag -a v1.1.0 -m "Added password reset"

# Breaking change
git tag -a v2.0.0 -m "Redesigned API (breaking changes)"

# Push all tags
git push --tags
```

---

## Stashing

Stashing temporarily saves changes without committing.

### What `git stash` Does

**Stash** saves your uncommitted changes and reverts your working directory to match HEAD.

**Use cases:**

- Switch branches quickly without committing
- Pull changes when you have uncommitted work
- Temporarily set aside work in progress

**Think of it as:** A clipboard for your changes.

### Common Stash Commands

```bash
# Stash current changes
git stash

# Stash with a message
git stash save "Work in progress on login feature"

# List stashes
git stash list

# Apply most recent stash (keeps it in stash list)
git stash apply

# Apply and remove most recent stash
git stash pop

# Apply specific stash
git stash apply stash@{1}

# Show stash contents
git stash show

# Show stash diff
git stash show -p

# Delete most recent stash
git stash drop

# Delete specific stash
git stash drop stash@{1}

# Delete all stashes
git stash clear

# Stash including untracked files
git stash -u

# Stash including untracked and ignored files
git stash -a
```

### When to Use Stashing

**Scenario 1: Need to switch branches**

```bash
# You're working on feature-login
git status
# Output: Changes not staged for commit: modified: login.py

# Need to switch to main urgently
git stash

# Now you can switch
git switch main

# Fix urgent bug, commit, then return
git switch feature-login

# Restore your work
git stash pop
```

**Scenario 2: Pull changes with uncommitted work**

```bash
# You have uncommitted changes
git pull
# Error: Your local changes would be overwritten by merge

# Stash changes
git stash

# Pull
git pull

# Restore changes
git stash pop
```

**Scenario 3: Try something experimental**

```bash
# Save current work
git stash

# Try experimental approach
# ... (make changes)

# If it doesn't work:
git restore .

# Restore original work
git stash pop
```

**Complete example:**

```bash
# Working on feature
git status
# modified: app.py
# modified: styles.css

# Stash with message
git stash save "WIP: Refactoring authentication"

# Verify clean working directory
git status
# nothing to commit, working tree clean

# List stashes
git stash list
# stash@{0}: On feature-auth: WIP: Refactoring authentication

# Do other work...

# Restore stash
git stash pop
# Output: On branch feature-auth
#         Changes not staged for commit:
#           modified: app.py
#           modified: styles.css
#         Dropped refs/stash@{0}

# Continue working
```

**Stash with conflicts:**

If changes conflict when applying stash:

```bash
git stash pop
# Output: CONFLICT (content): Merge conflict in app.py

# Resolve conflicts manually
# Edit app.py, remove markers

git add app.py
# Stash entry is automatically dropped after resolution
```

---

## Collaboration Workflows

Different teams use different Git workflows. Here are the most common.

### Centralized Workflow

**How it works:**

- Everyone works on `main`
- Pull before pushing
- Simple but risky

**Process:**

```bash
git pull origin main
# Make changes
git add .
git commit -m "Add feature"
git pull origin main  # Get latest changes
git push origin main
```

**Pros:**
- Simple
- Familiar (like SVN)

**Cons:**
- No code review
- Broken code goes directly to `main`
- Conflicts are common

**Best for:** Very small teams or solo projects.

### Feature Branch Workflow

**How it works:**

- Create a branch for each feature
- Merge to `main` when done
- Enables code review via pull requests

**Process:**

```bash
# Create feature branch
git switch -c feature/user-profile

# Work on feature
git add .
git commit -m "Add user profile"

# Push to remote
git push -u origin feature/user-profile

# Create pull request on GitHub
# After review and approval, merge to main
# Delete feature branch
```

**Pros:**
- Isolated work
- Code review via PRs
- `main` stays stable

**Cons:**
- Requires discipline
- Can have merge conflicts

**Best for:** Most teams (this is the most common workflow).

### GitHub Flow

**How it works:**

- `main` is always deployable
- Create feature branches
- Pull request + review
- Merge and deploy

**Rules:**

1. `main` is always deployable
2. Create descriptive branches (`feature/add-payment`)
3. Commit often
4. Open pull request early
5. Merge only after review
6. Deploy immediately after merge

**Process:**

```bash
# 1. Update main
git switch main
git pull origin main

# 2. Create branch
git switch -c feature/add-payment

# 3. Work and commit
git add payment.py
git commit -m "feat: Add payment processing"

git add payment_test.py
git commit -m "test: Add payment tests"

# 4. Push
git push -u origin feature/add-payment

# 5. Create PR on GitHub

# 6. Review, discuss, update

# 7. After approval, merge PR

# 8. Delete branch

# 9. Deploy main to production
```

**Pros:**
- Simple
- Fast feedback
- Continuous deployment friendly

**Cons:**
- Requires automation (CI/CD)
- Less suitable for scheduled releases

**Best for:** Web applications, continuous deployment.

### Basic Git Flow Overview

**How it works:**

- Multiple long-lived branches
- `main` — production code
- `develop` — integration branch
- Feature branches → `develop`
- Release branches → `main`
- Hotfix branches → `main` and `develop`

**Branches:**

```
main (production)
├── hotfix/critical-bug → main & develop
develop (integration)
├── feature/user-auth → develop
├── feature/payment → develop
└── release/v1.0.0 → main & develop
```

**Process:**

```bash
# Start feature
git switch develop
git switch -c feature/payment

# Work
git commit -m "Add payment"

# Merge to develop
git switch develop
git merge feature/payment

# Create release
git switch -c release/v1.0.0

# Fix release bugs
git commit -m "Fix release bug"

# Merge to main
git switch main
git merge release/v1.0.0
git tag -a v1.0.0

# Merge back to develop
git switch develop
git merge release/v1.0.0

# Hotfix
git switch main
git switch -c hotfix/critical-bug
git commit -m "Fix critical bug"
git switch main
git merge hotfix/critical-bug
git tag -a v1.0.1
git switch develop
git merge hotfix/critical-bug
```

**Pros:**
- Organized
- Clear release process
- Supports scheduled releases

**Cons:**
- Complex
- Overkill for small projects

**Best for:** Large projects, scheduled releases, multiple versions in production.

**Summary:**

| Workflow | Complexity | Best For |
|----------|------------|----------|
| Centralized | Simple | Solo projects |
| Feature Branch | Medium | Most teams |
| GitHub Flow | Simple-Medium | Web apps, continuous deployment |
| Git Flow | Complex | Large projects, scheduled releases |

**Recommendation:** Start with **Feature Branch Workflow**. It's the industry standard and works for most teams.

---

## Real-World Workflows: Easy, Intermediate & Expert

This section shows you how Git and GitHub are used in real projects, organized by difficulty. Each example is a complete, copy-paste-ready workflow you can use today.

---

### Easy Level: Solo Developer

These workflows are for people working alone on personal projects, homework, or learning to code.

#### Example 1: Personal Portfolio Website

**Scenario:** You're building a portfolio website and want to track your progress.

```bash
# === ONE-TIME SETUP ===
mkdir portfolio
cd portfolio
git init

# Create your first files
echo "<!DOCTYPE html><html><body><h1>My Portfolio</h1></body></html>" > index.html
echo "body { font-family: sans-serif; }" > style.css

git add index.html style.css
git commit -m "Create portfolio homepage"

# Connect to GitHub (create repo on github.com first)
git remote add origin https://github.com/your-username/portfolio.git
git push -u origin main
```

```bash
# === DAILY WORKFLOW ===
# Edit your files...

# Check what changed
git status

# Save your work
git add .
git commit -m "Add projects section to homepage"
git push
```

#### Example 2: Keeping Notes or Documentation

**Scenario:** You use Git to version-control your study notes.

```bash
# Start tracking your notes
cd my-notes
git init

# Add all existing notes
git add .
git commit -m "Add existing study notes"

# After studying...
git add biology-chapter5.md
git commit -m "Add Biology Chapter 5 notes"

# Next day...
git add math-formulas.md
git commit -m "Add calculus formula sheet"

# Review your study history
git log --oneline
# Output:
# c3d4e5f Add calculus formula sheet
# a1b2c3d Add Biology Chapter 5 notes
# 9f8e7d6 Add existing study notes
```

#### Example 3: Saving a School or University Project

**Scenario:** You're working on a Python assignment and want safe checkpoints.

```bash
# Initialize
cd python-assignment
git init

# Save first version
git add main.py
git commit -m "Add basic calculator functions"

# You try something risky...
git add main.py
git commit -m "Attempt: Add scientific calculator mode"

# It broke everything! Go back to the working version
git log --oneline
# a1b2c3d Attempt: Add scientific calculator mode
# e4f5g6h Add basic calculator functions

git revert a1b2c3d
# Now you're back to the working version, and the history shows what happened
```

---

### Intermediate Level: Small Team (2-5 People)

These workflows are for teams working on shared projects using branches and pull requests.

#### Example 4: Building a Web App with a Friend

**Scenario:** You and a friend are building a to-do app. You handle the backend, they handle the frontend.

```bash
# === YOUR SETUP (Backend Developer) ===
git clone https://github.com/team/todo-app.git
cd todo-app

# Create your feature branch
git switch -c feature/api-endpoints

# Build the API
# ... edit files ...
git add server.py routes.py
git commit -m "feat: Add CRUD endpoints for tasks"

git add database.py
git commit -m "feat: Add SQLite database integration"

# Push your branch
git push -u origin feature/api-endpoints

# Go to GitHub → Create Pull Request
# Title: "feat: Add backend API for task management"
# Your friend reviews your code, suggests changes

# Address their feedback
git add server.py
git commit -m "fix: Add input validation per review feedback"
git push

# After approval → Merge PR on GitHub
# Then clean up locally
git switch main
git pull origin main
git branch -d feature/api-endpoints
```

```bash
# === YOUR FRIEND'S SETUP (Frontend Developer) ===
git clone https://github.com/team/todo-app.git
cd todo-app

git switch -c feature/todo-ui

# Build the UI
git add index.html style.css app.js
git commit -m "feat: Add task list UI with add/delete buttons"

git push -u origin feature/todo-ui
# Create PR, get reviewed, merge
```

#### Example 5: Fixing a Bug Reported by a User

**Scenario:** A user reports that the login page crashes on mobile. You need to fix it urgently.

```bash
# Start from the latest main
git switch main
git pull origin main

# Create a bugfix branch
git switch -c bugfix/login-mobile-crash

# Investigate and fix the bug
# ... edit login.css and login.js ...

# Test your fix, then commit
git add login.css login.js
git commit -m "fix: Resolve login page crash on mobile devices

The login form container had a fixed width that caused
overflow on screens smaller than 375px. Changed to
max-width with percentage-based sizing.

Fixes #87"

# Push and create PR
git push -u origin bugfix/login-mobile-crash

# On GitHub: Create PR, link to issue #87
# After review → merge → the fix is live
```

#### Example 6: Working on the Same File as a Teammate

**Scenario:** Both you and your teammate edited `config.py`. Now you need to merge.

```bash
# You're on your branch, ready to merge
git switch main
git pull origin main
git switch feature/update-config
git merge main

# OH NO — merge conflict!
# Output: CONFLICT (content): Merge conflict in config.py

# Open config.py — you'll see:
# <<<<<<< HEAD
# DATABASE_URL = "postgresql://localhost/myapp_v2"
# =======
# DATABASE_URL = "postgresql://localhost/myapp_production"
# >>>>>>> main

# Talk to your teammate! Decide which is correct.
# Edit the file to keep the right version:
# DATABASE_URL = "postgresql://localhost/myapp_production"
# (Remove ALL conflict markers: <<<<<<<, =======, >>>>>>>)

git add config.py
git commit -m "fix: Resolve merge conflict in config.py, use production DB URL"
git push
```

---

### Expert Level: Professional Team & Open Source

These workflows are for production environments, CI/CD pipelines, and open-source contributions.

#### Example 7: Full Feature Development with CI/CD

**Scenario:** You're a developer at a company. You need to add a payment system. The team uses GitHub Flow with automated tests.

```bash
# === MORNING: Start the feature ===
git switch main
git pull origin main
git switch -c feature/payment-integration

# === DEVELOP IN SMALL COMMITS ===
# Step 1: Data model
git add models/payment.py
git commit -m "feat: Add Payment model with Stripe fields"

# Step 2: Business logic
git add services/payment_service.py
git commit -m "feat: Add payment processing service with Stripe SDK"

# Step 3: API endpoints
git add api/payment_routes.py
git commit -m "feat: Add POST /api/payments and GET /api/payments/:id"

# Step 4: Tests (always write tests!)
git add tests/test_payment_service.py tests/test_payment_routes.py
git commit -m "test: Add unit and integration tests for payment system"

# Step 5: Documentation
git add docs/api/payments.md
git commit -m "docs: Add payment API documentation"

# === BEFORE PR: Clean up and sync ===
# Get latest main changes
git fetch origin
git rebase origin/main

# If conflicts occur during rebase:
# Fix the file, then:
git add .
git rebase --continue

# Interactive rebase to clean up commits (squash WIP commits)
# git rebase -i origin/main
# (Mark small commits as "squash" to combine them)

# Push (force needed after rebase)
git push -u origin feature/payment-integration
# If already pushed before: git push --force-with-lease

# === CREATE PR ===
# On GitHub, create PR with:
# Title: "feat: Add Stripe payment integration"
# Body:
#   ## Summary
#   - Adds Stripe payment processing
#   - New API endpoints for creating and viewing payments
#   - Full test coverage
#   ## Testing
#   - [x] Unit tests pass
#   - [x] Integration tests pass
#   - [x] Manual testing with Stripe test keys
#   Closes #156

# CI/CD pipeline runs automatically:
# ✅ Linting passes
# ✅ Unit tests pass
# ✅ Integration tests pass
# ✅ Security scan clean

# === AFTER APPROVAL ===
# Merge via GitHub (Squash and merge)
# Delete branch on GitHub

# Local cleanup
git switch main
git pull origin main
git branch -d feature/payment-integration
```

#### Example 8: Contributing to Open Source

**Scenario:** You found a bug in a popular open-source library and want to submit a fix.

```bash
# === STEP 1: Fork and Clone ===
# On GitHub: Click "Fork" on the project page
# This creates YOUR copy: github.com/YOUR-USERNAME/cool-library

git clone https://github.com/YOUR-USERNAME/cool-library.git
cd cool-library

# Add the original project as "upstream"
git remote add upstream https://github.com/original-author/cool-library.git
git remote -v
# origin    https://github.com/YOUR-USERNAME/cool-library.git (fetch)
# origin    https://github.com/YOUR-USERNAME/cool-library.git (push)
# upstream  https://github.com/original-author/cool-library.git (fetch)
# upstream  https://github.com/original-author/cool-library.git (push)

# === STEP 2: Stay in Sync ===
git fetch upstream
git switch main
git merge upstream/main
git push origin main

# === STEP 3: Create Your Fix ===
git switch -c fix/csv-parser-unicode-error

# Fix the bug
# ... edit parser.py ...
git add parser.py
git commit -m "fix: Handle Unicode BOM in CSV parser

The CSV parser raised UnicodeDecodeError when reading files
with UTF-8 BOM (byte order mark). Added BOM detection and
stripping before parsing.

Fixes original-author/cool-library#423"

# Add a test for the bug
git add tests/test_parser.py
git commit -m "test: Add test case for Unicode BOM in CSV files"

# === STEP 4: Push to YOUR Fork ===
git push -u origin fix/csv-parser-unicode-error

# === STEP 5: Create PR to the Original Project ===
# On GitHub: Go to original-author/cool-library
# Click "New Pull Request"
# Choose: base=main (original) ← compare=fix/csv-parser-unicode-error (your fork)
#
# Write a clear PR description:
# Title: "fix: Handle Unicode BOM in CSV parser"
# Body:
#   ## Problem
#   CSV files with UTF-8 BOM cause UnicodeDecodeError (#423)
#
#   ## Solution
#   Detect and strip BOM bytes before parsing.
#
#   ## Testing
#   Added test with BOM-encoded CSV fixture file.

# === STEP 6: Respond to Maintainer Feedback ===
# The maintainer may ask for changes
git add parser.py
git commit -m "refactor: Use codecs.BOM_UTF8 constant per review"
git push
# The PR updates automatically

# === AFTER MERGE ===
# Sync your fork
git switch main
git fetch upstream
git merge upstream/main
git push origin main
git branch -d fix/csv-parser-unicode-error
```

#### Example 9: Hotfix in Production (Emergency)

**Scenario:** Production is down! A critical bug was found. You need to fix it immediately.

```bash
# === EMERGENCY FIX ===
# Drop everything. Start from main (which is deployed to production).
git switch main
git pull origin main

# Create hotfix branch
git switch -c hotfix/fix-auth-crash

# Fix the critical bug (be surgical — change as little as possible)
git add auth/session.py
git commit -m "hotfix: Fix null session token causing auth crash

Production users were getting 500 errors because the session
middleware did not handle expired tokens returning null.
Added null check before token validation.

Incident: INC-2024-0892"

# Push immediately
git push -u origin hotfix/fix-auth-crash

# Create PR — mark as URGENT
# Get emergency review (1 reviewer minimum)
# Merge immediately after approval

# Tag the hotfix release
git switch main
git pull origin main
git tag -a v2.3.1 -m "Hotfix: Fix auth crash (INC-2024-0892)"
git push origin v2.3.1

# Deploy to production immediately

# Don't forget to merge hotfix into develop too
git switch develop
git merge main
git push origin develop

# Clean up
git branch -d hotfix/fix-auth-crash
```

#### Example 10: Managing a Release (Release Manager Workflow)

**Scenario:** Your team is ready to release v2.0.0. You're the release manager.

```bash
# === STEP 1: Create Release Branch ===
git switch develop
git pull origin develop
git switch -c release/v2.0.0

# === STEP 2: Final Fixes on Release Branch ===
# Only bug fixes allowed — no new features!
git add config.py
git commit -m "fix: Update version number to 2.0.0"

git add changelog.md
git commit -m "docs: Update CHANGELOG for v2.0.0"

# QA tests the release branch...
# Fix any bugs found:
git add auth.py
git commit -m "fix: Correct session timeout value for production"

git push -u origin release/v2.0.0

# === STEP 3: Merge to Main (Production) ===
# Create PR: release/v2.0.0 → main
# After approval:
git switch main
git pull origin main
git merge release/v2.0.0
git push origin main

# === STEP 4: Tag the Release ===
git tag -a v2.0.0 -m "Release v2.0.0

New Features:
- User dashboard redesign
- Payment integration with Stripe
- Real-time notifications

Bug Fixes:
- Fixed login timeout issue
- Corrected tax calculation
- Resolved mobile layout bugs

Breaking Changes:
- API v1 endpoints deprecated (use v2)"

git push origin v2.0.0

# === STEP 5: Create GitHub Release ===
# On GitHub: Releases → Create Release
# Select tag v2.0.0
# Add release notes
# Attach compiled binaries if applicable

# === STEP 6: Merge Back to Develop ===
git switch develop
git merge main
git push origin develop

# === STEP 7: Clean Up ===
git branch -d release/v2.0.0
git push origin --delete release/v2.0.0

# === DONE! v2.0.0 is live! ===
```

### Workflow Difficulty Summary

| Level | Who It's For | Key Skills | Examples |
|-------|-------------|------------|----------|
| **Easy** | Solo developers, students | `add`, `commit`, `push`, `log` | Portfolio, notes, assignments |
| **Intermediate** | Small teams (2-5 people) | Branches, PRs, merge conflicts | Web apps, team projects, bug fixes |
| **Expert** | Professional teams, open source | Rebase, CI/CD, releases, hotfixes | Production apps, open source, release management |

> **Tip:** Start at the Easy level and work your way up. You don't need to learn everything at once. Each level builds on the previous one.

---

## Best Practices & Daily Workflow

### Daily Git Routine

**Start of day:**

```bash
# 1. Switch to main
git switch main

# 2. Pull latest changes
git pull origin main

# 3. Create feature branch
git switch -c feature/today-work
```

**During the day:**

```bash
# Make changes
# ...

# Check status frequently
git status

# Stage and commit
git add .
git commit -m "feat: Add validation logic"

# Push regularly (backup + collaboration)
git push
```

**End of day:**

```bash
# Ensure everything is committed
git status

# Push to remote
git push

# If work is incomplete, note it in commit message
git commit -m "WIP: Refactoring payment module (incomplete)"
```

**Professional daily habits:**

1. **Pull before starting:** `git pull origin main`
2. **Commit often:** Small, logical commits
3. **Push regularly:** Don't lose work
4. **Check status constantly:** `git status`
5. **Write good commit messages**
6. **Keep `main` updated:** Merge/rebase frequently

### Branch Naming Conventions

**Format:**

```
<type>/<description>
```

**Types:**

- `feature/` — New features
- `bugfix/` or `fix/` — Bug fixes
- `hotfix/` — Urgent fixes
- `docs/` — Documentation
- `refactor/` — Code restructuring
- `test/` — Adding tests
- `chore/` — Maintenance

**Examples:**

✅ **Good:**
```
feature/user-authentication
feature/payment-integration
bugfix/navbar-mobile-layout
hotfix/security-vulnerability
docs/api-endpoints
refactor/database-queries
```

❌ **Bad:**
```
my-branch
test
fix
new-stuff
branch1
```

**Best practices:**

- Use lowercase
- Use hyphens, not underscores
- Be descriptive but concise
- Include issue number if applicable: `feature/42-add-login`

### Commit Hygiene

**Good commit practices:**

✅ **Do:**
- Commit logically related changes together
- Write clear commit messages
- Commit frequently
- Test before committing
- Review your changes (`git diff`) before committing

❌ **Don't:**
- Commit broken code
- Mix unrelated changes
- Write vague messages ("fixed stuff")
- Commit generated files
- Commit secrets or API keys

**Reviewing before commit:**

```bash
# See what changed
git diff

# See what's staged
git diff --staged

# Review file by file
git add -p
```

**Amending last commit:**

```bash
# Forgot to include a file
git add forgotten_file.py
git commit --amend --no-edit

# Fix commit message
git commit --amend -m "Better commit message"
```

**Warning:** Only amend commits that haven't been pushed.

### Syncing with Main Branch

**Keep your feature branch updated with main:**

**Method 1: Merge (preserves history)**

```bash
git switch feature-login
git fetch origin
git merge origin/main
```

**Method 2: Rebase (clean history)**

```bash
git switch feature-login
git fetch origin
git rebase origin/main
```

**When to sync:**

- Before creating pull request
- When `main` has important changes
- Every few days on long-running branches

**Complete sync workflow:**

```bash
# Update local main
git switch main
git pull origin main

# Switch to feature
git switch feature-login

# Rebase onto main
git rebase main

# If conflicts, resolve them
git add .
git rebase --continue

# Force push (because rebase rewrites history)
git push --force-with-lease
```

**Daily professional workflow example:**

```bash
# Morning routine
git switch main
git pull origin main

# Create today's feature
git switch -c feature/add-email-validation

# Work...
git add validator.py
git commit -m "feat: Add email validation regex"

# More work...
git add test_validator.py
git commit -m "test: Add email validation tests"

# Before lunch, push
git push -u origin feature/add-email-validation

# After lunch, sync with main
git fetch origin
git rebase origin/main

# Finish work
git add .
git commit -m "feat: Integrate email validation into signup form"
git push

# Create pull request on GitHub

# After PR approved and merged
git switch main
git pull origin main
git branch -d feature/add-email-validation
```

---

## Common Mistakes & How to Fix Them

### Committed to Main Instead of Feature Branch

**Problem:**

```bash
# You're on main
git add .
git commit -m "Add feature"
# Oops! Should've been on a feature branch
```

**Fix:**

```bash
# Create feature branch from current position
git branch feature-login

# Reset main to before your commits
git reset --hard origin/main

# Switch to feature branch (your commits are safe here)
git switch feature-login
```

### Forgot to Pull Before Pushing

**Problem:**

```bash
git push
# Error: Updates were rejected because remote contains work
```

**Fix:**

```bash
# Pull with rebase
git pull --rebase origin main

# Or pull with merge
git pull origin main

# Resolve any conflicts
# Then push
git push
```

### Accidentally Deleted Local Changes

**Problem:**

```bash
git restore app.py
# Oh no! I needed those changes
```

**Fix (if not committed):**

Unfortunately, if changes were never committed or stashed, they're **permanently lost**.

**Prevention:** Commit often.

**If you used `git reset --hard` recently:**

```bash
# Check reflog
git reflog

# Find the commit before reset
git reset --hard HEAD@{1}
```

### Committed Secrets (API Keys, Passwords)

**Problem:**

```bash
git commit -m "Add config"
# Oops! .env file has API keys
```

**Fix (before pushing):**

```bash
# Remove file from last commit
git rm --cached .env
echo ".env" >> .gitignore
git add .gitignore
git commit --amend -m "Add config (excluding secrets)"
```

**Fix (after pushing):**

**Critical:** Secrets in Git history are **permanently exposed**.

1. **Rotate secrets immediately** (change API keys, passwords)
2. Remove from history (complex, requires force push):

```bash
# Use git filter-branch or BFG Repo Cleaner
# This is complex and rewrites history
# See: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository
```

**Prevention:**
- Always use `.gitignore`
- Never commit `.env` files
- Use environment variables
- Review `git diff --staged` before committing

### Pushed to Wrong Branch

**Problem:**

```bash
# Made changes on main instead of feature branch
git push origin main
# Oops!
```

**Fix:**

```bash
# Revert the commit on main
git revert HEAD
git push origin main

# Cherry-pick to feature branch
git switch feature-branch
git cherry-pick <commit-hash>
git push origin feature-branch
```

### Panic Recovery Tips

**General recovery strategy:**

1. **Don't panic** — Git is hard to truly break
2. **Check `git status`** — See current state
3. **Check `git log`** — See history
4. **Check `git reflog`** — See all recent actions

**The reflog is your safety net:**

```bash
# View recent Git actions
git reflog

# Output:
# a1b2c3d HEAD@{0}: commit: Add feature
# e4f5g6h HEAD@{1}: checkout: moving from main to feature
# i7j8k9l HEAD@{2}: reset: moving to HEAD~1

# Go back to any point
git reset --hard HEAD@{1}
```

**Emergency undo:**

```bash
# Undo last action
git reset --hard HEAD@{1}

# Undo multiple actions
git reset --hard HEAD@{3}
```

**Recover deleted branch:**

```bash
# Find last commit on deleted branch
git reflog

# Recreate branch
git branch recovered-branch <commit-hash>
```

**Create safety branch before dangerous operations:**

```bash
# Before resetting, rebasing, etc.
git branch backup-before-operation

# If something goes wrong:
git reset --hard backup-before-operation
```

---

## Git Cheat Sheet

### Most Used Commands

| Command | Description |
|---------|-------------|
| `git status` | Show working directory status |
| `git add <file>` | Stage file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit staged changes |
| `git push` | Push to remote |
| `git pull` | Pull from remote |
| `git log` | Show commit history |
| `git log --oneline` | Compact commit history |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |

### Branching

| Command | Description |
|---------|-------------|
| `git branch` | List branches |
| `git branch <name>` | Create branch |
| `git switch <name>` | Switch branch |
| `git switch -c <name>` | Create and switch branch |
| `git branch -d <name>` | Delete branch (safe) |
| `git branch -D <name>` | Delete branch (force) |
| `git merge <name>` | Merge branch into current |

### Remote Operations

| Command | Description |
|---------|-------------|
| `git clone <url>` | Clone repository |
| `git remote -v` | List remotes |
| `git fetch` | Download remote changes |
| `git pull` | Fetch and merge |
| `git push` | Upload commits |
| `git push -u origin <branch>` | Push and set upstream |

### Undoing Changes

| Command | Description |
|---------|-------------|
| `git restore <file>` | Discard unstaged changes |
| `git restore --staged <file>` | Unstage file |
| `git reset --soft HEAD~1` | Undo commit, keep changes staged |
| `git reset HEAD~1` | Undo commit, unstage changes |
| `git reset --hard HEAD~1` | Undo commit, discard changes |
| `git revert <commit>` | Create new commit undoing changes |

### Stashing

| Command | Description |
|---------|-------------|
| `git stash` | Stash changes |
| `git stash save "message"` | Stash with message |
| `git stash list` | List stashes |
| `git stash pop` | Apply and remove stash |
| `git stash apply` | Apply stash (keep in list) |
| `git stash drop` | Delete stash |

### Information

| Command | Description |
|---------|-------------|
| `git status` | Working directory status |
| `git log` | Commit history |
| `git log --oneline --graph` | Visual history |
| `git show <commit>` | Show commit details |
| `git diff` | Show changes |
| `git branch -v` | Show branches with last commit |
| `git reflog` | Show all Git actions |

### Configuration

| Command | Description |
|---------|-------------|
| `git config --global user.name "Name"` | Set username |
| `git config --global user.email "email"` | Set email |
| `git config --list` | View all config |

### Quick Reference Table

```
┌─────────────────────────────────────────────────┐
│           DAILY GIT WORKFLOW                    │
├─────────────────────────────────────────────────┤
│ Start:     git pull origin main                 │
│ Create:    git switch -c feature/name           │
│ Work:      (edit files)                         │
│ Check:     git status                           │
│ Stage:     git add .                            │
│ Commit:    git commit -m "message"              │
│ Push:      git push                             │
│ Review:    Create PR on GitHub                  │
│ Merge:     Merge PR after approval              │
│ Cleanup:   git branch -d feature/name           │
└─────────────────────────────────────────────────┘
```

---

## Learning & Growth

### How to Practice Git

**1. Create a practice repository:**

```bash
mkdir git-practice
cd git-practice
git init
```

**2. Practice exercises:**

**Exercise 1: Basic workflow**
```bash
echo "Hello" > file.txt
git add file.txt
git commit -m "Add file"
echo "World" >> file.txt
git add file.txt
git commit -m "Update file"
git log
```

**Exercise 2: Branching**
```bash
git switch -c feature
echo "Feature" > feature.txt
git add feature.txt
git commit -m "Add feature"
git switch main
git merge feature
```

**Exercise 3: Conflicts**
```bash
git switch -c branch1
echo "Branch 1" > conflict.txt
git add conflict.txt
git commit -m "Add conflict file"

git switch main
git switch -c branch2
echo "Branch 2" > conflict.txt
git add conflict.txt
git commit -m "Add different conflict file"

git switch main
git merge branch1
git merge branch2  # Conflict!
# Resolve it manually
git add conflict.txt
git commit -m "Resolve conflict"
```

**3. Online resources:**

- [Learn Git Branching](https://learngitbranching.js.org/) — Interactive visualizations
- [Oh My Git!](https://ohmygit.org/) — Card game to learn Git
- GitHub's Learning Lab
- GitKraken's Git tutorials

**4. Real projects:**

The best way to learn Git is by using it on real projects:
- Start a personal project
- Contribute to open source
- Build something with friends

### Recommended Habits

**Daily:**
- ✅ Commit frequently (multiple times per day)
- ✅ Write clear commit messages
- ✅ Pull before starting work
- ✅ Push at end of day

**Weekly:**
- ✅ Review your commit history: `git log --oneline`
- ✅ Clean up old branches
- ✅ Update `.gitignore` if needed

**Monthly:**
- ✅ Review your Git workflow
- ✅ Learn one new Git command/feature
- ✅ Read Git documentation

**Best practices to internalize:**

1. **Commit often:** Better to have many small commits than one large commit
2. **Branch for everything:** Never work directly on `main`
3. **Write meaningful messages:** Future you will thank present you
4. **Keep `main` clean:** Never push broken code to `main`
5. **Review before committing:** Use `git diff` to verify changes
6. **Pull regularly:** Stay in sync with team
7. **Don't fear mistakes:** Git has recovery mechanisms

### How Professionals Use Git Daily

**Morning routine:**

```bash
git switch main
git pull origin main
git switch -c feature/todays-task
```

**Throughout the day:**

```bash
# Small, frequent commits
git add specific-file.py
git commit -m "feat: Add specific function"

# Push often (backup + collaboration)
git push
```

**Before pull request:**

```bash
# Update with latest main
git fetch origin
git rebase origin/main

# Review all changes
git log origin/main..HEAD

# Push
git push --force-with-lease
```

**After PR merge:**

```bash
git switch main
git pull origin main
git branch -d feature/completed-task
```

**Professional Git habits:**

1. **Never commit to `main` directly**
2. **Always use feature branches**
3. **Write descriptive commit messages**
4. **Squash commits before merging (via GitHub PR)**
5. **Code review everything**
6. **Keep commits atomic**
7. **Rebase feature branches before merging**
8. **Delete branches after merge**

**What separates beginners from professionals:**

| Beginner | Professional |
|----------|--------------|
| `git commit -m "fixed"` | `git commit -m "fix: Resolve null pointer in login"` |
| Works on `main` | Always uses feature branches |
| Commits everything at once | Small, atomic commits |
| Ignores conflicts | Resolves conflicts cleanly |
| Doesn't push regularly | Pushes multiple times daily |
| Panics when things break | Uses `git reflog` and recovers |
| Never reviews changes | Always runs `git diff` before commit |

---

## Next Steps

Congratulations! You now have a comprehensive understanding of Git and GitHub.

**To solidify your knowledge:**

1. **Start using Git today**
   - Create a repository for any project you're working on
   - Practice the daily workflow

2. **Contribute to open source**
   - Find a project on GitHub
   - Fix a small issue
   - Submit a pull request

3. **Deep dive into specific topics**
   - Advanced rebasing
   - Git hooks
   - Submodules
   - Cherry-picking

4. **Read the official documentation**
   - [Git documentation](https://git-scm.com/doc)
   - [GitHub documentation](https://docs.github.com)

5. **Build good habits**
   - Commit often
   - Write good messages
   - Review before committing
   - Use branches for everything

**Remember:**

- Git is a skill that improves with practice
- Everyone makes mistakes (even experts)
- The Git community is helpful
- There's always more to learn

**Final advice:**

Start simple, practice consistently, and gradually incorporate more advanced features as you become comfortable. Git is one of the most valuable skills you'll develop as a developer.

Good luck, and happy coding!

---

## Additional Resources

**Official Documentation:**
- [Git Official Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Pro Git Book (Free)](https://git-scm.com/book/en/v2)

**Interactive Learning:**
- [Learn Git Branching](https://learngitbranching.js.org/)
- [GitHub Skills](https://skills.github.com/)

**Visualization Tools:**
- [Git Graph (VS Code Extension)](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
- [GitKraken](https://www.gitkraken.com/) — Git GUI client

**Community:**
- [Stack Overflow Git Tag](https://stackoverflow.com/questions/tagged/git)
- [r/git](https://reddit.com/r/git)

---

**Author's Note:** This guide was written to be your long-term reference. Bookmark it, refer back to it, and share it with others learning Git. Happy version controlling!
