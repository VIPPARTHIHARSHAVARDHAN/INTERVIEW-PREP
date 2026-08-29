# Git Basics and Workflow

> Placement-focused Git notes covering only the important concepts and commands required for fresher interviews.

---

# 1. What is Git?

Git is a **distributed version control system (VCS)** used to track changes in source code and collaborate with other developers.

### Why Git is used

```text
Track code changes
Maintain different versions
Work with multiple developers
Create branches
Merge changes
Recover previous versions
Collaborate through remote repositories
```

---

# 2. What is Version Control?

Version control is a system that tracks changes made to files over time.

It allows developers to:

```text
→ See what changed
→ See who changed it
→ Restore previous versions
→ Work on different features
→ Collaborate with others
```

---

# 3. Git vs GitHub

| Git | GitHub |
|---|---|
| Version control system | Hosting/collaboration platform |
| Runs locally | Cloud-based platform |
| Tracks code changes | Stores and collaborates on Git repositories |
| Can work without GitHub | Uses Git repositories |
| Command-line tool | Web-based service |

### Simple Interview Answer

> "Git is the version control system, while GitHub is a platform used to host Git repositories and collaborate with others."

---

# 4. What is a Repository?

A repository, or **repo**, is a location where a project's files and Git version history are stored.

A repository can be:

```text
Local Repository
Remote Repository
```

### Local Repository

Exists on your computer.

### Remote Repository

Exists on a remote hosting service such as GitHub.

---

# 5. What is a Working Directory?

The working directory is the actual folder containing the files you are currently working on.

Example:

```text
project/
├── app.py
├── README.md
└── data/
```

These files are part of your working directory.

---

# 6. What is the Staging Area?

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

# 7. What is a Commit?

A commit is a snapshot of the staged changes recorded in Git history.

Example:

```bash
git commit -m "Add login feature"
```

A good commit message briefly describes the change.

---

# 8. What is the Basic Git Workflow?

The most important Git workflow is:

```text
Create / Modify files
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

For an existing project, you may also first:

```text
git pull
```

to bring remote changes into your local repository.

---

# 9. `git init`

`git init` initializes a new Git repository in the current directory.

### Command

```bash
git init
```

It creates a hidden `.git` directory containing Git's repository metadata.

---

# 10. `git clone`

`git clone` creates a local copy of an existing remote repository.

### Command

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

---

# 11. `git status`

`git status` shows the current state of the working directory and staging area.

### Command

```bash
git status
```

It can show:

```text
Modified files
Untracked files
Staged changes
Branch information
```

---

# 12. `git add`

`git add` moves changes from the working directory to the staging area.

### Add one file

```bash
git add file.py
```

### Add multiple files

```bash
git add file1.py file2.py
```

### Add all changes

```bash
git add .
```

---

# 13. `git commit`

`git commit` records staged changes in the local repository.

### Command

```bash
git commit -m "Add new feature"
```

### Important

`git commit` does **not** normally send changes to GitHub.

It creates the commit locally.

---

# 14. `git push`

`git push` sends local commits to a remote repository.

### Command

```bash
git push
```

Common first push:

```bash
git push -u origin main
```

---

# 15. `git pull`

`git pull` retrieves changes from a remote repository and integrates them into the current local branch.

A simplified view is:

```text
git fetch
+
git merge
```

### Command

```bash
git pull
```

---

# 16. `git fetch`

`git fetch` downloads information and commits from a remote repository without automatically integrating those changes into your current branch.

### Command

```bash
git fetch
```

Then you can inspect the changes before merging or rebasing.

---

# 17. `git pull` vs `git fetch`

| `git fetch` | `git pull` |
|---|---|
| Downloads remote changes | Downloads remote changes |
| Does not automatically integrate them | Integrates them into current branch |
| Gives more control | More convenient |

### Simple Interview Answer

> "`git fetch` downloads remote changes without integrating them, while `git pull` fetches and integrates them into the current branch."

---

# 18. What is a Branch?

A branch is an independent line of development in a Git repository.

Branches allow developers to work on features without directly modifying the main branch.

Example:

```text
main
 │
 ├── feature-login
 │
 └── feature-payment
