Here’s a **start-to-end Git guide** with **commands, concepts, and real project workflow**.

---

# Git: Full Detailed Guide

## 1. What is Git?

**Git** is a **version control system**.

It helps you:

* track changes in code
* go back to old versions
* work safely without losing files
* collaborate with teams
* manage different features using branches

### Simple idea

Think of Git like a **time machine for your project**.

Without Git:

* you make changes
* something breaks
* you do not know what changed

With Git:

* every important change is saved as a **commit**
* you can compare, restore, branch, and merge

---

# 2. Git vs GitHub

Many beginners confuse these.

## Git

A tool installed on your computer.

## GitHub

A website/service where you store Git repositories online.

Also similar:

* GitLab
* Bitbucket

### Example

* **Git** = engine
* **GitHub** = garage/cloud storage

---

# 3. Basic Git Terms

## Repository (repo)

A project tracked by Git.

## Commit

A saved snapshot of your project.

## Branch

A separate line of development.

## Merge

Combining branches.

## Clone

Downloading a remote repo to your computer.

## Push

Uploading local commits to remote.

## Pull

Downloading updates from remote and applying them.

## Staging Area

A place where you prepare files before commit.

---

# 4. Git Installation

## Check if Git is installed

```bash
git --version
```

If installed, output may look like:

```bash
git version 2.x.x
```

## Configure Git for the first time

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Check config:

```bash
git config --list
```

---

# 5. How Git Works Internally

Git mainly has 3 areas:

## 1. Working Directory

Your normal project files.

## 2. Staging Area

Files prepared for commit.

## 3. Repository

Committed history.

### Flow

```text
Working Directory -> Staging Area -> Repository
```

### Commands involved

* modify file
* `git add` -> move to staging
* `git commit` -> save permanently

---

# 6. Starting a Git Project

## Option A: Create a new repository

```bash
mkdir my-project
cd my-project
git init
```

This creates a hidden `.git` folder.

## Option B: Clone an existing repository

```bash
git clone https://github.com/user/repo.git
cd repo
```

---

# 7. Your First Git Project

Let’s make a simple project.

## Create project

```bash
mkdir git-demo
cd git-demo
git init
```

## Create a file

```bash
echo "# Git Demo" > README.md
```

## Check status

```bash
git status
```

You may see:

```bash
Untracked files:
  README.md
```

### Meaning

Git sees the file, but it is not tracked yet.

## Add file to staging

```bash
git add README.md
```

## Commit it

```bash
git commit -m "Initial commit with README"
```

Now Git has saved your first snapshot.

---

# 8. `git status` — Most Important Command

This is one of the most used commands.

```bash
git status
```

It shows:

* current branch
* modified files
* staged files
* untracked files

Use it constantly.

---

# 9. Tracking Files

## Add one file

```bash
git add index.html
```

## Add multiple files

```bash
git add index.html style.css app.js
```

## Add all files

```bash
git add .
```

Be careful with `git add .` because it stages many files.

---

# 10. Commiting Changes

## Basic commit

```bash
git commit -m "Add homepage structure"
```

A good commit message should explain **what changed**.

### Good examples

```bash
git commit -m "Add login form validation"
git commit -m "Fix navbar mobile alignment"
git commit -m "Refactor product filtering logic"
```

### Bad example

```bash
git commit -m "update"
```

---

# 11. View Commit History

## Show history

```bash
git log
```

## Short version

```bash
git log --oneline
```

Example:

```bash
a1b2c3d Add login page
d4e5f6g Add CSS for navbar
h7i8j9k Initial commit
```

---

# 12. See File Changes

## Show unstaged changes

```bash
git diff
```

## Show staged changes

```bash
git diff --staged
```

This helps you see what exactly changed before committing.

---

# 13. Rename and Delete Files

## Rename file

```bash
git mv oldname.js newname.js
```

## Delete file

```bash
git rm file.txt
```

Then commit:

```bash
git commit -m "Rename utility file"
```

---

# 14. Ignore Files with `.gitignore`

Some files should not go to Git.

