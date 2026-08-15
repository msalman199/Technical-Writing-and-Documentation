<div align="center">

# 🗄️ Design a Knowledge Base with Notion-Style Tools

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![BookStack](https://img.shields.io/badge/BookStack-0288D1?style=for-the-badge&logo=bookstack&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Information Architecture](https://img.shields.io/badge/Information%20Architecture-4B8BBE?style=for-the-badge)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Objectives](#-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Environment Setup](#️-environment-setup)
- [🚀 Tasks](#-tasks)
  - [Task 1: 🐳 Deploy BookStack via Docker Compose](#task-1-🐳-deploy-bookstack-via-docker-compose)
  - [Task 2: 🗂️ Build the Information Architecture](#task-2-🗂️-build-the-information-architecture)
  - [Task 3: 🧭 Landing Page, Navigation, and Cross-Linking](#task-3-🧭-landing-page-navigation-and-cross-linking)
  - [Task 4: 🧪 Usability Testing (First-Time User Simulation)](#task-4-🧪-usability-testing-first-time-user-simulation)
- [✅ Verification](#-verification)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Deploy and configure an open-source wiki platform (BookStack) as a self-hosted knowledge base |
| 2 | Architect an information taxonomy applying content classification best practices |
| 3 | Implement cross-referenced documentation with tagging, glossary, and reusable content blocks |
| 4 | Evaluate knowledge base usability through structured heuristic testing |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| CLI & infra | Comfortable with Linux CLI, Docker, systemd services, and reverse proxy concepts |
| Information architecture | Understanding of IA principles (taxonomy vs. tagging, content hierarchy) |
| Database | Familiarity with MySQL/MariaDB basics |
| Editors | Basic knowledge of Markdown and WYSIWYG editors |

---

## 🖥️ Environment Setup

| Item | Value |
|---|---|
| Machine | Al Nafi-provisioned single Linux VM (Ubuntu 22.04 LTS recommended) |
| Dependencies | Docker Engine and Docker Compose installed |
| Resources | Minimum 2GB RAM, 10GB free disk space |
| Access | Root or sudo access |

Verify environment:

```bash
# ✅ Confirm Docker and Docker Compose are available
docker --version && docker compose version
sudo systemctl status docker
```

> If Docker is not installed, install it using the official convenience script and enable the service before proceeding.

---

## 🚀 Tasks

### Task 1: 🐳 Deploy BookStack via Docker Compose

**Requirements:**
- Deploy BookStack with a MariaDB backend using Docker Compose (no cloud dependencies)
- Persist data using named volumes (survive container restarts)
- Expose the app on a local port and confirm accessibility via browser or curl

**Architecture to implement:**

```text
[BookStack App Container] <--> [MariaDB Container]
         |
    Named Volumes (uploads, db-data)
         |
    Host Port 6875 -> Container Port 80
```

Design your own `docker-compose.yml` covering:
- `db` service (`mariadb:10.6`, environment vars for root password, db name, user)
- `bookstack` service (image: `lscr.io/linuxserver/bookstack`, env vars linking to db, `APP_URL`)
- A shared network and two volumes

```yaml
# docker-compose.yml (skeleton - complete the values)
version: "3.8"
services:
  db:
    image: mariadb:10.6
    environment:
      # TODO: set MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER, MYSQL_PASSWORD
    volumes:
      # TODO: mount db-data volume
  bookstack:
    image: lscr.io/linuxserver/bookstack
    environment:
      # TODO: set DB_HOST, DB_USER, DB_PASS, DB_DATABASE, APP_URL
    ports:
      # TODO: map host:container port
    depends_on:
      - db
volumes:
  db-data:
```

Bring up the stack and verify:

```bash
# 🚀 Start the stack and confirm it's reachable
docker compose up -d
docker compose ps
curl -I http://localhost:6875
```

> **Decision point:** Justify your choice of `APP_URL` (localhost vs. VM IP) and its effect on link generation within BookStack.

---

### Task 2: 🗂️ Build the Information Architecture

**Requirements — implement inside the BookStack UI:**
- Create a Shelf named **"Product Documentation"**
- Create 4 Books mapped to the taxonomy: Getting Started, How-To Guides, Reference, Troubleshooting
- Within these books, create Chapters for logical grouping (e.g., "Installation" chapter under Getting Started)
- Author 6 pages minimum, distributed across all 4 books, each containing:
  - A short intro paragraph
  - At least one reusable content block (BookStack's "Page Templates" or embedded content)
  - Internal cross-links to at least 2 other pages (use BookStack's `@` page-link syntax or link picker)

**Content distribution matrix (design your own topics):**

| Book | Min Pages | Example Topics (choose your own) |
|---|---|---|
| Getting Started | 2 | Overview, Installation |
| How-To Guides | 2 | Task walkthroughs |
| Reference | 1 | API/config reference |
| Troubleshooting | 1 | Common errors |

**Tagging system:**
- Apply BookStack's built-in Tags feature (name/value pairs) to every page — minimum 2 tags per page (e.g., `audience:beginner`, `component:auth`)
- Use the Tags search/filter to validate consistent taxonomy usage

**Glossary implementation:**
- Create a dedicated Book called **"Glossary"**
- Add a single page structured as an alphabetized term list, OR use one page per term with cross-links from content pages back to glossary entries
- Minimum 8 glossary terms tied to your documentation content

---

### Task 3: 🧭 Landing Page, Navigation, and Cross-Linking

**Requirements:**
- Configure BookStack's homepage setting (Settings > Customization) to display a custom landing page or the Shelf view
- Edit the top navigation to include quick links to all 4 taxonomy books and the Glossary
- Ensure at least 3 pages contain "Related Articles" sections linking across different books (not just within the same book)

**Design decisions to document** (in a short README or wiki page):
- Why you chose shelf-first vs. book-first navigation
- Trade-offs between deep chapter nesting vs. flat page structures for findability
- How tags complement (not duplicate) the taxonomy

---

### Task 4: 🧪 Usability Testing (First-Time User Simulation)

**Method:**
- Log out or use a private/incognito browser session with a viewer-role account (create one via Settings > Users)
- Perform 3 realistic tasks as a first-time user, e.g.:
  - Find how to resolve a specific error using only navigation (no search)
  - Locate a glossary term referenced from a How-To page
  - Use global search to find a Reference page

**Deliverable:**

Produce a short usability report (markdown file, 1 page) capturing:
- Task completion time/success (pass/fail)
- Navigation friction points observed
- 2–3 concrete IA improvements you would implement

```bash
# 📝 Save your report on the VM for verification
mkdir -p ~/kb-lab && nano ~/kb-lab/usability_report.md
```

---

## ✅ Verification

Run these checks on the same machine:

```bash
# 🐳 Confirm containers are running and healthy
docker compose ps

# 🗄️ Confirm BookStack DB has expected content (approximate check)
docker compose exec db mysql -u root -p -e \
  "USE bookstackapp; SELECT COUNT(*) FROM pages;"

# 📄 Confirm report file exists
ls -l ~/kb-lab/usability_report.md
```

**Manual verification checklist:**

- [ ] 4 taxonomy books + 1 Glossary book exist under the Shelf
- [ ] 6+ pages created, each with 2+ tags and 2+ internal cross-links
- [ ] Glossary contains 8+ terms
- [ ] Landing page/navigation exposes all books
- [ ] Usability report documents 3 tasks and improvement recommendations

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **Information Taxonomy** | A hierarchical classification (Shelf → Book → Chapter → Page) organizing content by topic |
| **Tagging vs. Taxonomy** | Tags are cross-cutting metadata filters; taxonomy is the primary structural hierarchy — they complement, not duplicate, each other |
| **Reusable Content Block** | A page template or embedded snippet reused across multiple pages to keep content consistent |
| **Cross-Linking** | Internal links between pages (and across books) that improve discoverability and reduce duplication |
| **Heuristic Usability Testing** | Evaluating navigation/findability by observing a first-time user complete realistic tasks |
| **Named Volumes** | Docker-managed persistent storage that survives container restarts, independent of the container filesystem |

---

## 🎯 Conclusion

In this lab, you deployed a self-hosted BookStack knowledge base using Docker Compose, architected a four-category documentation taxonomy backed by a glossary, and implemented tagging and cross-linking to model reusable, discoverable content — mirroring Notion-style knowledge management with fully open-source tooling. You then validated your design decisions through structured usability testing, simulating a first-time user journey to identify navigation and findability gaps.

**Key Accomplishments:**
- ✅ Deployed BookStack + MariaDB via Docker Compose with persistent named volumes
- ✅ Architected a 4-book taxonomy plus a Glossary book inside a shared Shelf
- ✅ Tagged and cross-linked 6+ pages following a consistent metadata scheme
- ✅ Configured landing-page navigation exposing the full taxonomy
- ✅ Ran a first-time-user usability test and documented improvement recommendations

**Real-World Applications:**
These skills directly support the Documentation Specialist and Knowledge Base Manager roles and reinforce IA competencies assessed under the STC CPTC – Practitioner Level certification — directly transferable to standing up and maintaining an internal team wiki or customer-facing help center.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