```

---

# 19. Why are Branches Used?

Branches are used to:

```text
Develop features separately
Fix bugs safely
Work with multiple developers
Test changes
Keep main code stable
```

---

# 20. Create a Branch

### Command

```bash
git branch feature-login
```

This creates the branch but does not switch to it.

---

# 21. Switch to a Branch

### Command

```bash
git switch feature-login
```

Older commonly used command:

```bash
git checkout feature-login
```

---

# 22. Create and Switch to a Branch

Modern command:

```bash
git switch -c feature-login
```

Older equivalent:

```bash
git checkout -b feature-login
```

---

# 23. List Branches

### Local branches

```bash
git branch
```

### Remote branches

```bash
git branch -r
```

### All branches

```bash
git branch -a
```

---

# 24. Delete a Branch

### Delete a local branch

```bash
git branch -d feature-login
```

If the branch has unmerged changes and you intentionally want to force deletion:

```bash
git branch -D feature-login
```

---

# 25. What is `main`?

`main` is commonly used as the primary branch of a repository.

It is not a special requirement of Git; repositories can use other branch names.

Example:

```text
main
├── feature-login
├── feature-payment
└── bugfix-header
```

---

# 26. What is a Remote?

A remote is a named reference to another Git repository, usually a repository hosted somewhere else.

The most common remote name is:

```text
origin
```

---

# 27. What is `origin`?

`origin` is the conventional default name Git gives to the remote repository when you clone a repository.

Example:

```bash
git clone https://github.com/user/project.git
```

Git commonly creates:

```text
origin
```

as the remote name.

---

# 28. `git remote`

To see configured remotes:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

# 29. What is HEAD?

`HEAD` is a reference that indicates the currently checked-out commit, normally through the current branch.

Example:

```text
HEAD
 ↓
main
 ↓
latest commit
```

It tells Git where your current checkout is positioned.

---

# 30. What is `.git`?

`.git` is the hidden directory created when a Git repository is initialized.

It contains important repository metadata, including:

```text
Commit history
Branch references
Configuration
Repository objects
Other Git metadata
```

Deleting `.git` removes the repository's local Git metadata from that directory.

---

# 31. What is `.gitignore`?

`.gitignore` specifies files and directories that Git should normally ignore when detecting untracked files.

Example:

```gitignore
__pycache__/
.env
*.log
node_modules/
```

Typical files to ignore:

```text
Passwords / secrets
Environment files
Temporary files
Build files
Logs
Generated files
Dependencies
```

### Important

`.gitignore` does not automatically stop tracking a file that is already tracked.

---

# 32. Why should `.env` files usually be ignored?

`.env` files may contain sensitive configuration such as:

```text
API keys
Database passwords
Access tokens
Secret credentials
```

They should generally not be committed to a public repository.

Instead, provide an example file such as:

```text
.env.example
```

with placeholder values.

---

# 33. What is `git log`?

`git log` displays commit history.

### Command

```bash
git log
```

A compact version:

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

# 34. What is `git diff`?

`git diff` shows differences between versions of files.

### Show unstaged changes

```bash
git diff
```

### Show staged changes

```bash
git diff --staged
```

This is useful for reviewing changes before committing.

---

# 35. What is `git rm`?

`git rm` removes a tracked file from Git and normally from the working directory.

### Command

```bash
git rm file.txt
```

If you want to stop tracking a file but keep it locally:

```bash
git rm --cached file.txt
```

---

# 36. What is `git mv`?

`git mv` renames or moves a tracked file.

### Command

```bash
git mv old.txt new.txt
```

---

# 37. What is `git restore`?

`git restore` is used to restore files to another state.

For example, discard unstaged changes in a file:

```bash
git restore file.py
```

Restore a staged file from the index:

```bash
git restore --staged file.py
```

---

# 38. What is `git reset`?

`git reset` moves the current branch reference to another commit and can also modify the staging area and working tree depending on the mode.

Common modes:

```text
--soft
--mixed
--hard
```

---

# 39. `git reset --soft` vs `--mixed` vs `--hard`

| Command | Commit | Staging Area | Working Files |
|---|---|---|---|
| `--soft` | Moves | Kept | Kept |
| `--mixed` | Moves | Reset | Kept |
| `--hard` | Moves | Reset | Reset |

### Important

```bash
git reset --hard
```

can discard local changes. Use it carefully.

---

# 40. What is `git revert`?

`git revert` creates a **new commit** that reverses the changes introduced by an earlier commit.

Example:

```bash
git revert <commit-id>
```

It is generally safer than rewriting shared history because it preserves the existing commits.

---

# 41. `git reset` vs `git revert`

| Reset | Revert |
|---|---|
| Moves branch history | Creates a new reversing commit |
| Can rewrite local history | Preserves existing history |
| Useful for local changes | Often preferred for shared history |

### Interview Answer

> "`git reset` can move the branch back and potentially rewrite history, while `git revert` creates a new commit that undoes an earlier commit."

---

# 42. What is `git checkout`?

`git checkout` is an older multi-purpose Git command that has been used for switching branches and restoring files.

Modern Git provides more specific commands:

```bash
git switch
git restore
```

These make the intended operation clearer.

---

# 43. What is Merging?

Merging combines changes from one branch into another branch.

Example:

```text
main
  ↑
  │ merge