Examples:

* `node_modules/`
* `.env`
* build files
* logs
* temporary files

## Create `.gitignore`

```bash
touch .gitignore
```

Example content:

```gitignore
node_modules/
.env
dist/
*.log
```

Then add and commit:

```bash
git add .gitignore
git commit -m "Add gitignore"
```

---

# 15. Branching

Branches are one of Git’s strongest features.

## Why branches?

You can work on a new feature without touching the stable main code.

## See branches

```bash
git branch
```

## Create branch

```bash
git branch feature-login
```

## Switch branch

```bash
git checkout feature-login
```

## Create and switch at once

```bash
git checkout -b feature-login
```

Modern Git also supports:

```bash
git switch -c feature-login
```

---

# 16. Real Branch Example

Suppose your main project has:

* homepage
* navbar
* footer

Now you want login feature.

## Create branch

```bash
git checkout -b feature-login
```

## Make files

```bash
touch login.html login.css login.js
git add .
git commit -m "Add initial login page files"
```

## More changes

```bash
git add .
git commit -m "Implement login validation"
```

Now your `main` branch is still clean.

---

# 17. Merge Branches

After feature is ready, merge it into main.

## Go to main

```bash
git checkout main
```

## Merge

```bash
git merge feature-login
```

If there are no conflicts, Git combines changes automatically.

---

# 18. Merge Conflicts

A conflict happens when two branches change the same part of a file.

Example conflict markers:

```txt
<<<<<<< HEAD
color: blue;
=======
color: red;
>>>>>>> feature-login
```

### How to fix

1. Open file
2. Decide final code
3. Remove conflict markers
4. Save file
5. Stage and commit

```bash
git add style.css
git commit -m "Resolve merge conflict in style"
```

---

# 19. `git checkout`, `git switch`, `git restore`

These are related but different.

## Switch branch

```bash
git switch main
```

## Create and switch branch

```bash
git switch -c feature-cart
```

## Restore file to last commit

```bash
git restore app.js
```

## Unstage file

```bash
git restore --staged app.js
```

Older Git often used:

```bash
git checkout main
```

---

# 20. Undoing Changes

Very important for real work.

## Undo unstaged changes

```bash
git restore file.txt
```

## Unstage a staged file

```bash
git restore --staged file.txt
```

## Amend last commit

```bash
git commit --amend -m "Better commit message"
```

## Reset commit but keep changes

```bash
git reset --soft HEAD~1
```

## Reset commit and unstage changes

```bash
git reset --mixed HEAD~1
```

## Reset commit and delete changes

```bash
git reset --hard HEAD~1
```

Be careful with:

```bash
git reset --hard
```

It can permanently remove uncommitted work.

---

# 21. Git Stash

Sometimes you are working, but suddenly need to switch tasks.

## Save unfinished work temporarily

```bash
git stash
```

## See stash list

```bash
git stash list
```

## Restore last stash

```bash
git stash pop
```

## Restore without deleting from stash list

```bash
git stash apply
```

Example:

```bash
git stash
git switch main
# fix urgent bug
git switch feature-login
git stash pop
```

---

# 22. Remote Repositories

A remote repo is an online version of your project.

## Add remote

```bash
git remote add origin https://github.com/user/repo.git
```

## See remotes

```bash
git remote -v
```

---

# 23. Push Code to GitHub

After linking remote:

## Push first time

```bash
git push -u origin main
```

`-u` sets upstream, so later you can just use:

```bash
git push
```

---

# 24. Pull and Fetch

## Pull

Downloads remote changes and merges them:

```bash
git pull
```

## Fetch

Downloads remote changes but does not merge:

```bash
git fetch
```

Then you can inspect before merging.

---

# 25. Clone a Repository

```bash
git clone https://github.com/user/project.git
```

This downloads the entire project with history.

---

# 26. Rebase

Rebase is another way to integrate changes.

## Merge vs Rebase

### Merge

Creates a merge commit.

### Rebase

Replays commits on top of another branch for cleaner history.

Example:

