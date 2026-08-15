<div align="center">

# 📘 Write a Structured Technical User Guide in Markdown

![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![Pandoc](https://img.shields.io/badge/Pandoc-1A1A1A?style=for-the-badge&logo=pandoc&logoColor=white)
![Technical Writing](https://img.shields.io/badge/Technical%20Writing-4B8BBE?style=for-the-badge)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Learning Objectives](#-learning-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Lab Environment](#️-lab-environment)
- [🚀 Tasks](#-tasks)
  - [Task 1: 📝 Install a Markdown Editor](#task-1-📝-install-a-markdown-editor)
  - [Task 2: 🎯 Define Target Audience](#task-2-🎯-define-target-audience)
  - [Task 3: 🗂️ Draft the User Guide Outline](#task-3-🗂️-draft-the-user-guide-outline)
  - [Task 4: ⚙️ Write Installation and Usage Sections](#task-4-⚙️-write-installation-and-usage-sections)
  - [Task 5: 🔗 Add Glossary and Cross-References](#task-5-🔗-add-glossary-and-cross-references)
  - [Task 6: 🔍 Check Readability](#task-6-🔍-check-readability)
  - [Task 7: 🌐 Export Markdown to HTML](#task-7-🌐-export-markdown-to-html)
- [✅ Verification](#-verification)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Learning Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Install and use a Markdown editor on Linux |
| 2 | Analyze a target audience for technical documentation |
| 3 | Structure a user guide with standard sections |
| 4 | Write clear installation and usage instructions using plain language |
| 5 | Add a glossary and cross-reference links in Markdown |
| 6 | Check and improve document readability |
| 7 | Convert a Markdown file to HTML |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| Terminal familiarity | Basic comfort opening a terminal and running simple commands |
| Prior experience | No prior technical writing experience required |
| Machine | A single Linux machine (provided via Start Lab) |
| Network | Internet connection for installing packages |

---

## 🖥️ Lab Environment

> This lab uses a **single Linux machine** provided by Al Nafi via Start Lab. No cloud services or external accounts are required. All tools used are free and open-source.

Open a terminal on your lab machine before starting Task 1.

---

## 🚀 Tasks

### Task 1: 📝 Install a Markdown Editor

We will use VS Code with the built-in Markdown Preview feature (no extra extension required for basic preview).

```bash
# 🔄 Update package lists
sudo apt update

# 📦 Install required dependencies
sudo apt install -y wget gpg apt-transport-https

# ⬇️ Download and install VS Code (Debian/Ubuntu-based systems)
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install -y code
```

Verify installation:

```bash
# ✅ Confirm VS Code installed correctly
code --version
```

**Expected outcome:** You should see three lines of output (version number, commit hash, architecture).

> 💡 **Tip:** If the `code` command is unavailable, restart your terminal session.

---

### Task 2: 🎯 Define Target Audience

Create a working directory and an audience analysis file for a sample CLI tool (we will document a fictional tool called `filetool`).

```bash
# 📁 Create project folder
mkdir -p ~/user-guide-lab
cd ~/user-guide-lab

# 🆕 Create audience analysis file
touch audience-analysis.md
```

Open `audience-analysis.md` in VS Code:

```bash
# ✏️ Open the file for editing
code audience-analysis.md
```

Add the following content (fill in the blanks yourself):

```markdown
# Audience Analysis: filetool CLI

- **Primary audience:** _(e.g., junior developers, sysadmins)_
- **Technical skill level:** _(beginner / intermediate / advanced)_
- **Goals:** What does the reader want to achieve with filetool?
- **Environment:** Operating system, terminal familiarity
- **Pain points:** What confuses new users of CLI tools?
```

Save the file (`Ctrl+S`).

---

### Task 3: 🗂️ Draft the User Guide Outline

Create the main guide file:

```bash
# 🆕 Create and open the user guide file
touch user-guide.md
code user-guide.md
```

Add this outline skeleton — fill in placeholder text where indicated:

```markdown
# filetool User Guide

## Introduction
<!-- TODO: One paragraph describing what filetool does -->

## Prerequisites
<!-- TODO: List required software/OS -->

## Installation
<!-- TODO: Step-by-step install instructions -->

## Usage
<!-- TODO: Numbered steps showing common commands -->

## Troubleshooting
<!-- TODO: Common errors and fixes -->

## FAQ
<!-- TODO: 3-5 question/answer pairs -->

## Glossary
<!-- TODO: Key terms and definitions -->
```

Save the file.

---

### Task 4: ⚙️ Write Installation and Usage Sections

Replace the placeholders in the Installation and Usage sections using plain language and active voice.

Example pattern to follow:

```markdown
## Installation

1. Open a terminal.
2. Run the following command to install filetool:
   ```bash
   sudo apt install filetool
   ```
3. Confirm the installation:
   ```bash
   filetool --version
   ```

> **Note:** If the command is not found, check that `/usr/local/bin` is in your PATH.

## Usage

1. Run `filetool list` to view all files in the current directory.
2. Run `filetool rename old.txt new.txt` to rename a file.
3. Run `filetool --help` to see all available options.
```

Use **active voice** ("Run the command" not "The command should be run") and **numbered steps** for procedures.

**Callout box syntax reminder** (Markdown blockquote used as a note/warning):

```markdown
> **Warning:** Back up your files before running batch operations.
```

---

### Task 5: 🔗 Add Glossary and Cross-References

Update the Glossary section:

```markdown
## Glossary

- **CLI**: Command Line Interface, a text-based way to interact with software.
- **Flag**: An optional parameter (e.g., `--help`) that modifies command behavior.
- **PATH**: An environment variable listing directories the shell searches for executables.
```

Add cross-reference links between sections using Markdown anchor links:

```markdown
See the [Installation](#installation) section before proceeding to [Usage](#usage).

Refer to the [Glossary](#glossary) for term definitions.
```

> 💡 **Tip:** Markdown anchors are auto-generated from headings — lowercase, spaces replaced with hyphens.

---

### Task 6: 🔍 Check Readability

Install a simple local readability tool (`write-good`, an open-source npm-based prose linter):

```bash
# 📦 Install Node.js and npm if not already installed
sudo apt install -y nodejs npm

# 📦 Install write-good globally
sudo npm install -g write-good
```

Run it against your guide:

```bash
# 🔍 Lint the user guide for wordy/passive phrasing
write-good user-guide.md
```

**Expected outcome:** Terminal prints suggestions (e.g., passive voice, wordy phrases) or nothing if the text is clean.

Revise flagged sentences in `user-guide.md` to be shorter and more direct. Re-run `write-good` until output is minimal.

---

### Task 7: 🌐 Export Markdown to HTML

Install `pandoc`, an open-source document converter:

```bash
# 📦 Install pandoc
sudo apt install -y pandoc
```

Convert your guide:

```bash
# 🔄 Convert Markdown to HTML
pandoc user-guide.md -o user-guide.html
```

Open the HTML file in a browser to verify formatting:

```bash
# 🌐 Open the converted file in the default browser
xdg-open user-guide.html
```

**Expected outcome:** A browser tab opens showing your formatted guide with headings, lists, and blockquotes rendered correctly.

**Troubleshooting:**
- If `xdg-open` fails, manually navigate to the file path in your file manager or run `firefox user-guide.html`.
- If headings look unstyled, this is normal for plain pandoc output — formatting is minimal by default.

---

## ✅ Verification

Confirm your lab is complete by checking the following on your machine:

```bash
# 📂 Confirm all files exist
ls ~/user-guide-lab
# Expected: audience-analysis.md  user-guide.md  user-guide.html

# ✅ Confirm VS Code is installed
code --version

# ✅ Confirm pandoc conversion worked
file user-guide.html
# Expected output includes: HTML document text
```

- [ ] `user-guide.md` contains all six sections (Introduction, Prerequisites, Installation, Usage, Troubleshooting, FAQ) plus Glossary
- [ ] `write-good` runs without major warnings
- [ ] `user-guide.html` opens correctly in a browser

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **Markdown** | Lightweight plain-text markup language used to structure documentation |
| **Audience Analysis** | Identifying the reader's skill level, goals, and pain points before writing |
| **Active Voice** | Writing style where the subject performs the action ("Run the command") — clearer than passive voice |
| **Cross-Reference Links** | Markdown anchor links (`#heading-name`) that let readers jump between sections |
| **Readability Linting** | Automated checking (e.g., `write-good`) for passive voice, wordy phrases, and clarity issues |
| **Pandoc** | Open-source universal document converter, used here to render Markdown as HTML |

---

## 🎯 Conclusion

In this lab, you installed a Markdown editor on a Linux machine, analyzed a target audience, and drafted a structured technical user guide with standard sections (Introduction, Prerequisites, Installation, Usage, Troubleshooting, FAQ, and Glossary). You practiced writing in plain language and active voice, added cross-reference links, checked readability with an open-source linter, and exported your final document to HTML for verification.

**Key Accomplishments:**
- ✅ Installed and configured a Markdown editor (VS Code) on Linux
- ✅ Produced a target-audience analysis for a sample CLI tool
- ✅ Structured a complete user guide skeleton with all standard sections
- ✅ Wrote installation and usage instructions in plain, active-voice language
- ✅ Added a glossary and Markdown cross-reference links
- ✅ Ran and responded to automated readability feedback
- ✅ Converted the final Markdown document to HTML with Pandoc

**Real-World Applications:**
These skills form the foundation of professional technical writing and align with the STC CPTC Foundation-level competencies in document structure and clarity — directly applicable to writing README files, API documentation, onboarding guides, and internal runbooks in any engineering or DevOps role.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