feature-login
```

If you are on `main`:

```bash
git merge feature-login
```

---

# 44. What is a Merge Conflict?

A merge conflict occurs when Git cannot automatically combine changes.

A common case is when two branches modify overlapping parts of the same file differently.

Example:

```text
main:
print("Hello")

feature:
print("Hi")
```

Git may need the developer to decide which version should remain.

---

# 45. How do you Resolve a Merge Conflict?

Basic process:

```text
1. Run merge/pull/rebase.
2. Git identifies conflicting files.
3. Open the conflicting files.
4. Decide which changes to keep.
5. Remove conflict markers.
6. Test the code.
7. Stage resolved files.
8. Complete the merge/rebase.
```

Typical commands after resolving a merge conflict:

```bash
git add .
git commit
```

---

# 46. What are Conflict Markers?

Git may mark conflicts like:

```text
<<<<<<< HEAD
Current branch code
=======
Incoming branch code
>>>>>>> feature-login
```

You must manually choose the correct content and remove these markers.

---

# 47. What is a Pull Request?

A Pull Request (PR) is a request to merge changes from one branch into another branch on a platform such as GitHub.

Typical workflow:

```text
Create branch
      ↓
Make changes
      ↓
Commit
      ↓
Push branch
      ↓
Create Pull Request
      ↓
Code Review
      ↓
Merge
```

---

# 48. What is Code Review?

Code review is the process of examining code changes before they are merged.

Reviewers may check:

```text
Correctness
Code quality
Security
Performance
Maintainability
Tests
```

---

# 49. What is Forking?

A fork is a separate copy of another repository under your own account on a Git hosting platform.

Forks are commonly used when you do not have direct write access to the original repository.

Typical open-source workflow:

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

# 50. Fork vs Clone

| Fork | Clone |
|---|---|
| Creates a repository copy on a hosting platform | Creates a local copy on your computer |
| Usually done through GitHub/Git hosting | Done using Git |
| Useful for contributing without direct access | Used to work with a repository locally |

They are often used together.

---

# 51. What is `git stash`?

`git stash` temporarily saves uncommitted changes so you can switch tasks or branches without committing unfinished work.

### Command

```bash
git stash
```

Later:

```bash
git stash pop
```

---

# 52. When would you use `git stash`?

Example:

```text
You are working on Feature A.
Your changes are incomplete.

Suddenly:
A bug needs immediate fixing on another branch.
```

You can:

```bash
git stash
```

Switch branches, fix the bug, and later restore the unfinished changes.

---

# 53. What is `git stash pop`?

It restores the most recently stashed changes and removes that stash entry if the operation succeeds.

```bash
git stash pop
```

---

# 54. What is a Git Tag?

A tag is a reference used to mark a specific point in Git history.

Tags are commonly used for releases.

Example:

```text
v1.0.0
v2.0.0
```

---

# 55. What is `git tag`?

Create a tag:

```bash
git tag v1.0.0
```

List tags:

```bash
git tag
```

Tags can also be pushed to a remote:

```bash
git push origin v1.0.0
```

---

# 56. What is `git config`?

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

# 57. What is the difference between local and remote repository?

```text
Local Repository
→ Exists on your computer.

Remote Repository
→ Exists on a remote hosting service.
```

Typical flow:

```text
Local changes
     ↓
Commit
     ↓
Push
     ↓
