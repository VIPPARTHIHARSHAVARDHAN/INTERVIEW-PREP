# Git & GitHub Important Interview Questions

> Placement-focused Git and GitHub interview questions with **simple, interview-ready answers**. This file covers the important concepts, differences, commands, and practical scenarios commonly expected from freshers.

---

# 1. What is Git?

### Answer

Git is a **distributed version control system** used to track changes in source code and collaborate with other developers.

It allows developers to:

- Track changes
- Create branches
- Merge code
- Maintain project history
- Revert changes
- Work with other developers

### Interview Answer

> "Git is a distributed version control system used to track code changes and manage different versions of a project."

---

# 2. What is GitHub?

### Answer

GitHub is a platform used to **host Git repositories** and provide collaboration features.

It provides features such as:

- Remote repositories
- Pull Requests
- Code reviews
- Issues
- Project collaboration
- Repository management

### Interview Answer

> "GitHub is a platform that hosts Git repositories and provides collaboration features such as Pull Requests and code reviews."

---

# 3. Git vs GitHub?

### Answer

| Git | GitHub |
|---|---|
| Version control system | Hosting and collaboration platform |
| Works locally | Primarily provides remote hosting/services |
| Tracks code changes | Hosts repositories |
| Can work without GitHub | Commonly works with Git |
| Command-line tool | Web platform |

### Easy Answer

> "Git manages version history, while GitHub provides a platform to host Git repositories and collaborate."

---

# 4. What is Version Control?

### Answer

Version control is a system used to track changes to files over time.

It allows developers to:

```text
Track changes
View history
Restore previous versions
Work on different features
Collaborate with developers
```

---

# 5. What is a Git Repository?

### Answer

A Git repository is a project directory containing files along with Git's version history and metadata.

A repository can exist:

```text
Locally → On your computer

Remotely → On a platform such as GitHub
```

---

# 6. What is the difference between a local and remote repository?

### Answer

```text
Local Repository
→ Exists on your computer.

Remote Repository
→ Exists on a remote hosting service.
```

Typical workflow:

```text
Local Changes
      ↓
Commit
      ↓
Push
      ↓
Remote Repository
```

---

# 7. What is the Git working directory?

### Answer

The working directory is the folder containing the files you are currently working on.

Example:

```text
project/
├── app.py
├── README.md
└── config.py
```

These files are part of your working directory.

---

# 8. What is the staging area?

### Answer

The staging area is an intermediate area where you select changes that should be included in the next commit.

```text
Working Directory
       ↓
    git add
       ↓
Staging Area
       ↓
   git commit
       ↓
Local Repository
```

---

# 9. What is a commit?

### Answer

A commit is a recorded snapshot of staged changes in the local repository.

Example:

```bash
git commit -m "Add login feature"
```

A commit creates a point in Git history that can later be inspected or used as a reference.

---

# 10. Explain the basic Git workflow.

### Answer

The basic workflow is:

```text
Create / Modify Files
        ↓
    git status
        ↓
      git add
        ↓
    git commit
        ↓
     git push
        ↓
Remote Repository
```

For an existing project, you may first use:

```bash
git pull
```

to bring remote changes into your local branch.

---

# 11. What does `git init` do?

### Answer

`git init` initializes a new Git repository in the current directory.

```bash
git init
```

It creates a `.git` directory containing Git repository metadata.

---

# 12. What does `git clone` do?

### Answer

`git clone` creates a local copy of an existing remote repository.

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

---

# 13. What does `git status` do?

### Answer

`git status` shows the current state of the working directory and staging area.

```bash
git status
```

It can show:

```text
Modified files
Untracked files
Staged changes
Current branch
```

---

# 14. What does `git add` do?

### Answer

`git add` stages changes for the next commit.

### One file

```bash
git add app.py
```

### Multiple files

```bash
git add app.py README.md
```

### All changes under the current directory

```bash
git add .
```

---

# 15. What does `git commit` do?

### Answer

`git commit` records staged changes in the local repository.

```bash
git commit -m "Add user authentication"
```

Important:

