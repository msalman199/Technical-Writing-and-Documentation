<div align="center">

# 🔀 Set Up a Docs-as-Code Workflow with Git

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![MkDocs](https://img.shields.io/badge/MkDocs-526CFE?style=for-the-badge&logo=materialformkdocs&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Objectives](#-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Environment Setup](#️-environment-setup)
- [🚀 Tasks](#-tasks)
  - [Task 1: 🗂️ Initialize Git Repository and Docs Structure](#task-1-🗂️-initialize-git-repository-and-docs-structure)
  - [Task 2: ⚙️ Install and Configure MkDocs](#task-2-⚙️-install-and-configure-mkdocs)
  - [Task 3: ✍️ Write Documentation Content](#task-3-✍️-write-documentation-content)
  - [Task 4: 🌿 Branching Workflow for Documentation Changes](#task-4-🌿-branching-workflow-for-documentation-changes)
  - [Task 5: 🔍 Simulate a Pull-Request Review](#task-5-🔍-simulate-a-pull-request-review)
  - [Task 6: 🔗 Merge and Build the Final Site](#task-6-🔗-merge-and-build-the-final-site)
  - [Task 7: 🌐 Verify the Published Site Locally](#task-7-🌐-verify-the-published-site-locally)
- [✅ Verification Checklist](#-verification-checklist)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Initialize a Git-based documentation repository with a structured `docs/` directory |
| 2 | Install and configure MkDocs to render Markdown files into a static site |
| 3 | Author multi-page documentation content following standard project conventions |
| 4 | Apply a feature-branch workflow for documentation changes |
| 5 | Simulate a pull-request review process using diffs and review notes |
| 6 | Merge changes and build/verify the final static site locally |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| Terminal familiarity | Basic familiarity with Linux terminal commands (`cd`, `mkdir`, `nano`/`vim`) |
| Git knowledge | Basic Git knowledge (`init`, `add`, `commit`, `branch`) |
| Runtime | Python 3 and `pip` available on the machine |
| Accounts | No cloud accounts or external services required |

---

## 🖥️ Environment Setup

> Use the **single Linux machine** provided via Start Lab.

Open a terminal session and verify tools:

```bash
# ✅ Verify Git, Python, and pip are available
git --version
python3 --version
pip3 --version
```

If Git is missing:

```bash
# 📦 Install Git
sudo apt update && sudo apt install git -y
```

---

## 🚀 Tasks

### Task 1: 🗂️ Initialize Git Repository and Docs Structure

Create and enter the project directory:

```bash
# 📁 Create the project folder and initialize Git
mkdir ~/docs-as-code-project && cd ~/docs-as-code-project
git init
git config user.name "Your Name"
git config user.email "you@example.com"
```

Create the docs directory structure:

```bash
# 📂 Create the docs/ folder and starter pages
mkdir docs
touch docs/index.md
touch docs/getting-started.md
touch docs/configuration.md
touch docs/contributing.md
```

Add a `.gitignore` for build artifacts:

```bash
# 🙈 Ignore build artifacts
cat <<EOF > .gitignore
site/
__pycache__/
*.pyc
EOF
```

Make the initial commit:

```bash
# ✅ Commit the initial docs structure
git add .
git commit -m "Initial docs structure"
```

---

### Task 2: ⚙️ Install and Configure MkDocs

Install MkDocs and a theme:

```bash
# 📦 Install MkDocs and the Material theme
pip3 install mkdocs mkdocs-material
```

Generate the config file manually (do **not** use `mkdocs new`, since it overwrites your existing `docs/`):

```bash
# ⚙️ Write the MkDocs configuration
cat <<EOF > mkdocs.yml
site_name: Sample Project Docs
theme:
  name: material
nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - Configuration: configuration.md
  - Contributing: contributing.md
EOF
```

> **TODO:** Verify the config loads without errors:
> ```bash
> mkdocs build --strict
> ```
> If this fails, check YAML indentation (must use spaces, not tabs).

---

### Task 3: ✍️ Write Documentation Content

Populate each file with Markdown content. Minimum required sections below — expand with your own details.

**`docs/index.md`**

```markdown
# Sample Project

Brief overview of what this project does and who it is for.
```

**`docs/getting-started.md`** — TODO: complete with:
- Installation steps
- A minimal usage example
- Prerequisites list

**`docs/configuration.md`** — TODO: complete with:
- A table of configuration options (name, type, default, description)
- At least one YAML or JSON config example

**`docs/contributing.md`** — TODO: complete with:
- Steps to fork/clone and set up a dev environment
- Coding/documentation style guidelines
- How to submit changes (reference the branching workflow from Task 4)

Commit your content:

```bash
# ✅ Commit the core documentation pages
git add docs/
git commit -m "Add core documentation pages"
```

---

### Task 4: 🌿 Branching Workflow for Documentation Changes

Ensure you're on `main` and create a feature branch:

```bash
# 🌿 Rename to main and branch off for the change
git branch -M main
git checkout -b feature/update-configuration-docs
```

Edit `docs/configuration.md` — add a new configuration option (e.g., a `log_level` setting) to the table you created in Task 3.

Stage and commit the change on the feature branch:

```bash
# ✅ Commit the configuration doc change
git add docs/configuration.md
git commit -m "Document log_level configuration option"
```

Confirm branch status:

```bash
# 🔍 Inspect branches and commit history
git branch
git log --oneline --graph --all
```

---

### Task 5: 🔍 Simulate a Pull-Request Review

Since there is no remote server in this lab, simulate the PR review locally.

Generate a diff between `main` and your feature branch:

```bash
# 🔍 Generate and view the review diff
git diff main feature/update-configuration-docs -- docs/configuration.md > review.diff
cat review.diff
```

Create a `REVIEW.md` file with inline-style comments referencing the diff:

```bash
# 📝 Write the review notes file
cat <<EOF > REVIEW.md
# Review: feature/update-configuration-docs

## File: docs/configuration.md

- Line (log_level entry): Clarify accepted values (e.g., debug, info, warn, error)
- Suggestion: Add a default value example in a code block
- Approval status: Changes Requested / Approved (choose one after fixing)
EOF
```

> **TODO:** Address at least one review comment by editing `docs/configuration.md` on the feature branch, then amend or add a new commit:
> ```bash
> git add docs/configuration.md REVIEW.md
> git commit -m "Address review feedback on log_level docs"
> ```

---

### Task 6: 🔗 Merge and Build the Final Site

Switch to `main` and merge the feature branch:

```bash
# 🔗 Merge the feature branch into main
git checkout main
git merge feature/update-configuration-docs
```

Resolve any merge conflicts if prompted (unlikely in this simple case, but check):

```bash
# 🔍 Confirm working tree status
git status
```

Build the static site:

```bash
# 🏗️ Build the MkDocs static site
mkdocs build
ls site/
```

---

### Task 7: 🌐 Verify the Published Site Locally

Serve the site using MkDocs' built-in dev server:

```bash
# 🌐 Start the local dev server
mkdocs serve --dev-addr=127.0.0.1:8000
```

Open a browser on the lab machine and navigate to `http://127.0.0.1:8000`. Confirm:

- All four nav pages load (Home, Getting Started, Configuration, Contributing)
- The updated `log_level` configuration entry appears

Stop the server with `Ctrl+C` when done.

---

## ✅ Verification Checklist

Run these checks to confirm lab completion:

```bash
# 📜 Shows main + feature branch history merged
git log --oneline --all --graph

# 📂 4 markdown files present
ls docs/

# 📝 Review comments exist
cat REVIEW.md

# 🏗️ Built site exists
ls site/index.html
```

**Expected:** merge commit visible in log, `site/` directory populated, `REVIEW.md` contains at least one comment addressed in a follow-up commit.

---

## 🛠️ Troubleshooting

<details>
<summary>Click to expand common issues and fixes</summary>

- **`mkdocs`: command not found:** Ensure pip3's bin directory is on your PATH, or run via `python3 -m mkdocs`.
- **YAML errors in `mkdocs.yml`:** Check for tabs instead of spaces; YAML is indentation-sensitive.
- **Merge conflict on `docs/configuration.md`:** Open the file, resolve `<<<<<<</>>>>>>>` markers manually, then `git add` and `git commit`.

</details>

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **Docs-as-Code** | Treating documentation like software: version-controlled, reviewed, and built via pipeline |
| **Feature Branch Workflow** | Isolating a documentation change on its own branch until it's reviewed and merged |
| **MkDocs** | A static site generator that renders a `docs/` folder of Markdown into a navigable HTML site |
| **Simulated PR Review** | Using `git diff` and a written review file to practice review discipline without a remote host |
| **Merge Commit** | The commit created when a feature branch's history is joined back into `main` |
| **Strict Build** | `mkdocs build --strict` fails on warnings (e.g., broken nav links), catching errors early |

---

## 🎯 Conclusion

In this lab, you built a complete docs-as-code workflow on a single Linux machine. You initialized a Git repository, structured Markdown documentation, and configured MkDocs to render it as a static site. You practiced a realistic branching strategy by making changes on a feature branch, simulated a pull-request review using diffs and a `REVIEW.md` file, and merged reviewed changes back into `main`. Finally, you built and verified the documentation site locally.

**Key Accomplishments:**
- ✅ Initialized a Git repository with a structured `docs/` directory
- ✅ Installed and configured MkDocs with the Material theme
- ✅ Authored multi-page documentation content across four standard pages
- ✅ Applied a feature-branch workflow for a documentation change
- ✅ Simulated a pull-request review using diffs and written review notes
- ✅ Merged reviewed changes and built/verified the static site locally

**Real-World Applications:**
These skills reflect real-world practices used by Technical Writers and DevOps Documentation Engineers who manage documentation using version control and static site generators instead of traditional word processors — directly transferable to maintaining internal wikis, open-source project docs, and API references in a CI/CD pipeline.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