Remote repository
```

---

# 58. What is `origin/main`?

`origin/main` is a remote-tracking reference representing the `main` branch as last known from the remote named `origin`.

It is not the same thing as your local `main` branch.

Example:

```text
Local:
main

Remote-tracking:
origin/main
```

---

# 59. What happens when you run `git push`?

Simplified process:

```text
Local commits
      ↓
Git sends required objects
      ↓
Remote repository receives them
      ↓
Remote branch is updated
```

The exact behavior depends on the configured upstream and push command.

---

# 60. What happens when you run `git pull`?

A simplified view is:

```text
Remote Repository
       ↓
     fetch
       ↓
Local repository
       ↓
merge/rebase depending on configuration
       ↓
Current branch
```

---

# 61. What is an Upstream Branch?

An upstream branch is the remote-tracking branch associated with a local branch.

For example:

```text
Local branch:
main

Upstream:
origin/main
```

Then commands such as:

```bash
git pull
git push
```

can often work without specifying the remote and branch every time.

---

# 62. Why use `git push -u origin main`?

The `-u` option sets the upstream tracking relationship.

```bash
git push -u origin main
```

After that, future pushes from the branch can often simply use:

```bash
git push
```

---

# 63. What is the difference between `git add`, `git commit`, and `git push`?

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

# 64. What is the difference between `git clone` and `git pull`?

```text
git clone
→ Used to create a local repository from an existing remote repository,
  usually when setting up the project for the first time.

git pull
→ Used to bring newer remote changes into an existing local repository.
```

---

# 65. What is the difference between `git add .` and `git add -A`?

Both can stage changes, but their behavior can differ depending on the Git version and working-directory context.

For modern Git, `git add -A` stages additions, modifications, and deletions across the repository.

```bash
git add -A
```

`git add .` stages changes under the current directory.

For interview purposes:

> "`git add -A` stages all changes in the repository, while `git add .` stages changes under the current directory."

---

# 66. What is a Clean Working Directory?

A clean working directory means there are no uncommitted changes that Git considers modified, deleted, or untracked.

Check using:

```bash
git status
```

---

# 67. What is an Untracked File?

An untracked file is a file that exists in the working directory but is not currently tracked by Git.

Example:

```text
?? newfile.py
```

You can start tracking it with:

```bash
git add newfile.py
```

---

# 68. What is a Modified File?

A modified file is a tracked file whose content has changed since the last committed version.

Example:

```text
modified: app.py
```

---

# 69. What is a Staged File?

A staged file has changes that have been added to the staging area and are prepared to be included in the next commit.

```bash
git add app.py
```

Then:

```bash
git status
```

will show the staged change.

---

# 70. Complete Git Workflow Example

Suppose you want to create a new project.

### Step 1: Create a project

```bash
mkdir my-project
cd my-project
```

### Step 2: Initialize Git

```bash
git init
```

### Step 3: Create files

```text
app.py
README.md
```

### Step 4: Check status

```bash
git status
```

### Step 5: Stage files

```bash
git add .
```

### Step 6: Commit

```bash
git commit -m "Initial commit"
```

### Step 7: Connect remote

```bash
git remote add origin <repository-url>
```

### Step 8: Push

```bash
git push -u origin main
```

---

# 71. Feature Branch Workflow

A common team workflow is:

```text
main
  ↓
Create feature branch
  ↓
Develop feature
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
Merge
```

Example:

```bash
git switch -c feature-login

# make changes

git add .
git commit -m "Add login feature"
git push -u origin feature-login
```

Then create a Pull Request.

---

# 72. What is a Good Commit Message?

A good commit message should be:

```text
Short
Clear
Specific
Meaningful
```

Good:

```text
Add user authentication
Fix login validation
Update database connection
```

Poor:

```text
changes
update
done
final
```

---

# 73. Should You Commit Every Small Change?

Not necessarily.

Commits should represent meaningful, logical units of work.

For example:

```text
Good:
Add user authentication

Good:
Fix password validation

Less useful:
Change line 10

