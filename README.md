# Git Training Repository

This repository is designed to help you learn essential Git workflows. Follow this guide to practice common Git operations including pulling repositories, creating branches, making changes, and creating pull requests.

## Prerequisites

- Git installed on your machine
- A GitHub account
- Basic familiarity with command line

## Table of Contents

1. [Setting Up the Repository](#setting-up-the-repository)
2. [Forking the Repository (For Non-Owners)](#forking-the-repository-for-non-owners)
3. [Checking Your Current Branch](#checking-your-current-branch)
4. [Creating a New Branch](#creating-a-new-branch)
5. [Making Code Changes](#making-code-changes)
6. [Committing Changes](#committing-changes)
7. [Pushing Changes to GitHub](#pushing-changes-to-github)
8. [Creating a Pull Request](#creating-a-pull-request)
9. [Useful Git Commands](#useful-git-commands)

## Setting Up the Repository

### Option A: If You Own the Repository

If you are the owner of the repository, you can clone it directly:

```bash
git clone https://github.com/beachpeeps/cpg_sandbox.git
cd cpg_sandbox
```

### Option B: If You Don't Own the Repository (Recommended for Contributors)

If you want to contribute to someone else's repository, you should fork it first.

## Forking the Repository (For Non-Owners)

### What is a Fork?

A **fork** is your own copy of someone else's repository. It allows you to:
- Make changes without affecting the original repository
- Contribute back to the original project through pull requests
- Keep your own version of the project

### 1. Fork the Repository on GitHub

1. Navigate to the repository you want to contribute to on GitHub
2. Click the "Fork" button in the top-right corner
3. Choose where to fork it (usually your personal account)
4. GitHub will create a copy of the repository under your account

### 2. Clone Your Fork

After forking, clone **your fork** (not the original repository):

```bash
# Clone YOUR fork (replace 'your-username' with your actual GitHub username)
git clone https://github.com/your-username/cpg_sandbox.git
cd cpg_sandbox
```

### 3. Add the Original Repository as Upstream

To keep your fork synchronized with the original repository, add it as an "upstream" remote:

```bash
# Add the original repository as upstream
git remote add upstream https://github.com/beachpeeps/cpg_sandbox.git

# Verify your remotes
git remote -v
```

You should see output like:
```
origin    https://github.com/your-username/cpg_sandbox.git (fetch)
origin    https://github.com/your-username/cpg_sandbox.git (push)
upstream  https://github.com/beachpeeps/cpg_sandbox.git (fetch)
upstream  https://github.com/beachpeeps/cpg_sandbox.git (push)
```

### 4. Pull Latest Changes

Always ensure you have the latest changes from the original repository:

```bash
# Fetch changes from the original repository
git fetch upstream

# Switch to main branch
git checkout main

# Merge the latest changes from upstream
git merge upstream/main

# Push the updated main branch to your fork
git push origin main
```

## Checking Your Current Branch

It's important to know which branch you're currently working on. Use these commands:

```bash
# Show current branch name
git branch

# Show current branch with more details
git status

# Show all branches (local and remote)
git branch -a
```

The current branch will be highlighted with an asterisk (*) when using `git branch`.

## Understanding Branches

### What is a Git Branch?

A **branch** in Git is essentially a lightweight, movable pointer to a specific commit in your project's history. Think of it as an independent line of development where you can make changes without affecting the main codebase.

#### Key Concepts:

- **Main/Master Branch**: The primary branch of your repository (usually called `main` or `master`)
- **Feature Branch**: A separate branch created to work on a specific feature or fix
- **Branch Isolation**: Changes made on one branch don't affect other branches until you merge them
- **Branch History**: Each branch maintains its own commit history

#### Why Use Branches?

1. **Safe Development**: Work on new features without breaking the main code
2. **Collaboration**: Multiple people can work on different features simultaneously
3. **Code Review**: Changes can be reviewed before being merged into main
4. **Experimentation**: Try different approaches without fear of losing working code
5. **Rollback**: Easy to switch back to previous versions if needed

#### Visual Example:

```
main:     A---B---C---D
                \
feature:         E---F---G
```

In this example:
- `main` branch has commits A, B, C, D
- `feature` branch was created from commit B and has additional commits E, F, G
- The branches can be merged later to combine the changes

## Creating a New Branch

### 1. Create and Switch to a New Branch

```bash
# Create a new branch and switch to it
git checkout -b feature/your-feature-name

# Alternative method (Git 2.23+)
git switch -c feature/your-feature-name
```

### 2. Choose a Descriptive Branch Name

Good branch names help you and your team understand what work is being done. Here are some common naming conventions:

#### Branch Naming Patterns:

```bash
# Feature branches
feature/add-user-authentication
feature/implement-search-functionality
feature/create-dashboard-ui

# Bug fix branches
bugfix/fix-login-error
bugfix/resolve-memory-leak
bugfix/correct-typo-in-readme

# Hotfix branches (urgent fixes for production)
hotfix/fix-critical-security-issue
hotfix/resolve-payment-processing-bug

# Other common patterns
chore/update-dependencies
docs/add-api-documentation
refactor/improve-code-structure
test/add-unit-tests
```

#### Naming Best Practices:

- **Use lowercase letters** and hyphens (`-`) instead of spaces
- **Be descriptive** but concise (aim for 3-5 words)
- **Use prefixes** to categorize the type of work (`feature/`, `bugfix/`, etc.)
- **Include the issue number** if working on a specific ticket: `feature/123-add-login-form`
- **Avoid special characters** like `@`, `#`, `%`, `^`, `&`, `*`, `(`, `)`, `[`, `]`, `{`, `}`, `\`, `|`, `;`, `:`, `"`, `'`, `<`, `>`, `,`, `.`, `?`, `/`, `~`, `` ` ``, `!`

#### Examples for This Training:

```bash
# Good examples
feature/add-hello-world-script
feature/create-calculator-functions
bugfix/fix-typo-in-comments
docs/update-readme-instructions

# Avoid these
new-stuff
changes
test
my-branch
```

### 3. Verify You're on the New Branch

```bash
git branch
```

You should see your new branch highlighted with an asterisk.

## Making Code Changes

### Example: Create a Simple Python Script

Let's create a simple Python script as an example:

```bash
# Create a new Python file
touch hello_world.py
```

Add the following content to `hello_world.py`:

```python
#!/usr/bin/env python3
"""
A simple hello world script for Git training.
"""

def main():
    print("Hello, Git World!")
    print("This is a training exercise.")

if __name__ == "__main__":
    main()
```

### Example: Create a JavaScript File

```bash
# Create a new JavaScript file
touch calculator.js
```

Add the following content to `calculator.js`:

```javascript
// Simple calculator for Git training
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

function multiply(a, b) {
    return a * b;
}

function divide(a, b) {
    if (b === 0) {
        throw new Error("Division by zero is not allowed");
    }
    return a / b;
}

// Example usage
console.log("Calculator functions loaded!");
console.log("2 + 3 =", add(2, 3));
console.log("10 - 4 =", subtract(10, 4));
```

## Committing Changes

### 1. Check What Files Have Changed

```bash
# See which files have been modified
git status

# See the actual changes made
git diff
```

### 2. Stage Your Changes

```bash
# Stage specific files
git add hello_world.py
git add calculator.js

# Or stage all changes
git add .
```

### 3. Commit Your Changes

```bash
# Commit with a descriptive message
git commit -m "Add hello world Python script and calculator JavaScript functions"
```

### 4. Verify Your Commit

```bash
# See your commit history
git log --oneline

# See the last commit details
git show
```

## Pushing Changes to GitHub

### 1. Push Your Branch to GitHub

```bash
# Push your branch to the remote repository
git push origin feature/your-feature-name
```

If this is the first time pushing this branch, Git will provide a command to set the upstream:

```bash
git push --set-upstream origin feature/your-feature-name
```

### 2. Verify the Push

```bash
# Check the status
git status

# See all branches including remote
git branch -a
```

## Creating a Pull Request

### 1. Navigate to GitHub

#### If You Own the Repository:
1. Go to your repository on GitHub
2. You should see a banner suggesting to create a pull request for your recently pushed branch
3. Click "Compare & pull request"

#### If You Forked the Repository:
1. Go to **your fork** on GitHub (not the original repository)
2. You should see a banner suggesting to create a pull request for your recently pushed branch
3. Click "Compare & pull request"
4. **Important**: Make sure the pull request is targeting the **original repository**, not your fork
   - The "base repository" should be the original repository
   - The "head repository" should be your fork

### 2. Fill Out the Pull Request

- **Title**: Use a clear, descriptive title (e.g., "Add hello world script and calculator functions")
- **Description**: Explain what changes you made and why
- **Reviewers**: Assign reviewers if needed (only available if you have permissions)
- **Labels**: Add appropriate labels (only available if you have permissions)

### 3. Submit the Pull Request

Click "Create pull request" to submit your changes for review.

### 4. After Creating the Pull Request

- The original repository maintainers will review your changes
- They may request changes or ask questions
- Once approved, they will merge your pull request
- Your changes will then be part of the original repository

## Useful Git Commands

### Branch Management

```bash
# List all branches
git branch -a

# Switch to an existing branch
git checkout branch-name
# or
git switch branch-name

# Delete a local branch
git branch -d branch-name

# Delete a remote branch
git push origin --delete branch-name
```

### Checking Status and History

```bash
# Check current status
git status

# See commit history
git log --oneline

# See changes in working directory
git diff

# See staged changes
git diff --cached
```

### Undoing Changes

```bash
# Unstage a file
git reset HEAD filename

# Discard changes to a file
git checkout -- filename

# Undo the last commit (keep changes)
git reset --soft HEAD~1

# Undo the last commit (discard changes)
git reset --hard HEAD~1
```

### Remote Operations

```bash
# Fetch latest changes without merging
git fetch origin

# Pull and merge latest changes
git pull origin main

# See remote repositories
git remote -v
```

## Best Practices

1. **Always pull before starting work**: `git pull origin main`
2. **Use descriptive branch names**: `feature/add-login`, `bugfix/fix-header-styling`
3. **Write clear commit messages**: Use imperative mood ("Add feature" not "Added feature")
4. **Make small, focused commits**: Each commit should represent one logical change
5. **Review your changes**: Use `git diff` before committing
6. **Keep your branch up to date**: Regularly pull from main and merge/rebase

## Common Workflow Summary

### For Repository Owners:

```bash
# 1. Start from main branch
git checkout main
git pull origin main

# 2. Create and switch to new branch
git checkout -b feature/my-new-feature

# 3. Make your changes
# (edit files, add new files, etc.)

# 4. Check what you've changed
git status
git diff

# 5. Stage and commit changes
git add .
git commit -m "Descriptive commit message"

# 6. Push to GitHub
git push origin feature/my-new-feature

# 7. Create pull request on GitHub
# (Navigate to GitHub and use the web interface)
```

### For Contributors (Fork Workflow):

```bash
# 1. Fork the repository on GitHub first, then:

# 2. Clone your fork
git clone https://github.com/your-username/cpg_sandbox.git
cd cpg_sandbox

# 3. Add upstream remote
git remote add upstream https://github.com/beachpeeps/cpg_sandbox.git

# 4. Start from main branch and sync with upstream
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# 5. Create and switch to new branch
git checkout -b feature/my-new-feature

# 6. Make your changes
# (edit files, add new files, etc.)

# 7. Check what you've changed
git status
git diff

# 8. Stage and commit changes
git add .
git commit -m "Descriptive commit message"

# 9. Push to your fork
git push origin feature/my-new-feature

# 10. Create pull request on GitHub
# (Navigate to your fork on GitHub and create PR to original repository)
```

## Troubleshooting

### If you're on the wrong branch:
```bash
git checkout correct-branch-name
```

### If you have uncommitted changes and need to switch branches:
```bash
# Stash your changes
git stash

# Switch branches
git checkout other-branch

# Apply your stashed changes later
git stash pop
```

### If you need to update your branch with latest main:
```bash
git checkout main
git pull origin main
git checkout your-feature-branch
git merge main
```

### If you're working with a fork and need to sync with upstream:
```bash
# Fetch latest changes from the original repository
git fetch upstream

# Switch to main branch
git checkout main

# Merge upstream changes
git merge upstream/main

# Push updated main to your fork
git push origin main

# Switch back to your feature branch
git checkout your-feature-branch

# Merge the updated main into your feature branch
git merge main
```

### If you accidentally cloned the original repository instead of your fork:
```bash
# Add your fork as origin
git remote add origin https://github.com/your-username/cpg_sandbox.git

# Add the original as upstream
git remote add upstream https://github.com/beachpeeps/cpg_sandbox.git

# Verify your remotes
git remote -v
```

### If your pull request is targeting the wrong repository:
1. Go to your pull request on GitHub
2. Click "Edit" next to the title
3. Make sure the "base repository" is the original repository
4. Make sure the "head repository" is your fork

Happy coding and Git learning! 🚀