```text
git add
→ Stages changes

git commit
→ Records staged changes locally

git push
→ Sends commits to remote
```

---

# 16. What does `git push` do?

### Answer

`git push` sends local commits to a remote repository.

```bash
git push
```

For the first push of a new branch:

```bash
git push -u origin main
```

or:

```bash
git push -u origin feature-login
```

---

# 17. What does `git pull` do?

### Answer

`git pull` fetches changes from a remote repository and integrates them into the current branch.

A simplified view is:

```text
git pull
   ↓
git fetch
   +
integration
```

The integration may be a merge or rebase depending on configuration/options.

---

# 18. What does `git fetch` do?

### Answer

`git fetch` downloads changes and references from a remote repository without automatically integrating those changes into your current branch.

```bash
git fetch
```

It is useful when you want to inspect remote changes before integrating them.

---

# 19. `git pull` vs `git fetch`

### Answer

| `git pull` | `git fetch` |
|---|---|
| Downloads remote changes | Downloads remote changes |
| Integrates them into current branch | Does not automatically integrate them |
| More convenient | Gives more control |

### Interview Answer

> "`git fetch` downloads remote changes without integrating them, while `git pull` fetches and integrates them into the current branch."

---

# 20. What is a Git branch?

### Answer

A branch is an independent line of development in a Git repository.

Example:

```text
main
 │
 ├── feature-login
 │
 └── feature-payment
```

Branches allow developers to work on features without directly changing the main branch.

---

# 21. Why are branches used?

### Answer

Branches are used to:

```text
Develop features separately
Fix bugs
Test changes
Work with multiple developers
Keep main code stable
```

---

# 22. How do you create a branch?

### Answer

```bash
git branch feature-login
```

This creates a branch but does not switch to it.

Modern approach to create and switch:

```bash
git switch -c feature-login
```

---

# 23. How do you switch branches?

### Answer

Modern command:

```bash
git switch feature-login
```

Older commonly used command:

```bash
git checkout feature-login
```

---

# 24. How do you list branches?

### Answer

Local branches:

```bash
git branch
```

Remote branches:

```bash
git branch -r
```

All branches:

```bash
git branch -a
```

---

# 25. What is `main`?

### Answer

`main` is a commonly used name for the primary branch of a repository.

It is not a requirement that every repository use `main`.

---

# 26. What is `origin`?

### Answer

`origin` is the conventional default name for the remote repository created when a repository is cloned.

Example:

```text
origin → Remote repository
```

Check it using:

```bash
git remote -v
```

---

# 27. What is `HEAD`?

### Answer

`HEAD` is a reference to the currently checked-out commit, normally through the current branch.

Example:

```text
HEAD
 ↓
main
 ↓
latest commit
```

---

# 28. What is `.git`?

### Answer

`.git` is the hidden directory created when Git initializes a repository.

It contains Git's repository metadata, including:

```text
Commit information
Branch references
Configuration
Repository objects
Other Git metadata
```

---

# 29. What is `.gitignore`?

### Answer

`.gitignore` specifies files and directories that Git should normally ignore as untracked files.

Example:

```gitignore
.env
__pycache__/
*.log
node_modules/
```

Common things to ignore:

```text
Secrets
Environment files
Temporary files
Logs
Generated files
Dependencies
Build files
```

---

# 30. Does `.gitignore` remove an already tracked file?

### Answer

No.

If a file is already tracked, adding it to `.gitignore` does not automatically stop tracking it.

To stop tracking it while keeping the file locally:

```bash
git rm --cached .env
```

Then commit the change.

---

# 31. Why should `.env` usually be added to `.gitignore`?

### Answer

`.env` files can contain sensitive information such as:

```text
API keys
Passwords
Access tokens
Database credentials
Secret configuration
```

These should generally not be committed to a public repository.

A safer approach is to provide:

```text
.env.example
```

containing placeholder values.

---

# 32. What is a Pull Request?

### Answer

A Pull Request (PR) is a request to merge changes from one branch into another branch on a Git hosting platform.

Typical workflow:

