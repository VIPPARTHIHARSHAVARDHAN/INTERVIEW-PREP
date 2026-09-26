# Git & GitHub — 20 Basic Interview Questions & Answers

## 1. What is Git?

**Answer:**  
Git is a **distributed version control system** used to track changes in source code and manage different versions of a project.

It helps developers:
- Track changes
- Go back to previous versions
- Work with other developers
- Manage different versions of a project

---

## 2. What is GitHub?

**Answer:**  
GitHub is a **cloud-based platform** where Git repositories can be stored, shared, and collaborated on.

For example, I can keep my project code in a GitHub repository and share it with others.

---

## 3. What is the difference between Git and GitHub?

**Answer:**

| Git | GitHub |
|---|---|
| Version control system | Cloud platform |
| Runs locally on the computer | Runs online |
| Tracks code changes | Hosts Git repositories |
| Can work without internet | Usually accessed online |

**Simple example:**  
Git is the tool that manages my project versions, while GitHub is the online platform where I can store and share that repository.

---

## 4. What is a repository?

**Answer:**  
A repository, or **repo**, is a storage location for a project and its files along with the project's Git history.

It can be:
- **Local repository** — stored on my computer
- **Remote repository** — stored on GitHub or another Git hosting service

---

## 5. What is `git init`?

**Answer:**  
`git init` initializes a new Git repository in the current project folder.

```bash
git init
```

It creates a hidden `.git` directory that stores Git's tracking information.

---

## 6. What is `git clone`?

**Answer:**  
`git clone` creates a local copy of an existing remote repository.

```bash
git clone https://github.com/user/project.git
```

It downloads the repository, files, and Git history to my computer.

---

## 7. What does `git status` do?

**Answer:**  
`git status` shows the current state of my working directory.

It can show:
- Modified files
- Untracked files
- Staged files
- Current branch

```bash
git status
```

---

## 8. What is staging in Git?

**Answer:**  
Staging is the step where I select the changes that I want to include in the next commit.

```bash
git add file.py
```

Or:

```bash
git add .
```

The files are moved from the **working directory** to the **staging area**.

---

## 9. What is the difference between `git add` and `git commit`?

**Answer:**

`git add` puts changes into the **staging area**.

```bash
git add .
```

`git commit` saves the staged changes into the **local Git repository**.

```bash
git commit -m "Added data analysis"
```

### Simple flow:

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

## 10. What does `git push` do?

**Answer:**  
`git push` uploads my local commits to a remote repository such as GitHub.

```bash
git push
```

For example, after committing my project locally, I can use `git push` to upload those commits to GitHub.

---

## 11. What does `git pull` do?

**Answer:**  
`git pull` gets the latest changes from the remote repository and integrates them into my current local branch.

```bash
git pull
```

It is commonly used when other team members have pushed changes to the remote repository.

---

## 12. What is the difference between `git pull` and `git fetch`?

**Answer:**

`git fetch` downloads the latest changes from the remote repository but does **not automatically merge them** into my current branch.

```bash
git fetch
```

`git pull` downloads the changes and then integrates them into the current branch.

```bash
git pull
```

**Simple difference:**

```text
git fetch → Download changes
git pull  → Download + integrate changes
```

---

## 13. What is a branch in Git?

**Answer:**  
A branch is a separate line of development in a Git repository.

It allows me to work on a feature or change without directly modifying the main branch.

For example:

```bash
git branch feature-login
```

---

## 14. Why do we use branches?

**Answer:**  
Branches are used to develop features, fix bugs, or experiment without affecting the main code.

For example:

```text
main
  |
  └── feature-login
```

I can develop the login feature in `feature-login` and later merge it into `main`.

---

## 15. What is merging in Git?

**Answer:**  
Merging combines changes from one branch into another branch.

For example, if I want to merge `feature-login` into `main`:

```bash
git switch main
git merge feature-login
```

The changes from `feature-login` are integrated into `main`.

---

## 16. What is `.gitignore`?

**Answer:**  
`.gitignore` is a file that tells Git which files or folders should not be tracked.

For example:

```text
.env
__pycache__/
*.log
node_modules/
```

This is useful for preventing sensitive files, temporary files, dependencies, or generated files from being committed.

---

## 17. What is `origin` in Git?

**Answer:**  
`origin` is the default name commonly given to the remote repository from which a project was cloned.

For example:

```bash
git push origin main
```

Here:
- `origin` = remote repository
- `main` = branch

I can check remote repositories using:

```bash
git remote -v
```

---

## 18. What is a commit?

**Answer:**  
A commit is a saved snapshot of staged changes in the local Git repository.

Example:

```bash
git add .
git commit -m "Added sales dashboard"
```

The commit message describes what changes were made.

Each commit also has a unique identifier called a **commit hash**.

---

## 19. How do you upload a local project to GitHub?

**Answer:**

If I already have a local project, I can do the following:

### Step 1 — Initialize Git

```bash
git init
```

### Step 2 — Add files

```bash
git add .
```

### Step 3 — Commit

```bash
git commit -m "Initial commit"
```

### Step 4 — Connect the GitHub repository

```bash
git remote add origin <repository-url>
```

### Step 5 — Push to GitHub

```bash
git push -u origin main
```

After this, the project is available in the GitHub repository.

---

## 20. What happens if two people modify the same file?

**Answer:**  
If two people modify the same part of a file and Git cannot automatically combine the changes, a **merge conflict** occurs.

Git marks the conflicting section in the file.

The developer must:
1. Open the file
2. Decide which changes to keep
3. Remove the conflict markers
4. Save the file
5. Stage the resolved file
6. Commit the resolution

Example:

```bash
git add .
git commit -m "Resolved merge conflict"
```

---

# Important Git Workflow to Remember

For normal project work:

```text
Modify files
    ↓
git status
    ↓
git add .
    ↓
git commit -m "message"
    ↓
git push
```

To get other people's latest changes:

```text
git pull
```

---

# Most Important Commands

| Command | Purpose |
|---|---|
| `git init` | Initialize a repository |
| `git clone` | Copy a remote repository |
| `git status` | Check repository status |
| `git add` | Stage changes |
| `git commit` | Save staged changes |
| `git push` | Upload commits |
| `git pull` | Download and integrate changes |
| `git fetch` | Download remote changes |
| `git branch` | Manage branches |
| `git switch` | Switch branches |
| `git merge` | Merge branches |
| `git log` | View commit history |
| `git diff` | View changes |
| `git remote -v` | View remote repositories |

# Interview Tip

For a fresher, focus on understanding the **workflow** rather than memorizing commands.

The most important sequence is:

```text
git status
     ↓
git add
     ↓
git commit
     ↓
git push
```

You should also be able to explain the difference between:

- Git vs GitHub
- `git add` vs `git commit`
- `git push` vs `git pull`
- `git pull` vs `git fetch`
- Local vs remote repository
- Branch vs merge
- Working directory vs staging area