```bash
git checkout feature-login
git rebase main
```

Then later:

```bash
git checkout main
git merge feature-login
```

### Important

Do not casually rebase public shared commits unless you understand the effect.

---

# 27. Tags

Tags mark important versions, like releases.

## Create tag

```bash
git tag v1.0
```

## Push tags

```bash
git push origin v1.0
```

## Push all tags

```bash
git push --tags
```

---

# 28. GitHub Pull Request Workflow

In team projects:

1. create branch
2. make changes
3. commit
4. push branch
5. open Pull Request on GitHub
6. review
7. merge into main

Commands:

```bash
git checkout -b feature-payment
git add .
git commit -m "Add payment integration UI"
git push -u origin feature-payment
```

Then create PR on GitHub.

---

# 29. Real Project Implementation 1: Static Website

Let’s do a real mini workflow.

## Project structure

```text
portfolio-site/
  index.html
  style.css
  script.js
  .gitignore
```

## Start

```bash
mkdir portfolio-site
cd portfolio-site
git init
touch index.html style.css script.js
```

## Initial code

```bash
git add .
git commit -m "Initial project setup"
```

## Add homepage

Edit `index.html`, `style.css`

```bash
git add .
git commit -m "Build homepage hero section"
```

## Add navbar in new branch

```bash
git checkout -b feature-navbar
```

Edit files.

```bash
git add .
git commit -m "Add responsive navbar"
```

## Add contact section

```bash
git add .
git commit -m "Add contact section"
```

## Merge into main

```bash
git checkout main
git merge feature-navbar
```

## Connect to GitHub

```bash
git remote add origin https://github.com/username/portfolio-site.git
git push -u origin main
```

This is a real beginner workflow.

---

# 30. Real Project Implementation 2: Node.js App

## Create project

```bash
mkdir task-api
cd task-api
git init
npm init -y
```

## Install packages

```bash
npm install express
npm install -D nodemon
```

## Add `.gitignore`

```gitignore
node_modules/
.env
```

## Stage and commit

```bash
git add .
git commit -m "Initialize Node.js Express project"
```

## Create feature branch

```bash
git checkout -b feature-routes
```

Create files:

* `server.js`
* `routes/tasks.js`

Commit:

```bash
git add .
git commit -m "Add task routes"
```

## Add middleware

```bash
git add .
git commit -m "Add JSON middleware and error handler"
```

## Merge feature

```bash
git checkout main
git merge feature-routes
```

## Push to GitHub

```bash
git remote add origin https://github.com/username/task-api.git
git push -u origin main
```

---

# 31. Real Project Implementation 3: Team Workflow

Suppose 3 developers work on an e-commerce app.

## Branch strategy

* `main` = production-ready
* `develop` = integration branch
* `feature/cart`
* `feature/auth`
* `bugfix/navbar`

## Example flow

### Create develop branch

```bash
git checkout -b develop
git push -u origin develop
```

### Developer A

```bash
git checkout -b feature/auth develop
```

Work, then:

```bash
git add .
git commit -m "Implement login form UI"
git push -u origin feature/auth
```

### Developer B

```bash
git checkout -b feature/cart develop
git add .
git commit -m "Add cart state management"
git push -u origin feature/cart
```

Then each opens pull request into `develop`.

After testing:

* merge `develop` into `main`

---

# 32. Useful Git Commands Table

## Basic commands

```bash
git init
git clone <url>
git status
git add <file>
git add .
git commit -m "message"
git log
git diff
```

## Branch commands

```bash
git branch
git branch <name>
git checkout <branch>
git checkout -b <name>
git switch <branch>
git switch -c <name>
git merge <branch>
```

## Remote commands

```bash
git remote -v
git remote add origin <url>
git push
git pull
git fetch
```

## Undo commands

```bash
git restore <file>
git restore --staged <file>
git reset --soft HEAD~1
git reset --hard HEAD~1
git commit --amend
git stash
git stash pop
```

---

# 33. Best Commit Message Style

A strong commit message is:

* clear
* short
* action-based