```text
Create Branch
      ↓
Make Changes
      ↓
Commit
      ↓
Push
      ↓
Create Pull Request
      ↓
Code Review
      ↓
Merge
```

---

# 33. What is Code Review?

### Answer

Code review is the process of examining code changes before they are merged.

Reviewers may check:

```text
Correctness
Code quality
Security
Performance
Testing
Maintainability
```

---

# 34. What is a Merge?

### Answer

A merge combines changes from one branch into another.

Example:

```bash
git switch main
git merge feature-login
```

This attempts to integrate `feature-login` into `main`.

---

# 35. What is a Merge Conflict?

### Answer

A merge conflict occurs when Git cannot automatically combine changes.

For example, if two branches make conflicting changes to the same part of a file, Git may ask the developer to resolve the conflict manually.

---

# 36. How do you resolve a merge conflict?

### Answer

Basic process:

```text
1. Run merge/pull/rebase.
2. Git identifies conflicting files.
3. Open the conflicting files.
4. Decide which changes should remain.
5. Remove conflict markers.
6. Test the code.
7. Stage the resolved files.
8. Complete the merge/rebase.
```

For a merge, after resolving:

```bash
git add .
git commit
```

---

# 37. What are Git conflict markers?

### Answer

Git may mark a conflict like this:

```text
<<<<<<< HEAD
Current branch code
=======
Incoming branch code
>>>>>>> feature-login
```

You must decide which content to keep and remove the conflict markers.

---

# 38. What is a Fork?

### Answer

A fork is a separate copy of another repository under your account on a Git hosting platform.

It is commonly used when you do not have direct write access to the original repository.

Typical workflow:

```text
Original Repository
        ↓
      Fork
        ↓
Your Repository
        ↓
Create Branch
        ↓
Make Changes
        ↓
Pull Request
        ↓
Original Repository
```

---

# 39. Fork vs Clone

### Answer

| Fork | Clone |
|---|---|
| Creates a repository copy on the hosting platform | Creates a local copy on your computer |
| Usually done through GitHub/Git hosting | Done using Git |
| Useful for contributing without direct access | Useful for local development |

They are often used together.

---

# 40. What is `git stash`?

### Answer

`git stash` temporarily saves uncommitted changes so you can switch branches or work on another task without committing unfinished work.

```bash
git stash
```

Restore the changes:

```bash
git stash pop
```

---

# 41. When would you use `git stash`?

### Answer

Suppose:

```text
You are working on Feature A.
Your changes are incomplete.
A critical bug needs to be fixed immediately.
```

You can:

```bash
git stash
```

Then switch branches and fix the bug.

Later:

```bash
git stash pop
```

to restore the unfinished changes.

---

# 42. What is `git log`?

### Answer

`git log` displays the commit history.

```bash
git log
```

Compact version:

```bash
git log --oneline
```

Example:

```text
a31f2c1 Add login feature
92ab421 Fix validation
7d91e20 Initial commit
```

---

# 43. What is `git diff`?

### Answer

`git diff` shows changes between versions.

Unstaged changes:

```bash
git diff
```

Staged changes:

```bash
git diff --staged
```

It is useful for reviewing changes before committing.

---

# 44. What is `git restore`?

### Answer

`git restore` is used to restore files to another state.

Discard unstaged changes:

```bash
git restore app.py
```

Unstage a file:

```bash
git restore --staged app.py
```

---

# 45. What is `git reset`?

### Answer

`git reset` moves the current branch to another commit and can also modify the staging area and working tree depending on the selected mode.

Common modes:

```text
--soft
--mixed
--hard
```

---

# 46. Explain `git reset --soft`, `--mixed`, and `--hard`.

### Answer

| Mode | Commit Position | Staging Area | Working Files |
|---|---|---|---|
| `--soft` | Moved | Changes kept staged | Kept |
| `--mixed` | Moved | Reset | Kept |
| `--hard` | Moved | Reset | Reset |

Example:

```bash
git reset --soft HEAD~1
```

This removes the latest commit from the current branch while keeping its changes staged.

### Warning