Less useful:
Small update
```

---

# 74. What is Git History?

Git history is the sequence of commits recorded in the repository.

You can inspect it using:

```bash
git log
```

History helps developers:

```text
Understand changes
Find bugs
Identify when a change occurred
Review previous versions
```

---

# 75. What is a Distributed Version Control System?

Git is distributed because each cloned repository contains the information needed to maintain its own history.

Developers can work locally and create commits without requiring a remote server for every operation.

---

# 76. Why is Git useful in team projects?

Git allows teams to:

```text
Work on separate branches
Track changes
Review code
Merge features
Resolve conflicts
Revert changes
Maintain project history
Collaborate through remote repositories
```

---

# 77. What happens if two developers edit the same file?

If their changes do not overlap, Git may merge them automatically.

If they make conflicting changes to the same area, Git may produce a merge conflict.

The developers must resolve the conflict manually.

---

# 78. How can you avoid Git conflicts?

You cannot completely eliminate conflicts, but you can reduce them by:

```text
Pulling/rebasing regularly
Keeping branches focused
Making small logical commits
Communicating with teammates
Avoiding unnecessary changes to shared files
```

---

# 79. What should you do before pushing code?

A good workflow is:

```text
1. Check your changes.
2. Run tests.
3. Review the diff.
4. Check Git status.
5. Commit meaningful changes.
6. Pull/rebase as appropriate if the branch is shared.
7. Push.
```

Useful commands:

```bash
git status
git diff
git log --oneline
```

---

# 80. ⭐ Most Important Git Commands for Placements

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

# 81. ⭐ Git Command Cheat Sheet

| Task | Command |
|---|---|
| Initialize repository | `git init` |
| Clone repository | `git clone <url>` |
| Check status | `git status` |
| Stage file | `git add file` |
| Stage all changes | `git add .` |
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
| Temporarily save changes | `git stash` |
| Restore stash | `git stash pop` |
| Undo with new commit | `git revert <commit>` |
| Restore file | `git restore file` |
| Configure Git | `git config` |

---

# 82. ⭐ Rapid-Fire Interview Questions

## Q1. What is Git?

### Answer

Git is a distributed version control system used to track changes and collaborate on software projects.

---

## Q2. What is GitHub?

### Answer

GitHub is a platform for hosting Git repositories and collaborating on software projects.

---

## Q3. Git vs GitHub?

### Answer

Git is the version control system; GitHub is a platform that hosts Git repositories and provides collaboration features.

---

## Q4. What is a repository?

### Answer

A repository contains project files along with Git's version history and metadata.

---

## Q5. What is a commit?

### Answer

A commit is a recorded snapshot of staged changes in the local repository.

---

## Q6. What is staging?

### Answer

Staging means selecting changes that should be included in the next commit.

---

## Q7. What does `git add` do?

### Answer

It stages changes for the next commit.

---

## Q8. What does `git commit` do?

### Answer

It records staged changes in the local repository.

---

## Q9. What does `git push` do?

### Answer

It sends local commits to a remote repository.

---

## Q10. What does `git pull` do?

### Answer

It fetches remote changes and integrates them into the current branch.

---

## Q11. What does `git fetch` do?

### Answer

It downloads remote changes without automatically integrating them into the current branch.

---

## Q12. What is a branch?

### Answer

A branch is an independent line of development.

---

## Q13. Why are branches used?

### Answer

They allow developers to work on features or fixes independently without directly changing the main branch.

---

## Q14. What is a merge?

### Answer

A merge combines changes from one branch into another.

---

## Q15. What is a merge conflict?

### Answer

A merge conflict occurs when Git cannot automatically combine conflicting changes.

---

## Q16. What is `.gitignore`?

### Answer

It specifies files and directories that Git should normally ignore as untracked files.

---

## Q17. What is `origin`?

### Answer

`origin` is the conventional name for the remote repository created when cloning.

---

## Q18. What is HEAD?

### Answer

HEAD identifies the currently checked-out commit, normally through the current branch.

---

## Q19. What is `git stash`?

### Answer

It temporarily stores uncommitted changes so you can switch tasks or branches without committing unfinished work.

---

## Q20. What is `git revert`?

### Answer

It creates a new commit that reverses the changes introduced by an earlier commit.

---

## Q21. What is `git reset`?

### Answer

It moves the current branch to another commit and can also change the staging area and working tree depending on the selected mode.

---

## Q22. Reset vs Revert?

### Answer

Reset can rewrite the current branch history, while revert creates a new commit that undoes an earlier commit.

---

## Q23. Clone vs Pull?

### Answer

Clone creates a local copy of a remote repository, usually for initial setup. Pull brings new remote changes into an existing local repository.

---

## Q24. Pull vs Fetch?

### Answer

Fetch downloads remote changes without integrating them; pull downloads and integrates them.

---

## Q25. What is a Pull Request?

### Answer

A Pull Request is a request to merge changes from one branch into another, usually with code review.

---

## Q26. What is a Fork?

### Answer

A fork is a separate copy of a repository under your account on a Git hosting platform.

---

## Q27. Fork vs Clone?

### Answer

Fork creates a repository copy on the hosting platform, while clone creates a local copy on your computer.

---

## Q28. What is a remote repository?

### Answer

A remote repository is another Git repository, commonly hosted on a service such as GitHub, that can be synchronized with the local repository.

---

## Q29. What is an untracked file?

### Answer

A file present in the working directory that Git is not currently tracking.

---

## Q30. What is a staged file?

### Answer

A file whose changes have been added to the staging area for the next commit.

---

# 83. ⭐ Practical Interview Question

## Interviewer: "You made changes to a project. How will you push them to GitHub?"

### Answer

```bash
git status
git add .
git commit -m "Describe the changes"
git push
```

### Explanation

```text
git status
→ Check what changed.