Examples:

```bash
git commit -m "Add user registration page"
git commit -m "Fix product filter bug"
git commit -m "Refactor payment validation logic"
```

---

# 34. Common Beginner Mistakes

## 1. Forgetting `.gitignore`

Then `node_modules` or secret files get committed.

## 2. Using `git add .` blindly

You may stage unwanted files.

## 3. Writing bad commit messages

Like:

```bash
git commit -m "done"
```

## 4. Working directly on `main`

Better to use feature branches.

## 5. Using `git reset --hard` carelessly

Can delete work permanently.

## 6. Pulling without understanding conflicts

Always check `git status` and `git diff`.

---

# 35. Recommended Workflow for Personal Projects

For your own project:

```text
main
 ├── feature-ui
 ├── feature-auth
 ├── feature-api
 └── bugfix-navbar
```

Flow:

1. create branch from main
2. work on one feature
3. commit regularly
4. merge when finished

Commands:

```bash
git checkout main
git pull
git checkout -b feature-auth
# work
git add .
git commit -m "Add login form"
git commit -m "Add password validation"
git checkout main
git merge feature-auth
git push
```

---

# 36. Recommended Workflow for Deployment Projects

Example:

* `main` = live production
* `develop` = testing area
* feature branches = new work

This is common in real companies.

---

# 37. Git File Lifecycle

A file in Git usually goes through:

1. **Untracked**
2. **Tracked**
3. **Modified**
4. **Staged**
5. **Committed**

Example:

```bash
touch app.js
git status           # untracked
git add app.js       # staged/tracked
git commit -m "Add app file"
# edit app.js
git status           # modified
git add app.js
git commit -m "Update app logic"
```

---

# 38. Viewing Specific Commits

## Show one commit

```bash
git show <commit-id>
```

Example:

```bash
git show a1b2c3d
```

---

# 39. Remove a File from Git but Keep Locally

```bash
git rm --cached .env
git commit -m "Stop tracking env file"
```

Useful if you accidentally committed a sensitive file.

---

# 40. Revert a Commit Safely

If a bad commit is already pushed, safer than reset is:

```bash
git revert <commit-id>
```

This creates a new commit that undoes the bad one.

---

# 41. Cherry-pick

Take one specific commit from another branch.

```bash
git cherry-pick <commit-id>
```

Useful when you want only one fix, not full branch merge.

---

# 42. Example: Daily Real Project Git Usage

Suppose you are building a full-stack app.

## Morning

```bash
git pull
git switch -c feature-profile-page
```

## Work and save

```bash
git add .
git commit -m "Create profile page layout"
```

## More progress

```bash
git add .
git commit -m "Add profile image upload logic"
```

## Push

```bash
git push -u origin feature-profile-page
```

## After review

```bash
git switch main
git pull
git merge feature-profile-page
git push
```

That is very close to real development.

---

# 43. Real Mini Project Example with Actual Files

Let’s imagine a simple to-do app.

## Files

```text
todo-app/
  index.html
  style.css
  app.js
  .gitignore
```

## Step 1: initialize

```bash
mkdir todo-app
cd todo-app
git init
touch index.html style.css app.js .gitignore
```

## Step 2: first commit

```bash
git add .
git commit -m "Initialize todo app structure"
```

## Step 3: feature branch

```bash
git switch -c feature-add-task
```

### Add code in `app.js`

```js
const tasks = [];

function addTask(task) {
  tasks.push(task);
  console.log("Task added:", task);
}

addTask("Learn Git");
```

Commit:

```bash
git add app.js
git commit -m "Add task creation logic"
```

## Step 4: another branch for delete feature

```bash
git switch main
git switch -c feature-delete-task
```

Code:

```js
const tasks = ["Learn Git", "Build app"];

function deleteTask(index) {
  tasks.splice(index, 1);
  console.log(tasks);
}

deleteTask(0);
```

Commit:

```bash
git add app.js
git commit -m "Add task deletion logic"
```

Now two branches changed same file differently. Merge may create conflict. This is a good real example of why Git matters.