```bash
git reset --hard
```

can discard local changes, so it should be used carefully.

---

# 47. What is `git revert`?

### Answer

`git revert` creates a **new commit** that reverses the changes introduced by an earlier commit.

```bash
git revert <commit-id>
```

It is commonly preferred for undoing changes that have already been shared because it does not require rewriting existing shared history.

---

# 48. `git reset` vs `git revert`

### Answer

| Reset | Revert |
|---|---|
| Moves branch history | Creates a new reversing commit |
| Can rewrite history | Preserves existing commits |
| Useful for local history changes | Often preferred for shared history |

### Interview Answer

> "`git reset` can move the branch backward and rewrite history, while `git revert` creates a new commit that undoes an earlier commit."

---

# 49. What is `git checkout`?

### Answer

`git checkout` is an older multi-purpose Git command used for operations such as switching branches and restoring files.

Modern Git provides more specific commands:

```bash
git switch
git restore
```

---

# 50. What is a Git Tag?

### Answer

A tag is a reference used to mark a specific point in Git history.

Tags are commonly used for software releases.

Example:

```text
v1.0.0
v2.0.0
```

Create a tag:

```bash
git tag v1.0.0
```

List tags:

```bash
git tag
```

---

# 51. What is `git remote`?

### Answer

`git remote` is used to manage connections to remote repositories.

View remotes:

```bash
git remote -v
```

Add a remote:

```bash
git remote add origin <repository-url>
```

---

# 52. What is an upstream branch?

### Answer

An upstream branch is the remote-tracking branch associated with a local branch.

Example:

```text
Local branch:
main

Upstream:
origin/main
```

Setting the upstream:

```bash
git push -u origin main
```

After that, future pushes can often simply use:

```bash
git push
```

---

# 53. What is `git config`?

### Answer

`git config` is used to configure Git settings.

Set username:

```bash
git config --global user.name "Your Name"
```

Set email:

```bash
git config --global user.email "you@example.com"
```

View configuration:

```bash
git config --list
```

---

# 54. What is the difference between `git add`, `git commit`, and `git push`?

### Answer

```text
git add
→ Working Directory → Staging Area

git commit
→ Staging Area → Local Repository

git push
→ Local Repository → Remote Repository
```

### Easy Memory Trick

```text
ADD → COMMIT → PUSH
```

---

# 55. What is the difference between `git clone` and `git pull`?

### Answer

```text
git clone
→ Creates a local copy of an existing remote repository.

git pull
→ Brings newer remote changes into an existing local repository.
```

---

# 56. What is the difference between `git clone` and `git fetch`?

### Answer

```text
git clone
→ Creates a new local repository from a remote repository.

git fetch
→ Updates information about an existing remote repository
  without integrating those changes into the current branch.
```

---

# 57. What is the difference between `git pull` and `git push`?

### Answer

```text
git pull
→ Remote → Local

git push
→ Local → Remote
```

### Easy Memory Trick

```text
PULL = Bring changes
PUSH = Send changes
```

---

# 58. What is the difference between `git branch` and `git switch`?

### Answer

```text
git branch
→ Used to create, list, or delete branches.

git switch
→ Used primarily to switch branches.
```

Example:

```bash
git branch feature-login
git switch feature-login
```

Or:

```bash
git switch -c feature-login
```

---

# 59. What is the difference between `git merge` and Pull Request?

### Answer

```text
git merge
→ Git operation that combines branches.

Pull Request
→ Collaboration workflow for proposing, reviewing, and
  eventually merging changes on a hosting platform.
```

A Pull Request may eventually result in a merge, squash merge, or another integration method depending on the team's workflow.

---

# 60. What is a clean working directory?

### Answer

A clean working directory means Git does not currently report uncommitted changes, such as modified, deleted, or untracked files.

Check with:

```bash
git status
```

---

# 61. What is an untracked file?

### Answer

An untracked file exists in the working directory but is not currently tracked by Git.

Example:

```text
?? app.py
```

Start tracking it:

```bash
git add app.py
```

---

# 62. What is a modified file?

### Answer

