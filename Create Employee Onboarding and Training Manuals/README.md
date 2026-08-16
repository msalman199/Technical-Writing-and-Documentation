<div align="center">

# 📚 Create Employee Onboarding and Training Manuals

![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![Pandoc](https://img.shields.io/badge/Pandoc-1a1a1a?style=for-the-badge&logo=pandoc&logoColor=white)
![LaTeX](https://img.shields.io/badge/LaTeX-008080?style=for-the-badge&logo=latex&logoColor=white)
![ImageMagick](https://img.shields.io/badge/ImageMagick-00CCCC?style=for-the-badge&logo=imagemagick&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

*A hands-on lab for building a branded, accessible documentation package from raw Markdown*

</div>

---

## 📖 Table of Contents

- [🎯 Objectives](#-objectives)
- [📋 Prerequisites](#-prerequisites)
- [🖥️ Lab Environment](#️-lab-environment)
- [📝 Task 1: Outline the Onboarding Guide](#-task-1-outline-the-onboarding-guide)
- [🛠️ Task 2: Draft the Tools Setup Section](#️-task-2-draft-the-tools-setup-section)
- [📘 Task 3: Create the Training Manual](#-task-3-create-the-training-manual)
- [❓ Task 4: Add the Knowledge-Check Quiz](#-task-4-add-the-knowledge-check-quiz)
- [♿ Task 5: Accessibility Review](#-task-5-accessibility-review)
- [📄 Task 6: Compile into a Single PDF Package](#-task-6-compile-into-a-single-pdf-package)
- [✅ Verification](#-verification)
- [🔧 Troubleshooting](#-troubleshooting)
- [🔑 Key Concepts](#-key-concepts)
- [🏁 Conclusion](#-conclusion)

---

## 🎯 Objectives

| # | By the end of this lab, you will be able to... |
|---|---|
| 1 | Structure a multi-section employee onboarding guide using Markdown |
| 2 | Write clear, step-by-step technical instructions with visual aid placeholders |
| 3 | Build a standalone training manual with learning objectives, exercises, and a knowledge-check quiz |
| 4 | Apply accessibility best practices (alt-text, heading hierarchy, font readability) |
| 5 | Compile multiple Markdown documents into a single branded PDF documentation package |

## 📋 Prerequisites

| Requirement | Details |
|---|---|
| Markdown syntax | Basic familiarity — headings, lists, links, images |
| Linux terminal | Comfortable navigating directories and editing files |
| PDF tooling | No prior experience required — instructions provided |

## 🖥️ Lab Environment

> Al Nafi provides a single Linux machine via **Start Lab**. All tooling is installed and all work is performed on this one VM.

```bash
# 📦 Update package index and install required tools
sudo apt update
sudo apt install -y pandoc texlive-latex-base texlive-fonts-recommended imagemagick nano

# 📁 Create project directory structure
mkdir -p ~/onboarding-project/{docs,images,output}
cd ~/onboarding-project
```

Verify installation:

```bash
pandoc --version
```

---

## 📝 Task 1: Outline the Onboarding Guide

Create the onboarding guide skeleton with required sections.

```bash
# ✏️ Open the onboarding guide for editing
nano docs/onboarding-guide.md
```

Use this starter template — complete the `TODO` sections with realistic sample content for a fictional company:

```markdown
# Employee Onboarding Guide — [Company Name]

## 1. Welcome
<!-- TODO: Write a 2-3 sentence welcome message -->

## 2. Company Overview
<!-- TODO: Add mission, values, org structure summary -->

## 3. Role Expectations
<!-- TODO: List responsibilities and performance expectations -->

## 4. Tools Setup
<!-- Completed in Task 2 -->

## 5. Policies
<!-- TODO: Summarize leave policy, code of conduct, IT usage policy -->

## 6. First-Week Checklist
<!-- TODO: Add a Markdown checklist using - [ ] syntax -->
```

- Fill in each `TODO` with concise, realistic content (2-5 lines per section)
- Use `##` for section headers to maintain a clear heading hierarchy (H1 for title, H2 for sections)

---

## 🛠️ Task 2: Draft the Tools Setup Section

Generate placeholder "screenshots" using ImageMagick (simulating annotated tool screenshots):

```bash
# 🖼️ Create the first placeholder screenshot
convert -size 800x400 xc:lightgray -pointsize 24 -gravity center \
  -annotate 0 "Step 1: Login Screen" images/step1-login.png

# TODO: Create at least 2 more placeholder images for additional setup steps
# Example: convert -size 800x400 xc:lightgray -pointsize 24 -gravity center \
#   -annotate 0 "Step 2: <Your Label>" images/step2-<name>.png
```

Insert the Tools Setup section into `onboarding-guide.md`, replacing the placeholder comment:

```markdown
## 4. Tools Setup

### Step 1: Access the Company Portal
![Login screen showing username and password fields](images/step1-login.png "Company portal login page")

1. Navigate to `portal.company.com`
2. Enter your assigned credentials
<!-- TODO: Continue numbered steps referencing your additional images -->
```

> ⚠️ Every image must include descriptive alt-text in the brackets `[...]` — this is mandatory, not optional.

---

## 📘 Task 3: Create the Training Manual

Create a separate manual for a specific skill (example: using a project management tool like a Kanban board).

```bash
# ✏️ Open the training manual for editing
nano docs/training-manual.md
```

Starter template:

```markdown
# Training Manual: [Skill/Tool Name]

## Learning Objectives
By the end of this module, learners will be able to:
<!-- TODO: List 3 measurable objectives, e.g., "Create a new task card" -->

## Section 1: Getting Started
<!-- TODO: Step-by-step instructions -->

## Section 2: Core Exercise
<!-- TODO: Provide a hands-on exercise, e.g., "Create 3 tasks and move them across statuses" -->

## Knowledge Check
<!-- Completed in Task 4 -->
```

---

## ❓ Task 4: Add the Knowledge-Check Quiz

Append a quiz with at least 5 questions to `training-manual.md`. Use this format and complete it:

```markdown
## Knowledge Check

1. What is the primary purpose of [tool]?
   a) ___ b) ___ c) ___ d) ___

2. <!-- TODO: multiple choice question -->

3. <!-- TODO: true/false question -->

4. <!-- TODO: short answer question -->

5. <!-- TODO: scenario-based question -->

**Answer Key:** <!-- TODO: list correct answers -->
```

- Ensure question types vary (multiple choice, true/false, short answer, scenario) to test different comprehension levels

---

## ♿ Task 5: Accessibility Review

Manually audit both `.md` files against this checklist:

```bash
# 🔍 Search for images missing alt-text (empty brackets)
grep -n '!\[\]' docs/*.md

# 🔢 Verify heading hierarchy (no skipped levels, e.g., H1 -> H3)
grep -n '^#' docs/*.md
```

- Fix any image with empty `[]` alt-text
- Confirm heading order is sequential (`#` then `##` then `###`, no skipping)
- In your final PDF, standard fonts (e.g., default Pandoc/LaTeX serif) satisfy readability — do not use decorative fonts

---

## 📄 Task 6: Compile into a Single PDF Package

Combine both documents into one PDF using Pandoc.

```bash
cd ~/onboarding-project

# 📦 Compile onboarding guide + training manual into a single branded PDF
pandoc docs/onboarding-guide.md docs/training-manual.md \
  -o output/employee-documentation-package.pdf \
  --metadata title="Employee Onboarding & Training Package" \
  --toc \
  -V geometry:margin=1in
```

- `--toc` generates a table of contents from your headings — this only works correctly if heading hierarchy is clean (Task 5)
- If the build fails due to missing images, verify file paths are relative to `~/onboarding-project`

---

## ✅ Verification

Confirm successful completion on your Linux machine:

```bash
# 📏 Check PDF was generated and has reasonable size (not 0 bytes)
ls -lh output/employee-documentation-package.pdf

# 📄 Confirm page count (should be multiple pages given two documents)
pdfinfo output/employee-documentation-package.pdf | grep Pages

# 🔍 Re-check no missing alt-text remains
grep -c '!\[\]' docs/*.md
```

**Expected outcomes:**
- `employee-documentation-package.pdf` exists in `output/` with size > 20 KB
- PDF contains a table of contents, onboarding guide, and training manual with quiz
- `grep -c '!\[\]'` returns 0 for both files (no missing alt-text)

---

## 🔧 Troubleshooting

<details>
<summary>Click to expand common issues and fixes</summary>

| Issue | Fix |
|---|---|
| Pandoc PDF error (missing LaTeX package) | Run `sudo apt install -y texlive-latex-recommended` |
| Images not appearing in PDF | Confirm paths in Markdown are relative to the `.md` file location, not absolute paths |
| TOC not generating | Ensure headings use `#`/`##` syntax, not bold text mimicking headings |

</details>

---

## 🔑 Key Concepts

| Concept | Description |
|---|---|
| Markdown Document Structuring | Organizing multi-section technical content with a clean heading hierarchy |
| Accessibility (Alt-Text) | Ensuring every image includes descriptive alt-text for screen readers |
| Heading Hierarchy | Sequential heading levels (H1 → H2 → H3) required for valid navigation and TOC generation |
| Pandoc | Converting and compiling multiple Markdown files into a single formatted PDF |
| Table of Contents Generation | Auto-generating a navigable TOC from document headings via `--toc` |
| ImageMagick | Generating placeholder visual assets to simulate annotated screenshots |

---

## 🏁 Conclusion

### 🎉 Key Accomplishments
- Structured a multi-section onboarding guide from scratch using Markdown
- Documented a tools setup process with annotated visual aids
- Authored a skill-specific training manual with a knowledge-check quiz
- Audited both documents for accessibility compliance
- Compiled everything into a single professional PDF using Pandoc

### 💼 Real-World Applications
This workflow is directly applicable to real-world **Training Documentation Specialist** and **HR Technical Writer** roles.

---

<div align="center">

![Al Nafi](https://img.shields.io/badge/Al%20Nafi-Cybersecurity%20Education-blue?style=for-the-badge)

</div>