---

# 44. How to Solve Conflict in Real Project

Suppose conflict in `app.js`.

Final merged code may become:

```js
const tasks = [];

function addTask(task) {
  tasks.push(task);
  console.log("Task added:", task);
}

function deleteTask(index) {
  tasks.splice(index, 1);
  console.log("Task deleted");
}
```

Then:

```bash
git add app.js
git commit -m "Merge add and delete task features"
```

---

# 45. Essential Professional Commands

```bash
git status
git log --oneline --graph --all
git diff
git stash
git branch
git switch
git merge
git rebase
git fetch
git pull
git push
git revert
```

A very useful history command:

```bash
git log --oneline --graph --decorate --all
```

It shows branch structure visually.

---

# 46. Beginner-to-Advanced Learning Order

You should learn Git in this order:

## Level 1

* `git init`
* `git status`
* `git add`
* `git commit`
* `git log`

## Level 2

* `.gitignore`
* `git diff`
* branches
* `git merge`

## Level 3

* remote repo
* `git clone`
* `git push`
* `git pull`
* GitHub workflow

## Level 4

* `git stash`
* `git reset`
* `git revert`
* `git rebase`
* `git cherry-pick`

---

# 47. Best Practice Rules

1. commit often
2. write meaningful commit messages
3. create a branch per feature
4. do not commit secrets
5. use `.gitignore`
6. pull latest changes before starting
7. check `git status` often
8. review code with `git diff` before commit
9. use `revert` for already pushed bad commits
10. avoid force push unless you know exactly why

---

# 48. Full Git Workflow Cheat Sheet

## New project

```bash
git init
git add .
git commit -m "Initial commit"
```

## Connect GitHub

```bash
git remote add origin <repo-url>
git push -u origin main
```

## New feature

```bash
git switch -c feature-login
git add .
git commit -m "Add login page"
git push -u origin feature-login
```

## Merge feature

```bash
git switch main
git merge feature-login
git push
```

## Update local repo

```bash
git pull
```

## Save unfinished work

```bash
git stash
git stash pop
```

## Undo unstaged changes

```bash
git restore file.txt
```

## Undo last commit but keep changes

```bash
git reset --soft HEAD~1
```

---

# 49. One Complete End-to-End Example

Let’s do the full flow in order.

## Create app

```bash
mkdir shop-app
cd shop-app
git init
touch index.html style.css app.js .gitignore
```

## First commit

```bash
git add .
git commit -m "Initialize shop app"
```

## Add remote

```bash
git remote add origin https://github.com/username/shop-app.git
git push -u origin main
```

## Start feature

```bash
git switch -c feature-product-list
```

Edit files, then:

```bash
git add .
git commit -m "Add product list section"
git push -u origin feature-product-list
```

## Start another feature later

```bash
git switch main
git pull
git switch -c feature-cart
```

Work:

```bash
git add .
git commit -m "Add cart UI"
git push -u origin feature-cart
```

## Merge first feature

```bash
git switch main
git merge feature-product-list
git push
```

## Merge second feature

```bash
git merge feature-cart
git push
```

This is real project Git usage from start to finish.

---

# 50. Final Summary

Git helps you:

* track code changes
* work with confidence
* collaborate with others
* manage features using branches
* recover from mistakes

The most important beginner commands are:

```bash
git init
git status
git add .
git commit -m "message"
git log --oneline
git branch
git switch -c feature-name
git merge feature-name
git remote add origin <url>
git push -u origin main
git pull
```

---

# 51. Practice Project for You

To master Git, build this:

## Project idea

A simple **portfolio website** or **todo app**

Practice this exact flow:

1. initialize repo
2. first commit
3. create `feature-navbar`
4. commit navbar
5. create `feature-contact`
6. commit contact section
7. merge both to main
8. push to GitHub
9. create a conflict intentionally and solve it
10. use stash once
11. use revert once

That will teach you a lot.

If you want, I can next give you a **Git commands handbook in table form** or a **full real project with Git + GitHub workflow step by step**.
