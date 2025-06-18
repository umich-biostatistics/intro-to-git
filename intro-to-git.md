---
marp: true
---

# BDSI GitHub Workshop

---

## What is Git/GitHub?

---

### Git
- A distributed version control system.
- Tracks changes in source code.
- Enables collaboration among developers.

---

### GitHub
- A web-based hosting service for Git repositories.
- Facilitates collaboration and code sharing.
- Git is the tool, GitHub is the platform.

---

## Why should I use it?

---

### Key Benefits
- **Track changes:** See who changed what, when, and why.
- **Revert to previous versions:** Easily undo mistakes.
- **No more "final_final_v2.R":** Keep a clean project history.
- **Collaborate:** Work on the same project with others seamlessly.
- **Reproducibility & Transparency:** Core principles in data science.

---

## Getting Started

---

### 1. Create a GitHub Account
- Go to github.com and sign up.

---

### 2. Install Git
- Download from [git-scm.com](https://git-scm.com/).
- Accept default options during installation.
- Verify in terminal: `git --version`

---

### 3. Configure Git
- Tell Git who you are. This is important for tracking changes.
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

---

## Setup an SSH key (Recommended)

---

### Why SSH?
- Securely connect to GitHub without entering your username/password each time.
- GitHub no longer supports password auth over https

---

### Generating and Adding Your Key
1.  Generate key. Run in terminal and accept the defaults:
    ```bash
    ssh-keygen
    ```
2.  Copy your public key.
    ```bash
    # On macOS
    pbcopy < ~/.ssh/id_rsa.pub
    # On Linux
    cat ~/.ssh/id_rsa.pub
    ```
3.  Go to GitHub settings > SSH and GPG keys > New SSH key.
4.  Paste your key and save.

---

## The Basic Workflow

---

### 1. Clone a Repository
- "Cloning" means making a local copy of a remote repository.
- Use the SSH URL from the GitHub repository page.
  ```bash
  git clone git@github.com:user/repo.git
  ```

---

### 2. Make Changes
- Create, edit, or delete files in your project folder.

---

### 3. Save Changes (Commit)
- A "commit" is a snapshot of your changes.
- **Step A: Stage your changes.** Tell Git which files to include.
  ```bash
  git add <file1> <file2>
  # or stage all changes
  git add .
  ```
- **Step B: Commit the staged changes.**
  ```bash
  git commit -m "A short, descriptive message about your changes"
  ```

---

### 4. Push Changes to GitHub
- "Pushing" sends your committed changes to the remote repository on GitHub.
  ```bash
  git push
  ```

---

## Branches

---

### What is a Branch?
- A separate line of development.
- Allows you to work on new features or fixes without affecting the main codebase (`main` branch).

---

### Branching Workflow
1.  Create and switch to a new branch for your task:
    ```bash
    git checkout -b new-feature-branch
    ```
2.  Make your changes, `add`, and `commit` on this branch.
3.  Push your new branch to GitHub:
    ```bash
    git push --set-upstream origin new-feature-branch
    ```

---

## Pull Request (PR)

---

### What is a Pull Request?
- A request to merge your changes from your branch into another branch (usually `main`).
- It's the primary way to collaborate and ask for a code review on GitHub.

---

### PR Workflow
1. Push your branch to GitHub.
2. Go to the repository on GitHub.
3. Click "Compare & pull request".
4. Write a clear title and description, and request reviewers.
5. Once approved, it can be merged.

---

# Q&A
---

### Understanding Repositories
- **Remote:** on GitHub
- **Local:** on your machine (a clone)
- The `git clone` command.

---

### Cloning in RStudio
1. New Project > Version Control > Git.
2. Paste repository URL (SSH or HTTPS).
3. Select a local directory.

---

### Initial Project Setup
- RStudio's Git pane.
- The hidden `.git` directory.

---

## Making Changes

---

### The Three Areas
- **Working Directory:** Your local files.
- **Staging Area (Index):** Prepare changes for commit (`git add`).
- **Local Repository:** Where committed changes are stored (`git commit`).

---

### Common File Operations
- Create new files.
- Modify existing files.
- Delete files.
- Rename files.

---

### RStudio Integration
- Changes are visible in RStudio's Git pane.
- Use checkboxes for staging.

---

## Commit

---

### What is a Commit?
- A snapshot of your repository.
- Records staged changes.
- Has a unique ID (SHA-1 hash).

---

### The Commit Process
1. Stage changes: `git add <file(s)>`
2. Commit staged changes: `git commit -m "Your commit message"`
- Write clear, concise commit messages.

---

### Viewing Commit History
- `git log` in the command line.
- RStudio's Git history viewer.

---

## Divergent branch

---

### Understanding Divergence
- When two branches have different commit histories.
- Happens when `main` is updated while you work on a feature branch.

---

### Detecting Divergence
- `git status` will show your branch has diverged.
- `git log --graph --all --decorate` to visualize.

---

### Resolving Divergence
- `git pull` to get remote changes.
- Strategies: **rebase** or **merge**.

---

## Rebase vs. Merge

---

### Rebase
- Moves your commits on top of the latest changes from another branch.
- Creates a linear, cleaner history.
- **Rewrites commit history.**
- `git rebase main`

---

### Caution with Rebase
- **NEVER rebase a public/shared branch.**
- It can cause major issues for collaborators.
- Use it for your personal branches before merging.

---

### Merge
- Integrates changes from one branch to another with a "merge commit".
- Preserves the exact history of both branches.
- `git merge feature-branch`

---

### Merge Conflicts
- Happen when Git can't automatically combine changes.
- You must manually edit the files to resolve them.
- `git status` -> resolve -> `git add` -> `git commit`

---

### When to Use Merge
- Integrating feature branches into `main`.
- When you want to preserve the full history.

---

## Dangerous Commands

---

### `git push --force`
- Overwrites the remote branch with your local one.
- **Can erase collaborators' work.**
- Use `--force-with-lease` for a safer alternative.
- Only use on your own, unshared branches after a rebase.

---

### `git reset --hard`
- **Destructive!** Discards all local changes (uncommitted and staged).
- `git reset --hard HEAD`: discard changes since last commit.
- `git reset --hard <commit_hash>`: go back to a specific commit.
- Use with extreme caution.

---

## Branches

---

### What is a Branch?
- A pointer to a commit.
- Allows isolated development for features or bug fixes.

---

### Branching Workflow
- **`main`:** Stable, production-ready code.
- **Feature branches:** For new features.
- **Bugfix branches:** For fixing bugs.
- **Hotfix branches:** For urgent production fixes.

---

### Common Branch Commands
- `git branch`: List branches
- `git branch <name>`: Create branch
- `git checkout <name>`: Switch to branch
- `git checkout -b <name>`: Create and switch
- `git branch -d <name>`: Delete local branch
- `git push origin --delete <name>`: Delete remote branch

---

### Branching Best Practices
- Keep branches short-lived.
- Use descriptive names.
- Merge or rebase frequently.

---

## Pull Request (PR)

---

### What is a Pull Request?
- A request to merge your changes into another branch.
- Facilitates code review and discussion.

---

### PR Workflow
1. Create a new branch.
2. Make and commit your changes.
3. Push the branch to GitHub.
4. Open a Pull Request on GitHub.

---

### Key Elements of a PR
- **Title and Description:** Explain the "what" and "why".
- **Reviewers:** Request feedback.
- **Files Changed:** See the diff.
- **Comments and Discussion.**
- **Checks/CI:** Automated tests.

---

### Merging a PR
- After approval and passing checks.
- Options:
    - Merge commit
    - Squash and merge
    - Rebase and merge

---

### Closing a PR
- Can be closed without merging if the changes are not needed.

---

# Q&A
