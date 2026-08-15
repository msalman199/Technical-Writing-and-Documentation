<div align="center">

# 🤖 Draft AI-Assisted Technical Documentation Prompts

![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Prompt Engineering](https://img.shields.io/badge/Prompt%20Engineering-8A2BE2?style=for-the-badge)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![Technical Writing](https://img.shields.io/badge/Technical%20Writing-4B8BBE?style=for-the-badge)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Objectives](#-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Environment Setup](#️-environment-setup)
- [🚀 Tasks](#-tasks)
  - [Task 1: 📝 Create Your First Prompt Template — Release Notes](#task-1-📝-create-your-first-prompt-template--release-notes)
  - [Task 2: 🔍 Evaluate the Draft](#task-2-🔍-evaluate-the-draft)
  - [Task 3: 🔁 Iterate on the Prompt (3 Variations)](#task-3-🔁-iterate-on-the-prompt-3-variations)
  - [Task 4: 📚 Build a Reusable Prompt Library (5 Document Types)](#task-4-📚-build-a-reusable-prompt-library-5-document-types)
  - [Task 5: ✅ Create a Human Review Checklist](#task-5-✅-create-a-human-review-checklist)
- [✅ Verification](#-verification)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Set up a local LLM environment using Ollama on Linux |
| 2 | Design structured prompts for generating technical documentation |
| 3 | Iteratively refine prompts to improve AI output quality |
| 4 | Build a reusable prompt library for five common documentation types |
| 5 | Create a human review checklist to validate AI-generated content |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| Terminal familiarity | Basic Linux command-line familiarity (navigating directories, running scripts) |
| Documentation background | Basic understanding of technical documentation types (release notes, manuals, FAQs) |
| AI/LLM experience | No prior experience required, but familiarity with prompt engineering concepts is helpful |
| Machine | Single Linux machine (Ubuntu 22.04+ recommended) with sudo access and internet connectivity |

---

## 🖥️ Environment Setup

> Your Al Nafi Start Lab provides a **single Linux machine**. Perform the following setup.

```bash
# 🔄 Update system packages
sudo apt update && sudo apt upgrade -y

# 📦 Install curl if not present
sudo apt install -y curl

# ⬇️ Install Ollama (local LLM runtime)
curl -fsSL https://ollama.com/install.sh | sh

# ✅ Verify installation
ollama --version
```

Pull a small, fast model suitable for text generation:

```bash
# ⬇️ Pull a lightweight model (~2-4GB)
ollama pull llama3.2:3b

# 🧪 Test the model
ollama run llama3.2:3b "Write a one-line greeting."
```

Create a working directory for your prompt library:

```bash
# 📁 Create the prompt library folder structure
mkdir -p ~/doc-prompts/{release-notes,user-manual,faq,troubleshooting,changelog,api-overview,reviews}
cd ~/doc-prompts
```

---

## 🚀 Tasks

### Task 1: 📝 Create Your First Prompt Template — Release Notes

Create a file to store your prompt template.

```bash
# ✏️ Open a new prompt template file
nano release-notes/prompt_template.txt
```

Fill in the template using this structure (complete the bracketed sections):

```text
ROLE: You are a technical writer creating software release notes.

AUDIENCE: [Define audience — e.g., end users, developers, IT admins]

TONE: [Define tone — e.g., professional, concise, friendly]

STRUCTURE:
- Title and version number
- Summary (2-3 sentences)
- New Features (bulleted)
- Bug Fixes (bulleted)
- Known Issues (bulleted)
- Upgrade Instructions

INPUT DATA:
[Paste raw changelog/feature list here]

TASK: Generate release notes following the structure above.
```

Save the file, then generate output by piping it into Ollama:

```bash
# TODO: Fill in raw feature/bug data below before running
cat release-notes/prompt_template.txt | ollama run llama3.2:3b > release-notes/draft_v1.md

cat release-notes/draft_v1.md
```

---

### Task 2: 🔍 Evaluate the Draft

Create an evaluation notes file and manually assess the output:

```bash
# ✏️ Open a new evaluation notes file
nano release-notes/evaluation_v1.md
```

Answer these questions in the file:

- **Clarity:** Is the language clear and unambiguous?
- **Accuracy:** Does it correctly reflect the input data (no invented features)?
- **Completeness:** Are all required sections present?
- **Tone match:** Does it match the audience/tone specified?

---

### Task 3: 🔁 Iterate on the Prompt (3 Variations)

Refine your prompt at least three times, saving each version separately.

```bash
cp release-notes/prompt_template.txt release-notes/prompt_v2.txt
# TODO: Edit prompt_v2.txt — e.g., add explicit word limit, add example output
nano release-notes/prompt_v2.txt

cat release-notes/prompt_v2.txt | ollama run llama3.2:3b > release-notes/draft_v2.md
```

Repeat for `prompt_v3.txt`. Suggested refinement strategies for each version:

| Version | Refinement Focus |
|---------|-------------------|
| v1 | Baseline structure only |
| v2 | Add explicit tone examples + word count limit |
| v3 | Add a "few-shot" example of ideal output inside the prompt |

```bash
cp release-notes/prompt_v2.txt release-notes/prompt_v3.txt
# TODO: Add a sample release note snippet as a "few-shot example" inside the prompt
nano release-notes/prompt_v3.txt

cat release-notes/prompt_v3.txt | ollama run llama3.2:3b > release-notes/draft_v3.md
```

Compare all three drafts and note improvements in `evaluation_v1.md`.

---

### Task 4: 📚 Build a Reusable Prompt Library (5 Document Types)

For each remaining document type, create a prompt template file following the same ROLE/AUDIENCE/TONE/STRUCTURE/INPUT/TASK format used in Task 1.

```bash
# ✏️ Open the user-manual prompt template
nano user-manual/prompt_template.txt
```

```text
ROLE: You are a technical writer creating a user manual section.
AUDIENCE: [TODO]
TONE: [TODO]
STRUCTURE:
- Section heading
- Purpose statement
- Step-by-step instructions (numbered)
- Tips/warnings callout
INPUT DATA: [TODO — paste feature description]
TASK: Generate the manual section following the structure above.
```

Repeat this pattern for the remaining four types — create and complete:

- `faq/prompt_template.txt` (structure: Question/Answer pairs grouped by topic)
- `troubleshooting/prompt_template.txt` (structure: Symptom, Cause, Resolution steps)
- `changelog/prompt_template.txt` (structure: Version, Date, Added/Changed/Fixed/Removed)
- `api-overview/prompt_template.txt` (structure: Endpoint, Method, Parameters, Example request/response)

Generate a sample draft for each using Ollama:

```bash
# TODO: Repeat for faq, troubleshooting, changelog, api-overview
cat user-manual/prompt_template.txt | ollama run llama3.2:3b > user-manual/draft_v1.md
```

---

### Task 5: ✅ Create a Human Review Checklist

```bash
# ✏️ Open a new review checklist file
nano reviews/checklist.md
```

Build a checklist covering at minimum these categories (complete each with 2-3 concrete checks):

```markdown
# AI-Generated Documentation Review Checklist

## Accuracy
- [ ] TODO: Verify facts against source material
- [ ] TODO: Check no hallucinated features/functions

## Clarity
- [ ] TODO: ...

## Tone & Audience Fit
- [ ] TODO: ...

## Structure & Completeness
- [ ] TODO: ...

## Compliance & Sensitivity
- [ ] TODO: Check for region-specific terminology (GCC/global audience)
```

---

## ✅ Verification

Confirm your work is complete by running:

```bash
# ✅ Verify Ollama is installed and model is available
ollama list

# 📂 Verify directory structure and file counts
find ~/doc-prompts -type f -name "*.txt" -o -name "*.md" | sort

# Expected: at least 3 release-notes prompt versions, 5 document-type
# prompt templates, and 1 checklist file
ls ~/doc-prompts/release-notes/
ls ~/doc-prompts/reviews/
```

**Expected outcomes:**
- `release-notes/` contains `prompt_v1` through `prompt_v3` and matching drafts
- Five subdirectories each contain a completed `prompt_template.txt` and at least one draft
- `reviews/checklist.md` contains a completed, non-empty checklist

---

## 🛠️ Troubleshooting

<details>
<summary>Click to expand common issues and fixes</summary>

- **Ollama command not found:** Restart terminal or run `source ~/.bashrc`; verify install script completed without errors.
- **Model pull fails/slow:** Check internet connection; retry `ollama pull llama3.2:3b`.
- **Ollama service not running:** Run `ollama serve` in a separate terminal session.
- **Output too generic/inaccurate:** Add more specific INPUT DATA and constraints to the prompt (Task 3 iteration).

</details>

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **Local LLM Runtime** | A model server (Ollama) running entirely on-device — no data leaves the machine |
| **Structured Prompt** | A template with fixed fields (ROLE/AUDIENCE/TONE/STRUCTURE/INPUT/TASK) for repeatable output |
| **Prompt Iteration** | Systematically refining a prompt across versions to improve clarity, tone, or accuracy |
| **Few-Shot Example** | Including a sample of the desired output inside the prompt to guide the model's style |
| **Prompt Library** | A reusable set of templates covering common documentation types across a team |
| **Human Review Checklist** | A validation gate ensuring AI-generated content is accurate, on-tone, and complete before publishing |

---

## 🎯 Conclusion

In this lab, you set up a local LLM environment using Ollama and used it to draft, evaluate, and iteratively refine AI-generated technical documentation. You built a structured prompt template for release notes, tested three refinement iterations, and extended this approach into a reusable prompt library covering five core documentation types: user manuals, FAQs, troubleshooting guides, changelogs, and API overviews. Finally, you created a human review checklist to ensure AI-generated content meets standards for accuracy, clarity, tone, and completeness before publication.

**Key Accomplishments:**
- ✅ Installed and configured a local LLM runtime (Ollama) on Linux
- ✅ Designed a structured, reusable prompt template format
- ✅ Iteratively refined a prompt across three versions and compared outputs
- ✅ Built a five-document-type prompt library (manuals, FAQs, troubleshooting, changelogs, API overviews)
- ✅ Created a human review checklist for accuracy, clarity, tone, and completeness

**Real-World Applications:**
These skills form a practical foundation for AI-assisted technical writing workflows used by Technical Writers and AI Content Specialists — directly transferable to scaling documentation output while keeping a human-in-the-loop review gate for accuracy and tone.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
