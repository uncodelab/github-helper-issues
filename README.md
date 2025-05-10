# GitHub Helper 🚀
[![License: Restricted](https://img.shields.io/badge/License-Proprietary-red)](LICENSE) 
[![GitHub Issues](https://img.shields.io/github/issues/uncodelab/github-helper-issues?label=Public%20Issues)](https://github.com/uncodelab/github-helper-issues) 

**This Bash script simplifies Git repository management by automating tasks in the GitHub Flow.** It provides an interactive interface to manage Git repositories using the **GitHub Flow** workflow, featuring a single default branch (e.g., `main`) and two branch types: `feature` and `hotfix`.

**GitHub Flow** is a lightweight, branch-based workflow ideal for teams making incremental changes:
- **Default Branch**: Holds production-ready code; all changes merge here (configurable, defaults to `main` or `master` if detected).
- **Feature Branches**: For new features or enhancements, prefixed with `feature/`.
- **Hotfix Branches**: For urgent fixes to the default branch, prefixed with `hotfix/`.

This script streamlines Git operations like repository setup, branch management, commits, and updates, reducing errors and saving time. It focuses on local Git management while adhering to GitHub Flow.

**Note**: Pull Requests (PRs) must be created and merged via GitHub’s web interface, as this script does not automate PR creation.

---

## Requirements 📋

Before running, ensure your system meets these prerequisites:
- Unix-like operating system (e.g., Linux, macOS, WSL on Windows).
- Bash shell (version 4+ recommended). Verify with `bash --version`.
- Git installed. Check with `git --version`.
  - If `user.name` or `user.email` are not set globally, the script will prompt you to configure them on first run.
- curl installed for GitHub API calls. Verify with `curl --version`.
- A GitHub Fine-Grained Personal Access Token with `Read access to metadata` and `Read and write access to administration` for creating and deleting repositories via the GitHub API.
- Terminal with color support (for status messages).
- Write permissions in the working directory.

---

## Installation 🛠️

Install the `github-helper.sh` script from the provided `github-helper-<version>.zip` file (e.g., `github-helper-0.1.0.zip`). Replace `<version>` with the version number of your downloaded ZIP. The script will be installed into a fixed `github-helper` directory. Choose one of these methods:

### Option 1: Current User (Alias)
For personal use:
1. **Extract the ZIP**:
   ```bash
   unzip github-helper-<version>.zip
   ```
   Example: For `github-helper-v0.1.0.zip`, use `unzip github-helper-v0.1.0.zip`.
2. **Move to Fixed Directory**:
   ```bash
   mv github-helper ~/scripts/github-helper
   ```
3. **Set Permissions**:
   ```bash
   chmod +x ~/scripts/github-helper/github-helper.sh
   ```
4. **Add Alias** to `~/.bashrc` (or `~/.zshrc`):
   ```bash
   echo -e '\nalias gh="~/scripts/github-helper/github-helper.sh"' >> ~/.bashrc
   ```
5. **Reload Shell**:
   ```bash
   source ~/.bashrc  # or source ~/.zshrc
   ```
6. **Test**:
   ```bash
   gh
   ```

### Option 2: Global (Symlink)
For all users:
1. **Extract the ZIP**:
   ```bash
   unzip github-helper-<version>.zip
   ```
   Example: For `github-helper-v0.1.0.zip`, use `unzip github-helper-v0.1.0.zip`.
2. **Move to Fixed Directory**:
   ```bash
   sudo mv github-helper /usr/local/share/github-helper
   ```
3. **Set Permissions**:
   ```bash
   sudo chmod +x /usr/local/share/github-helper/github-helper.sh
   ```
4. **Create Symlink**:
   ```bash
   sudo ln -sf /usr/local/share/github-helper/github-helper.sh /usr/bin/gh
   ```
5. **Test**:
   ```bash
   gh
   ```

### Cleanup
Remove the ZIP file (optional):
```bash
rm -f github-helper-<version>.zip
```
Example: `rm -f github-helper-v0.1.0.zip`

**Notes**:
- The ZIP extracts to a `github-helper-<version>` folder, which is then moved to `github-helper`.
- For updates, overwrite the existing `github-helper` directory with the new version’s contents.
- If `gh` conflicts with another tool (e.g., GitHub CLI), use a unique alias like `ghh` or `git-helper`.

---

## Updates ⬆️

To get the latest version of GitHub Helper:
1. **Visit the Updates Portal**:
   - Go to [givemeupdates.uncodelab.com](https://givemeupdates.uncodelab.com).
2. **Enter Purchase Key**:
   - Input your BuyMeACoffee or Ko-fi purchase key (received after buying the script).
3. **Receive Download Link**:
   - A download link for the latest `github-helper-<version>.zip` will be emailed to you.
4. **Update the Script**:
   - Replace your existing files with the new:
     - For **Alias**: Extract to `~/scripts/github-helper` and overwrite the old files.
     - For **Symlink**: Extract to `/usr/local/share/github-helper` and overwrite, then re-run `sudo ln -sf` if needed.
   - Verify the update by running `gh` (version displayed as `v0.1.0` as of script creation).

**Note**: Check [givemeupdates.uncodelab.com](https://givemeupdates.uncodelab.com) periodically for new features and bug fixes.

---

## Features ✨

The GitHub Helper provides these key functionalities:

### Initial Setup
- **Git Configuration**: Prompts for `user.name` and `user.email` if not set globally on first run.

### Repository Management
- **Setup Repository**: 
  - Initialize a new repo with an initial commit and optional tag (e.g., `v0.1.0`), or clone an existing one from GitHub.
  - Configures remote URL (e.g., `git@github.com:owner/repo.git`).
  - Creates or deletes GitHub repositories using a GitHub Fine-Grained Personal Access Token (PAT) with `Read access to metadata` and `Read and write access to administration` permissions. The PAT will be securely stored in ~/.config/github-helper/.github_pat (automatically created if missing). The directory and file are restricted to your user account (chmod 600).
- **Update Branch**: Sync local/remote branches (pull, push, or merge from default branch).

### Branch Operations
- **Feature Start**: Create `feature/` branches from the default branch for new work.
- **Hotfix Start**: Create `hotfix/` branches from the default branch for urgent fixes.
- **Finish Branch**: Push to remote for PR, switch to default branch, pull updates, delete local branch, and optionally tag releases (major/minor for features, patch for hotfixes).
- **Switch Branch**: Switch between local and remote branches, fetching remote branches if needed.
- **Delete Branch**: Safely delete local and/or remote branches, with pruning of stale remote branches.

### Commit Management
- **Commit Changes**: Flexible staging and committing with conventional commit types (e.g., `feat`, `fix`, `docs`):
  - Stage all (modified + untracked), modified only, untracked only, or interactively (`git add -i`).
  - Unstage all changes or undo the last unpushed commit.
- **Conflict Resolution**: Detects merge conflicts, provides guidance, and waits for manual resolution.

### Status Display
- Real-time info on current directory, remote URL, branch, last commit, and working directory state (staged, modified, untracked counts).

---

## Usage 💻

Run the script with:
```bash
gh
```
Navigate the menu using numbers (0-8) and Enter to select options. Use `0` to return or exit where allowed.

### First Run
- If Git is not installed, the script exits with an error.
- If `user.name` or `user.email` are unset, it prompts:
  ```
  > Enter your Git username: Your Name
  > Enter your Git email: your.email@example.com
  ```

### Main Menu
1. **Setup Repository**: Initialize or clone a repo.
2. **Commit Changes**: Stage and commit changes with flexible options.
3. **Feature Start**: Start a new `feature/` branch.
4. **Hotfix Start**: Start a new `hotfix/` branch.
5. **Finish Current Branch**: Merge to default branch (via GitHub PR), tag, and clean up.
6. **Update Current Branch**: Sync with remote or default branch.
7. **Switch Branch**: Switch to another branch.
8. **Delete Branch**: Delete local/remote branches.
0. **Exit**: Quit the script.

---

## Example Workflow 🔄

Here’s how to use the script for a typical feature development cycle:

1. **Start a Feature**:
   - Run `gh`, select **"3" (Feature Start)**, and enter `add-login`.
   - Script switches to `main`, pulls updates, and creates `feature/add-login`.

2. **Make Changes**:
   - Edit files (e.g., add a login page).

3. **Commit and Push Changes**:
   - Select **"2" (Commit Changes)**, choose **"1" (Stage all and commit)**, select commit type `feat`, and enter message: `add login page`.
   - When prompted `> Push changes to remote branch 'feature/add-login'? [y/N]:`, enter `y`.
   - Script pulls any remote updates (if the branch exists) and pushes the commit to `origin/feature/add-login`.

4. **Finish the Branch**:
   - Select **"5" (Finish Current Branch)**.
   - If not already pushed, it prompts to push for a PR. After merging the PR on GitHub and deleting the remote branch, it switches to `main`, pulls updates, deletes `feature/add-login` locally, and offers to tag a release (e.g., `v1.1.0` for a minor feature).

5. **Verify**:
   - Check `main` with **"6" (Update Current Branch)** → **"1" (Pull)** to sync with remote updates.

**Notes**:
- The working directory must be clean (no uncommitted changes) for branch operations, or the script will warn and pause.
- Merge conflicts require manual resolution (e.g., edit files, `git add`, `git commit`) with step-by-step guidance.
- Use **"6" (Update Current Branch)** for maintenance tasks like pulling updates or pushing existing commits not yet synced.

---

## Changelog 📜
See the [CHANGELOG.md](https://github.com/uncodelab/github-helper-issues/blob/main/CHANGELOG.md) file for a detailed history of updates and changes to GitHub Helper.

---

## Issue Tracker 🐞
[![GitHub Issues](https://img.shields.io/github/issues/uncodelab/github-helper-issues?label=Public%20Issues)](https://github.com/uncodelab/github-helper-issues)

All bug reports and feature requests are managed through our public issue tracker.

Encounter a bug or have a feature idea? File it at [GitHub Helper Issues](https://github.com/uncodelab/github-helper-issues):
- **Bugs**: Provide steps to reproduce, expected vs. actual behavior, and system details (OS, Bash/Git versions).
- **Features**: Describe the feature and its benefits.

**Tip**: Check existing issues to avoid duplicates.

---

## Project Status 🏗️

Actively maintained with regular updates.

---

## License 📝
[![License: Restricted](https://img.shields.io/badge/License-Proprietary-red)](LICENSE)

**This is NOT open-source software.**  
**See full [LICENSE](LICENSE) for legal terms of use.**  
**Unauthorized distribution violates copyright laws.**

---

*Copyright (c) 2025 uncodelab. All rights reserved.*