A modified file is a tracked file whose content has changed since the last committed version.

Example:

```text
modified: app.py
```

---

# 63. What is a staged file?

### Answer

A staged file has changes that have been added to the staging area and are prepared for the next commit.

```bash
git add app.py
```

---

# 64. What is a good Git commit message?

### Answer

A good commit message should be:

```text
Short
Clear
Specific
Meaningful
```

### Good Examples

```text
Add user authentication
Fix login validation
Update database connection
Add sales dashboard
```

### Poor Examples

```text
update
changes
done
final
```

---

# 65. Why should commits be small and meaningful?

### Answer

Small, logical commits make it easier to:

```text
Review code
Understand history
Find bugs
Revert specific changes
Collaborate with teammates
```

Example:

```text
Add login API
Fix password validation
Add login tests
```

are more useful than one large commit called:

```text
Complete project
```

---

# 66. What happens if two developers modify the same file?

### Answer

If the changes do not overlap, Git may merge them automatically.

If the changes conflict in the same area, Git may produce a merge conflict that developers must resolve manually.

---

# 67. How can you reduce merge conflicts?

### Answer

You cannot completely eliminate conflicts, but you can reduce them by:

```text
Pulling/fetching regularly
Keeping branches focused
Making small logical commits
Communicating with teammates
Avoiding unnecessary changes
```

---

# 68. What should you do before pushing code?

### Answer

A good workflow is:

```text
1. Check status.
2. Review changes.
3. Run tests.
4. Stage required changes.
5. Commit meaningful changes.
6. Synchronize with remote when appropriate.
7. Push.
```

Useful commands:

```bash
git status
git diff
git diff --staged
git log --oneline
```

---

# 69. What is a GitHub Issue?

### Answer

A GitHub Issue is used to track work such as:

```text
Bugs
Features
Tasks
Improvements
Questions
```

Example:

```text
Issue:
"Login fails for users with special characters in passwords."
```

Developers can work on the issue and submit a Pull Request containing the fix.

---

# 70. What is the relationship between an Issue and a Pull Request?

### Answer

An Issue generally describes a task or problem, while a Pull Request proposes code changes that may solve that task or problem.

Typical workflow:

```text
Issue
  ↓
Create Branch
  ↓
Implement Fix
  ↓
Commit
  ↓
Push
  ↓
Pull Request
  ↓
Review
  ↓
Merge
```

---

# 71. What is GitHub Actions?

### Answer

GitHub Actions is a GitHub feature used to automate workflows such as:

```text
Running tests
Building applications
Linting code
Deploying applications
```

A workflow can automatically run when events occur, such as a push or Pull Request.

### Placement Note

For a fresher interview, knowing the basic purpose of GitHub Actions is generally sufficient unless the job specifically focuses on DevOps or CI/CD.

---

# 72. What is CI/CD?

### Answer

CI/CD refers to practices and automation used to continuously integrate, test, deliver, or deploy software.

```text
CI
→ Continuous Integration

CD
→ Continuous Delivery / Continuous Deployment
```

GitHub Actions can be used to implement CI/CD pipelines.

---

# 73. What is a README file?

### Answer

A README provides important information about a project.

It commonly contains:

```text
Project description
Installation steps
Usage instructions
Technologies used
Examples
Project structure
Contribution information
```

A good GitHub repository should usually have a clear README.

---

# 74. How do you upload a local project to GitHub?

### Answer

A typical process is:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <repository-url>
git push -u origin main
```

### Flow

```text
Local Project
     ↓
git init
     ↓
git add
     ↓
git commit
     ↓
Connect Remote
     ↓
git push
     ↓
GitHub
```

---

# 75. How do you download an existing GitHub project?

### Answer

Use:

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

Then:

```bash
cd project
```

---

# 76. How do you create a feature and push it to GitHub?

### Answer

```bash
git switch -c feature-login

# Make changes

