<div align="center">

# 🤖 Automate Doc Generation with AI and Templates

![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

*A design-brief lab: architect a template-driven, AI-powered documentation pipeline from scratch*

</div>

---

## 📖 Table of Contents

- [🎯 Objectives](#-objectives)
- [📋 Prerequisites](#-prerequisites)
- [🖥️ Lab Environment](#️-lab-environment)
- [🏗️ Task 1: Design the Template and Config Architecture](#️-task-1-design-the-template-and-config-architecture)
- [⚙️ Task 2: Build the Generation Pipeline Script](#️-task-2-build-the-generation-pipeline-script)
- [🚦 Task 3: Quality Gate and Batch Execution](#-task-3-quality-gate-and-batch-execution)
- [📘 Task 4: Documentation, Versioning, and Handoff](#-task-4-documentation-versioning-and-handoff)
- [✅ Verification](#-verification)
- [🔑 Key Concepts](#-key-concepts)
- [🏁 Conclusion](#-conclusion)

---

## 🎯 Objectives

| # | By the end of this lab, you will... |
|---|---|
| 1 | Design a template-driven documentation pipeline combining Markdown templates, shell scripting, and local AI generation |
| 2 | Integrate Ollama (local LLM) into an automated content-generation workflow |
| 3 | Build a config-driven variable substitution system for document metadata |
| 4 | Implement automated linting and quality gates in a documentation pipeline |
| 5 | Produce a maintainer-facing runbook for the automation system |
| 6 | Manage the pipeline as a versioned, reproducible artifact in Git |

## 📋 Prerequisites

| Requirement | Details |
|---|---|
| Linux CLI | Strong proficiency — bash scripting, process substitution, piping, `sed`/`awk` |
| Git | Working knowledge — branching, commits, `.gitignore` |
| Markdown / config formats | Familiarity with Markdown syntax and YAML/INI config formats |
| LLM prompting | Basic exposure — system/user prompts, context windows |
| General troubleshooting | Comfort installing and troubleshooting packages independently |

## 🖥️ Lab Environment

> Al Nafi provides a single Linux machine (Ubuntu) via **Start Lab**.

```bash
# 📦 Update system and install core dependencies
sudo apt update && sudo apt install -y git curl jq nodejs npm

# 🧹 Install markdownlint CLI
sudo npm install -g markdownlint-cli

# 🦙 Install Ollama (local LLM runtime)
curl -fsSL https://ollama.com/install.sh | sh
ollama --version

# 📥 Pull a lightweight model suited to CPU-only environments
ollama pull llama3.2:1b
```

- Verify Ollama service is running: `systemctl status ollama` or `ollama list`
- Confirm `markdownlint --version` and `git --version` succeed

---

## 🏗️ Task 1: Design the Template and Config Architecture
**⏱️ 45–60 min**

Build a repository structure that separates templates, configuration, generated output, and automation logic.

**Requirements:**
- Three Markdown templates with placeholder syntax of your choice (e.g. `{{VERSION}}`, `{{DATE}}`, `{{AUTHOR}}`, `{{AI_BODY}}`):
  - `templates/release_notes.md`
  - `templates/api_changelog.md`
  - `templates/meeting_minutes.md`
- A single config file (`config/doc.conf` — YAML, JSON, or `.env` style; justify your choice) holding: `version`, `date`, `author`, `doc_type`, and an `ai_prompt` field per document type
- Directory layout supporting multiple generated batches (e.g. `output/<timestamp>/`)

**🧭 Architecture decision points to resolve yourself:**
- How will the script know which template maps to which config entry?
- How will you handle missing/malformed config values (fail-fast vs. defaults)?
- Placeholder syntax must not collide with legitimate Markdown syntax

```markdown
<!-- templates/release_notes.md skeleton -->
# Release Notes — v{{VERSION}}
**Date:** {{DATE}}  |  **Author:** {{AUTHOR}}

## Summary
{{AI_BODY}}
```

---

## ⚙️ Task 2: Build the Generation Pipeline Script
**⏱️ 60–75 min**

Write `generate_docs.sh` that orchestrates the full pipeline: config parsing → variable substitution → AI content injection → linting → output.

**Function contract** (design your own implementation):

```bash
#!/usr/bin/env bash
# generate_docs.sh

# 🧩 load_config(): parse config/doc.conf into shell variables or an assoc array
load_config() { :; }

# 🖋️ render_template(template_path, output_path): substitute {{VAR}} placeholders
render_template() { :; }

# 🦙 generate_ai_content(prompt, model): call Ollama, return generated text
# Contract: must not leave prompt/response artifacts in the final doc
generate_ai_content() { :; }

# 🔍 lint_document(file_path): run markdownlint, return 0/nonzero
lint_document() { :; }

# 🚀 main(): sequence the pipeline for all three doc types, write to output/<ts>/
main() { :; }

main "$@"
```

**Integration requirements:**
- Use `ollama run <model> "<prompt>"` (or the REST API on `localhost:11434/api/generate`) to fetch AI content — choose based on reliability/latency tradeoffs and document your choice
- Sanitize AI output (strip markdown code fences the model may add, trim excess whitespace) before injection
- Use `sed`, `awk`, or `envsubst` for substitution — justify performance/safety tradeoffs (e.g. `sed` delimiter collisions with `/` in text)
- Script must exit non-zero if linting fails on any generated document, and must log which document failed and why

---

## 🚦 Task 3: Quality Gate and Batch Execution
**⏱️ 30–45 min**

- Create a `.markdownlint.json` config enforcing at least 4 custom rules (e.g. heading style, line length, no trailing spaces, ordered list style)
- Run the pipeline to generate one instance each of Release Notes, API Changelog, and Meeting Minutes in a single batch
- Handle lint failures programmatically: on failure, either auto-fix (`markdownlint --fix`) or halt and report — **implement one approach and justify it**
- Manually review all three generated documents for factual/structural correctness against your config inputs; log discrepancies in a `review_notes.md`

---

## 📘 Task 4: Documentation, Versioning, and Handoff
**⏱️ 30–45 min**

- Write `RUNBOOK.md` for future maintainers covering: architecture overview, how to add a new document type, how to swap the LLM model, known limitations, and troubleshooting steps for common failures (Ollama not responding, lint failures, malformed config)
- Initialize a local Git repository for the entire pipeline (templates, script, configs, lint rules, runbook)
- Use meaningful commit history (minimum 4 logical commits — e.g. templates, script, lint integration, docs) rather than a single commit
- Add a `.gitignore` excluding generated `output/` artifacts and any local model cache paths

---

## ✅ Verification

Confirm the following on your machine:

```bash
# 🚀 Pipeline executes end-to-end without manual intervention
./generate_docs.sh && echo "Pipeline exit: $?"

# 📄 Three documents exist in the latest output batch
ls output/*/*.md | wc -l   # expect 3

# 🔍 All generated docs pass linting
markdownlint output/*/*.md

# 🕒 Git history reflects staged, logical development
git log --oneline

# 📘 Runbook exists and covers required sections
grep -E "Architecture|Add a new document type|Troubleshooting" RUNBOOK.md
```

**Expected outcomes:**
- Successful run produces exactly 3 lint-clean Markdown files with correctly substituted variables and non-empty AI-generated bodies
- Re-running with a different config (e.g. new version/date) produces a distinct, correctly updated batch

---

## 🔑 Key Concepts

| Concept | Description |
|---|---|
| Template-Driven Documentation | Separating structure (templates) from content (config + AI) for reusable doc generation |
| Config-Driven Variable Substitution | Injecting metadata (version, date, author) into templates via a single source of truth |
| Local LLM Integration | Using Ollama to generate document content without external API dependencies |
| Quality Gates | Automated linting (markdownlint) as a pass/fail checkpoint before publishing |
| Runbook Documentation | Maintainer-facing docs covering architecture, extension points, and troubleshooting |
| Pipeline Versioning | Managing scripts, templates, configs, and docs as a reproducible Git artifact |

---

## 🏁 Conclusion

### 🎉 Key Accomplishments
- Architected and implemented an end-to-end documentation automation pipeline
- Unified structured templates, config-driven metadata substitution, local LLM content generation via Ollama, and automated quality gating with markdownlint
- Made independent architectural decisions around configuration formats, substitution mechanics, AI output sanitization, and failure-handling strategy
- Produced maintainer-facing documentation and version-controlled the entire system

### 💼 Real-World Applications
These skills are directly aligned with the **Documentation Automation Engineer** role, reflecting real-world practices for sustainable, scalable technical writing operations.

---

<div align="center">

![Al Nafi](https://img.shields.io/badge/Al%20Nafi-Cybersecurity%20Education-blue?style=for-the-badge)

</div>