git add .
→ Stage the changes.

git commit
→ Save them in local Git history.

git push
→ Send the commits to the remote repository.
```

---

# 84. ⭐ Practical Interview Question

## Interviewer: "You need to work on a new feature. What will you do?"

### Answer

```bash
git switch -c feature-name
```

Then:

```bash
# Make changes

git add .
git commit -m "Add feature"
git push -u origin feature-name
```

Then create a Pull Request if the team's workflow uses PRs.

---

# 85. ⭐ Practical Interview Question

## Interviewer: "You have unfinished changes but need to switch branches. What will you do?"

### Answer

Use:

```bash
git stash
```

Switch branches:

```bash
git switch other-branch
```

Later restore the changes:

```bash
git stash pop
```

---

# 86. ⭐ Practical Interview Question

## Interviewer: "You committed something locally but do not want that commit anymore. What can you do?"

### Answer

If the commit has not been shared and I want to move the branch backward, I can use an appropriate `git reset` mode.

For example:

```bash
git reset --soft HEAD~1
```

This removes the commit from the branch while keeping its changes staged.

If the commit has already been shared with others, I would generally prefer:

```bash
git revert <commit-id>
```

because it preserves shared history.

---

# 87. ⭐ Practical Interview Question

## Interviewer: "You pushed a wrong commit to a shared branch. What would you do?"

### Answer

I would generally avoid rewriting shared history.

Instead, I would use:

```bash
git revert <commit-id>
git push
```

This creates a new commit that reverses the unwanted change.

---

# 88. ⭐ Practical Interview Question

## Interviewer: "How do you check what changed before committing?"

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

# 89. ⭐ Practical Interview Question

## Interviewer: "How do you see previous commits?"

### Answer

```bash
git log
```

For a compact view:

```bash
git log --oneline
```

---

# 90. ⭐ Interview Workflow to Remember

The most important workflow is:

```text
                GIT WORKFLOW

                    Start
                      ↓
                 git clone/init
                      ↓
                Create Branch
                      ↓
                Make Changes
                      ↓
                 git status
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
                   Merge
                      ↓
                    main
```

---

# 91. Final Placement Revision

Before a Git/GitHub interview, make sure you can explain these without memorizing blindly:

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
```

## Most Important Differences

```text
Git vs GitHub
git add vs git commit vs git push
git clone vs git pull
git pull vs git fetch
git reset vs git revert
git merge vs Pull Request
Fork vs Clone
Working Directory vs Staging Area vs Repository
```

## Most Important Practical Skills

```text
Create a repository
Create a branch
Make changes
Stage changes
Commit changes
Push changes
Pull changes
Create a Pull Request
Resolve a basic merge conflict
Use git stash
Undo a local change
Revert a shared commit
Use .gitignore
```

> **Placement Priority:** Focus first on the Git workflow, staging/commits, branches, merge conflicts, push/pull/fetch, reset/revert, `.gitignore`, Pull Requests, and practical Git commands. These are the highest-value Git concepts for fresher interviews.