git status
git add .
git commit -m "Add login feature"
git push -u origin feature-login
```

Then create a Pull Request on GitHub if the project uses PR-based collaboration.

---

# 77. You have unfinished changes and suddenly need to fix a bug. What do you do?

### Answer

I can temporarily save the unfinished changes:

```bash
git stash
```

Then switch to the required branch:

```bash
git switch bugfix
```

After fixing the bug, I can restore my previous work:

```bash
git stash pop
```

---

# 78. You accidentally committed a change locally. How can you undo it?

### Answer

If the commit has not been shared, an appropriate `git reset` can be used depending on whether I want to keep the changes.

For example:

```bash
git reset --soft HEAD~1
```

This removes the latest commit while keeping its changes staged.

If the commit has already been shared, I would generally prefer:

```bash
git revert <commit-id>
```

to avoid rewriting shared history.

---

# 79. You pushed a wrong commit to a shared branch. What would you do?

### Answer

I would generally avoid rewriting shared history.

Instead:

```bash
git revert <commit-id>
git push
```

This creates a new commit that reverses the unwanted change.

---

# 80. How do you check what changed before committing?

### Answer

```bash
git status
git diff
```

After staging:

```bash
git diff --staged
```

---

# 81. How do you see previous commits?

### Answer

```bash
git log
```

For a compact view:

```bash
git log --oneline
```

---

# 82. How do you remove a file from Git but keep it on your computer?

### Answer

Use:

```bash
git rm --cached filename
```

Example:

```bash
git rm --cached .env
```

Then add the file to `.gitignore` if it should remain untracked.

---

# 83. How do you rename a file using Git?

### Answer

```bash
git mv old.txt new.txt
```

---

# 84. What is the difference between `git restore` and `git reset`?

### Answer

```text
git restore
→ Primarily used to restore file contents or unstage files.

git reset
→ Moves the current branch and can also modify staging and
  working files depending on the mode.
```

For modern Git, `restore` is generally clearer for file restoration.

---

# 85. What is the difference between `git revert` and deleting a commit?

### Answer

`git revert` does not delete the old commit.

Instead, it creates a new commit that reverses the earlier changes.

Example:

```text
Commit A
   ↓
Commit B
   ↓
Commit C
```

If B is reverted:

```text
Commit A
   ↓
Commit B
   ↓
Commit C
   ↓
Revert B
```

The original commit remains in history.

---

# 86. ⭐ Scenario: Your `git push` is rejected. What could be the reason?

### Answer

One common reason is that the remote branch contains commits that are not present locally.

I would first inspect the situation and synchronize appropriately.

For example:

```bash
git fetch
```

Then inspect the remote/local differences and integrate the remote changes using the team's preferred workflow.

A common approach is:

```bash
git pull --rebase
```

followed by:

```bash
git push
```

The exact solution depends on the branch and team workflow.

---

# 87. ⭐ Scenario: What happens if you run `git pull` and get conflicts?

### Answer

I would:

```text
1. Read the conflicting files.
2. Understand both changes.
3. Resolve the conflict.
4. Remove conflict markers.
5. Test the code.
6. Stage the resolved files.
7. Complete the merge/rebase.
8. Push the updated branch if required.
```

---

# 88. ⭐ Scenario: You accidentally deleted a file before committing. What can you do?

### Answer

If the file was tracked and the deletion has not been committed, it can often be restored with:

```bash
git restore filename
```

If the file was already committed in Git history, its previous version can be recovered using appropriate Git commands and the commit history.

---

# 89. ⭐ Scenario: Your teammate pushed changes while you were working. What should you do?

### Answer

Before pushing my work, I should synchronize with the latest remote changes.

For example:

```bash
git fetch
```

Then inspect and integrate the changes using the team's preferred approach.

If the workflow uses rebase:

```bash
git pull --rebase
```

Then resolve any conflicts, test, and push.

---

# 90. ⭐ Scenario: You need to work on two features at the same time. What would you do?

### Answer

I would create separate branches:

```text
main
 ├── feature-login
 └── feature-payment
```

This keeps the work isolated and makes it easier to develop, test, review, and merge each feature independently.

---

# 91. ⭐ Scenario: You need to contribute to a project but do not have write access. What would you do?

### Answer

A common GitHub workflow is:

```text
Fork Repository
      ↓
