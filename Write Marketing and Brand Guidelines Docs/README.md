<div align="center">

# 🎨 Write Marketing and Brand Guidelines Docs

![LibreOffice](https://img.shields.io/badge/LibreOffice-18A303?style=for-the-badge&logo=libreofficewriter&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![PDF](https://img.shields.io/badge/PDF%20Export-EC1C24?style=for-the-badge&logo=adobeacrobatreader&logoColor=white)
![Brand Guidelines](https://img.shields.io/badge/Brand%20Guidelines-4B8BBE?style=for-the-badge)
![Marketing](https://img.shields.io/badge/Marketing%20Copy-FF6F61?style=for-the-badge)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Objectives](#-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Environment Setup](#️-environment-setup)
- [🚀 Tasks](#-tasks)
  - [Task 1: 📈 Draft the Marketing Strategy Document](#task-1-📈-draft-the-marketing-strategy-document)
  - [Task 2: 🎨 Create the Brand Guidelines Document](#task-2-🎨-create-the-brand-guidelines-document)
  - [Task 3: 📱 Write Sample Social Media Copy](#task-3-📱-write-sample-social-media-copy)
  - [Task 4: 📖 Build the Content Style Guide Appendix](#task-4-📖-build-the-content-style-guide-appendix)
  - [Task 5: ✅ Review Using the Quality Checklist](#task-5-✅-review-using-the-quality-checklist)
  - [Task 6: 📤 Export Documents as PDF](#task-6-📤-export-documents-as-pdf)
- [✅ Verification](#-verification)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Draft a one-page marketing strategy document with clear structure |
| 2 | Create a brand guidelines document covering visual and verbal identity |
| 3 | Write sample social media copy aligned with brand tone |
| 4 | Build a content style guide appendix for terminology and formatting |
| 5 | Review documents using a quality checklist |
| 6 | Export final documents as PDF using local tools |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| Computer literacy | Basic computer literacy (typing, saving files, opening applications) |
| Prior experience | No prior marketing or writing experience required |
| Machine | A single Linux machine (provided via Start Lab) |
| Network | Internet access for installing tools |

---

## 🖥️ Environment Setup

Launch your Al Nafi Start Lab Linux machine.

Open a terminal and install LibreOffice (if not pre-installed):

```bash
# 🔄 Update package list
sudo apt update

# 📦 Install LibreOffice Writer for document creation
sudo apt install -y libreoffice-writer

# ✅ Verify installation
libreoffice --version
```

Create a working folder for this lab:

```bash
# 📁 Create and move into a project folder
mkdir -p ~/marketing-docs && cd ~/marketing-docs
```

Open LibreOffice Writer from the terminal:

```bash
# ✏️ Launch LibreOffice Writer
libreoffice --writer &
```

---

## 🚀 Tasks

### Task 1: 📈 Draft the Marketing Strategy Document

In LibreOffice Writer, create a new file: `marketing-strategy.odt`

Add the following headings (use **Heading 1** style for each):
- Objectives
- Target Audience
- Channels
- KPIs
- Timeline

Under each heading, write 2-3 sentences. Use this template as a guide:

```text
Objectives:
- TODO: State the main goal (e.g., "Increase brand awareness in GCC markets by 20% in Q3")

Target Audience:
- TODO: Describe demographics, region, and buyer type
  (e.g., "SMEs in UAE and Saudi Arabia, decision-makers aged 30-50")

Channels:
- TODO: List 2-3 channels (e.g., LinkedIn, Instagram, Email Newsletter)

KPIs:
- TODO: List measurable indicators (e.g., "500 new leads, 10% engagement rate")

Timeline:
- TODO: Add a simple 3-month plan with milestones
```

Save the file: `File > Save As > marketing-strategy.odt`

---

### Task 2: 🎨 Create the Brand Guidelines Document

Create a new file: `brand-guidelines.odt`

Add these section headings:
- Logo Usage
- Color Palette
- Typography
- Tone of Voice
- Do's and Don'ts

Fill in each section using this scaffold:

```text
Logo Usage:
- TODO: Describe minimum size, clear space rules, and placement
  Example: "Logo must have 10px clear space on all sides. Do not stretch."

Color Palette:
- TODO: List primary and secondary colors with hex codes
  Example: Primary Blue #1A4E8A, Secondary Gold #D4A017

Typography:
- TODO: Name the fonts for headings and body text
  Example: Headings - Montserrat Bold; Body - Open Sans Regular

Tone of Voice:
- TODO: Describe 3 tone traits (e.g., "Professional, Approachable, Confident")

Do's and Don'ts:
- Do: Use approved colors and fonts only
- Do: Keep messaging consistent across regions
- Don't: Alter the logo proportions
- Don't: Use informal slang in official communications
```

Save the file: `File > Save As > brand-guidelines.odt`

> 💡 **Optional visual step:** Use Canva (web browser) to create a simple logo color swatch or typography sample image, then insert it into your `brand-guidelines.odt` using `Insert > Image`.

---

### Task 3: 📱 Write Sample Social Media Copy

Create a new file: `social-media-samples.odt`

Write 3 short social media posts (Twitter/X style, under 280 characters) that follow the tone described in Task 2.

```text
Post 1 (Announcement):
TODO: Write a post announcing a new product/service

Post 2 (Engagement):
TODO: Write a post asking a question to your audience

Post 3 (Promotional):
TODO: Write a post promoting a discount or event
```

Below each post, add a one-line note explaining how it matches your Tone of Voice section.

> Example note: *"This post uses confident, direct language matching our brand tone."*

---

### Task 4: 📖 Build the Content Style Guide Appendix

In `brand-guidelines.odt`, add a new section at the end titled **Appendix: Style Guide**

Fill in this template:

```text
Approved Terminology:
- TODO: List 3-5 approved terms/phrases (e.g., use "clients" not "customers")

Formatting Rules:
- TODO: Define heading capitalization (e.g., Title Case for headings)
- TODO: Define number formatting (e.g., spell out numbers one-nine, use digits 10+)
- TODO: Define date format (e.g., DD-MM-YYYY for GCC alignment)
```

---

### Task 5: ✅ Review Using the Quality Checklist

Use this checklist to review both documents. Mark each item Yes/No in a new file `review-checklist.txt`:

```bash
# 📝 Create the checklist file in terminal
cat > ~/marketing-docs/review-checklist.txt << 'EOF'
Marketing Documentation Quality Checklist
------------------------------------------
[ ] All required sections are present
[ ] Language is clear and free of jargon
[ ] Tone is consistent across all documents
[ ] Colors and fonts match the brand palette
[ ] KPIs are measurable and specific
[ ] No spelling or grammar errors
[ ] Terminology matches the style guide appendix
EOF

# 👀 View the checklist
cat ~/marketing-docs/review-checklist.txt
```

Open the file in a text editor, mark each box, and save.

---

### Task 6: 📤 Export Documents as PDF

In LibreOffice Writer, open each `.odt` file, then go to `File > Export As > Export as PDF` for each document. Save PDFs in your working folder.

Alternatively, export from the terminal using LibreOffice headless mode:

```bash
# 🔄 Convert all .odt files in the folder to PDF
libreoffice --headless --convert-to pdf ~/marketing-docs/*.odt --outdir ~/marketing-docs/
```

---

## ✅ Verification

Run these commands to confirm all deliverables exist:

```bash
# 📂 List all files created in the lab
ls -l ~/marketing-docs/

# 📄 Confirm PDF exports exist
ls ~/marketing-docs/*.pdf
```

**Expected output should show:**
- `marketing-strategy.odt` and `marketing-strategy.pdf`
- `brand-guidelines.odt` and `brand-guidelines.pdf`
- `social-media-samples.odt` and `.pdf`
- `review-checklist.txt`

---

## 🛠️ Troubleshooting

<details>
<summary>Click to expand common issues and fixes</summary>

- **LibreOffice won't open:** Run `sudo apt install -y libreoffice` for the full suite.
- **PDF export command fails:** Ensure filenames have no spaces; use hyphens instead.
- **Headless conversion produces no output:** Check you are in the correct directory using `pwd` and `ls`.
- **Text formatting lost after save:** Always use "Save As" with `.odt` format, not `.txt`.

</details>

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **Marketing Strategy Brief** | A one-page document defining objectives, audience, channels, KPIs, and timeline |
| **Brand Guidelines** | A reference document standardizing visual identity (logo, color, typography) and verbal tone |
| **Tone of Voice** | A defined set of personality traits (e.g., professional, approachable) that shapes all brand copy |
| **Style Guide Appendix** | A terminology and formatting reference that keeps content consistent across writers |
| **Headless Conversion** | Running LibreOffice without a GUI (`--headless`) to batch-convert documents from the command line |
| **Quality Checklist Review** | A structured pass/fail review gate applied before content is considered publish-ready |

---

## 🎯 Conclusion

In this lab, you practiced creating core marketing documentation used by Content Strategists and Marketing Documentation Writers. You drafted a one-page marketing strategy brief, built a complete brand guidelines document with visual and verbal identity rules, wrote sample social media copy aligned with brand tone, and created a style guide appendix for consistent terminology. You also reviewed your work against a quality checklist and exported all documents as PDFs using LibreOffice, a free and open-source tool.

**Key Accomplishments:**
- ✅ Drafted a structured one-page marketing strategy document
- ✅ Built a complete brand guidelines document (logo, color, typography, tone, do's/don'ts)
- ✅ Wrote three on-brand social media posts with tone-matching notes
- ✅ Created a terminology and formatting style guide appendix
- ✅ Reviewed both documents against a 7-point quality checklist
- ✅ Exported all deliverables to PDF using LibreOffice headless conversion

**Real-World Applications:**
These skills directly apply to real-world brand documentation tasks for GCC and global enterprises — directly transferable to onboarding new marketing hires, briefing external agencies, and keeping multi-writer content teams consistent across campaigns.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