Clone Fork
      ↓
Create Branch
      ↓
Make Changes
      ↓
Commit
      ↓
Push
      ↓
Create Pull Request
      ↓
Original Repository
```

---

# 92. ⭐ Scenario: A secret API key was accidentally committed. What should you do?

### Answer

First, treat the secret as compromised.

```text
1. Revoke/rotate the exposed secret immediately.
2. Remove the secret from the project.
3. Add the secret file/configuration to .gitignore if appropriate.
4. Use environment variables or a proper secret-management system.
5. Remove the secret from Git history when necessary.
6. Inform the appropriate team if the repository is shared.
```

### Important

Simply deleting the secret in a new commit does **not** remove it from Git's previous history.

---

# 93. ⭐ Scenario: What would you do if a merge conflict occurs?

### Answer

I would not blindly choose one side.

I would:

```text
Understand both changes
        ↓
Determine the correct business/code behavior
        ↓
Resolve the conflict
        ↓
Remove conflict markers
        ↓
Run tests
        ↓
Stage the resolution
        ↓
Complete merge/rebase
```

---

# 94. ⭐ Scenario: How would you explain your Git workflow in a real project?

### Answer

> "I usually create a separate branch for a feature or bug fix. I make the changes, review them using `git diff` and `git status`, stage them with `git add`, and commit them with a meaningful message. Then I push the branch to the remote repository and create a Pull Request for code review. After the review and required checks, the changes are merged into the main branch."

---

# 95. ⭐ Most Important Git Commands

```bash
git init
git clone
git status
git add
git commit
git push
git pull
git fetch
git branch
git switch
git merge
git log
git diff
git remote
git restore
git reset
git revert
git stash
git tag
git config
```

---

# 96. ⭐ Git Command Cheat Sheet

| Task | Command |
|---|---|
| Initialize repository | `git init` |
| Clone repository | `git clone <url>` |
| Check status | `git status` |
| Stage file | `git add file` |
| Stage changes | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull | `git pull` |
| Fetch | `git fetch` |
| Create branch | `git branch branch-name` |
| Switch branch | `git switch branch-name` |
| Create + switch | `git switch -c branch-name` |
| Merge branch | `git merge branch-name` |
| View history | `git log` |
| Compact history | `git log --oneline` |
| View changes | `git diff` |
| View staged changes | `git diff --staged` |
| View remote | `git remote -v` |
| Stash changes | `git stash` |
| Restore stash | `git stash pop` |
| Revert commit | `git revert <commit-id>` |
| Restore file | `git restore file` |
| Unstage file | `git restore --staged file` |
| Configure Git | `git config` |

---

# 97. ⭐ Top Differences to Memorize

## Git vs GitHub

```text
Git
→ Version control system.

GitHub
→ Hosting and collaboration platform.
```

## Add vs Commit vs Push

```text
git add
→ Working Directory → Staging

git commit
→ Staging → Local Repository

git push
→ Local Repository → Remote
```

## Pull vs Push

```text
pull
→ Remote → Local

push
→ Local → Remote
```

## Pull vs Fetch

```text
pull
→ Fetch + Integration

fetch
→ Download remote changes without automatic integration
```

## Clone vs Pull

```text
clone
→ Create local repository from remote.

pull
→ Update an existing local repository.
```

## Reset vs Revert

```text
reset
→ Moves branch history.

revert
→ Creates a new commit that reverses an earlier commit.
```

## Fork vs Clone

```text
fork
→ Repository copy on hosting platform.

clone
→ Repository copy on local computer.
```

## Branch vs Pull Request

```text
Branch
→ Separate line of development.

Pull Request
→ Request to review and integrate changes between branches.
```

---

# 98. ⭐ Rapid-Fire Interview Questions

## Q1. What is Git?

**Answer:** A distributed version control system.

## Q2. What is GitHub?

**Answer:** A platform for hosting Git repositories and collaboration.

## Q3. What is a repository?

**Answer:** A project directory containing files and Git history/metadata.

## Q4. What is a commit?

**Answer:** A recorded snapshot of staged changes.

## Q5. What is staging?

**Answer:** Selecting changes for the next commit.

## Q6. What does `git add` do?

**Answer:** Stages changes.

## Q7. What does `git commit` do?

**Answer:** Records staged changes locally.

## Q8. What does `git push` do?

**Answer:** Sends local commits to a remote repository.

## Q9. What does `git pull` do?

**Answer:** Fetches remote changes and integrates them into the current branch.

## Q10. What does `git fetch` do?

**Answer:** Downloads remote changes without automatically integrating them.

## Q11. What is a branch?

**Answer:** An independent line of development.

## Q12. What is a merge?

**Answer:** Combining changes from one branch into another.

## Q13. What is a merge conflict?

**Answer:** A situation where Git cannot automatically combine conflicting changes.

## Q14. What is `.gitignore`?

**Answer:** A file that specifies files/directories Git should normally ignore as untracked.

## Q15. What is `origin`?

**Answer:** The conventional name for a remote repository.

## Q16. What is HEAD?

**Answer:** A reference to the currently checked-out commit.

## Q17. What is `git stash`?

**Answer:** Temporarily saves uncommitted changes.

## Q18. What is `git revert`?

**Answer:** Creates a new commit that reverses an earlier commit.

## Q19. What is `git reset`?

**Answer:** Moves the current branch and can modify staging/working files depending on the mode.

## Q20. What is a Pull Request?

**Answer:** A request to review and integrate changes from one branch into another.

## Q21. What is a fork?

**Answer:** A repository copy under your account on a hosting platform.

## Q22. What is code review?

**Answer:** Reviewing code changes before integration.

## Q23. What is `git log`?

**Answer:** Displays commit history.

## Q24. What is `git diff`?

**Answer:** Shows differences between versions or states.

## Q25. What is `.git`?

**Answer:** The directory containing Git repository metadata.

---

# 99. ⭐ Complete Interview Workflow

```text
                    PROJECT
                       ↓
                  Git Repository
                       ↓
                  Create Branch
                       ↓
                Make Code Changes
                       ↓
                  git status
                       ↓
                   git diff
                       ↓
                    git add
                       ↓
                  git commit
                       ↓
                   git push
                       ↓
                Pull Request
                       ↓
                  Code Review
                       ↓
                 Tests / Checks
                       ↓
                     Merge
                       ↓
                    main
```

---

# 100. ⭐ Final Placement Checklist

Before a Git/GitHub interview, make sure you can explain:

```text
☑ Git
☑ GitHub
☑ Version Control
☑ Repository
☑ Working Directory
☑ Staging Area
☑ Commit
☑ Branch
☑ Remote
☑ origin
☑ HEAD
☑ .git
☑ .gitignore
☑ git init
☑ git clone
☑ git status
☑ git add
☑ git commit
☑ git push
☑ git pull
☑ git fetch
☑ git merge
☑ Merge Conflict
☑ Pull Request
☑ Fork
☑ git stash
☑ git reset
☑ git revert
☑ git restore
☑ git diff
☑ git log
☑ GitHub Issues
☑ Basic GitHub Actions
```

## Highest-Priority Differences

```text
Git vs GitHub
Working Directory vs Staging Area vs Repository
git add vs git commit vs git push
git clone vs git pull
git pull vs git fetch
git reset vs git revert
git merge vs Pull Request
Fork vs Clone
```

## Highest-Priority Practical Skills

```text
Create a repository
Clone a repository
Create a branch
Switch branches
Make changes
Check status
Review differences
Stage changes
Commit changes
Push changes
Pull changes
Fetch changes
Create a Pull Request
Resolve a basic merge conflict
Use git stash
Undo a local change
Revert a shared commit
Use .gitignore
```

> **Placement Priority:** Focus most on the Git workflow, branches, staging, commits, push/pull/fetch, merge conflicts, reset/revert, `.gitignore`, Pull Requests, and practical scenarios. These are the highest-value Git/GitHub topics for fresher placement interviews.