<div align="center">

# 🔌 Build an API Reference with OpenAPI and Swagger UI

![OpenAPI](https://img.shields.io/badge/OpenAPI%203.0-6BA539?style=for-the-badge&logo=openapiinitiative&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger%20UI-85EA2D?style=for-the-badge&logo=swagger&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![YAML](https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)

**Al Nafi Cybersecurity Education Platform — Hands-On Lab**

</div>

---

## 📑 Table of Contents

- [📋 Objectives](#-objectives)
- [🧰 Prerequisites](#-prerequisites)
- [🖥️ Environment Setup](#️-environment-setup)
- [🚀 Tasks](#-tasks)
  - [Task 1: 📦 Install Swagger UI and a local server tool](#task-1-📦-install-swagger-ui-and-a-local-server-tool)
  - [Task 2: 📝 Author the OpenAPI YAML file](#task-2-📝-author-the-openapi-yaml-file)
  - [Task 3: ✅ Validate the specification](#task-3-✅-validate-the-specification)
  - [Task 4: 🔗 Point Swagger UI to your spec](#task-4-🔗-point-swagger-ui-to-your-spec)
  - [Task 5: 🌐 Serve Swagger UI locally](#task-5-🌐-serve-swagger-ui-locally)
  - [Task 6: 🧪 Test an endpoint with Try-It-Out](#task-6-🧪-test-an-endpoint-with-try-it-out)
  - [Task 7: 📤 Export static HTML documentation](#task-7-📤-export-static-html-documentation)
- [✅ Verification](#-verification)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [📚 Key Concepts](#-key-concepts)
- [🎯 Conclusion](#-conclusion)

---

## 📋 Objectives

By the end of this lab, you will be able to:

| # | Objective |
|---|-----------|
| 1 | Author an OpenAPI 3.0 YAML specification for a sample task-tracker API |
| 2 | Document endpoints with parameters, request/response schemas, and API key authentication |
| 3 | Serve and test the spec interactively using Swagger UI on a local Linux machine |
| 4 | Export the rendered documentation as a static HTML site |

---

## 🧰 Prerequisites

| Requirement | Details |
|---|---|
| REST concepts | Basic familiarity with REST API concepts (endpoints, HTTP methods, JSON) |
| Terminal & editor | Comfortable with Linux terminal and a text editor (nano/vim) |
| YAML | Basic YAML syntax knowledge |
| OpenAPI/Swagger | No prior experience required, but helpful |

---

## 🖥️ Environment Setup

> Al Nafi provides a **single Linux machine** via Start Lab — use it for all steps below.

Verify internet access for package installation:

```bash
# 🔄 Update package lists
sudo apt update

# 📦 Install Node.js (skip the setup script if already installed)
node -v || curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# ✅ Confirm Node.js and npm are available
node -v && npm -v
```

Create a working directory:

```bash
# 📁 Create the lab project folder
mkdir -p ~/api-docs-lab && cd ~/api-docs-lab
```

---

## 🚀 Tasks

### Task 1: 📦 Install Swagger UI and a local server tool

Install `swagger-ui-dist` (static Swagger UI assets) and `http-server` (simple static file server):

```bash
# 🆕 Initialize a Node project
npm init -y

# 📦 Install Swagger UI assets and a local static server
npm install swagger-ui-dist http-server
```

Copy Swagger UI static files into your project:

```bash
# 📂 Copy the prebuilt Swagger UI assets into docs/
mkdir -p docs
cp -r node_modules/swagger-ui-dist/* docs/
```

> **TODO:** Inspect `docs/index.html` and note the line referencing `swagger-initializer.js` — you will edit this later to point to your spec file.

---

### Task 2: 📝 Author the OpenAPI YAML file

Create `openapi.yaml` in your project root. Complete the `TODO` sections.

```yaml
openapi: 3.0.3
info:
  title: Task Tracker API
  description: A sample API for managing tasks
  version: "1.0.0"
servers:
  - url: http://localhost:3000/api/v1
    description: Local development server

paths:
  /tasks:
    get:
      summary: List all tasks
      # TODO: add a description field
      responses:
        '200':
          description: A list of tasks
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Task'
    post:
      summary: Create a new task
      security:
        - ApiKeyAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TaskInput'
      responses:
        '201':
          description: Task created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Task'

  /tasks/{taskId}:
    # TODO: define the "parameters" section here (shared by PUT and DELETE)
    put:
      summary: Update an existing task
      security:
        - ApiKeyAuth: []
      # TODO: add parameters reference for taskId
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TaskInput'
      responses:
        '200':
          description: Task updated
        '404':
          description: Task not found
    delete:
      summary: Delete a task
      security:
        - ApiKeyAuth: []
      # TODO: add parameters reference for taskId
      responses:
        '204':
          description: Task deleted
        '404':
          description: Task not found

components:
  schemas:
    Task:
      type: object
      properties:
        id:
          type: integer
        title:
          type: string
        completed:
          type: boolean
      # TODO: add "required" list for id and title

    TaskInput:
      type: object
      properties:
        title:
          type: string
        completed:
          type: boolean
      required:
        - title

  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: X-API-KEY
```

**Requirements to complete:**

- Add a `description` to the `GET /tasks` operation
- Add a shared `parameters` block for `taskId` (type integer, in path, required) under `/tasks/{taskId}` and reference it (`$ref`) from `PUT` and `DELETE`, or repeat it inline
- Add `required: [id, title]` to the `Task` schema
- Validate your YAML indentation carefully — errors here will break Swagger UI rendering

---

### Task 3: ✅ Validate the specification

Install a quick CLI validator:

```bash
# 📦 Install the Redocly CLI globally
npm install -g @redocly/cli

# 🔍 Lint your OpenAPI spec
redocly lint openapi.yaml
```

Fix any reported errors before proceeding (common issues: bad indentation, missing `$ref` targets, mismatched types).

---

### Task 4: 🔗 Point Swagger UI to your spec

Copy your spec into the `docs` folder:

```bash
# 📂 Copy the spec file into the Swagger UI docs folder
cp openapi.yaml docs/
```

Edit `docs/swagger-initializer.js`. Replace the default URL:

```javascript
window.ui = SwaggerUIBundle({
  url: "openapi.yaml",   // TODO: confirm this matches your copied file name
  dom_id: '#swagger-ui',
  presets: [
    SwaggerUIBundle.presets.apis,
    SwaggerUIStandalonePreset
  ],
});
```

---

### Task 5: 🌐 Serve Swagger UI locally

```bash
# 🚀 Start the local static file server
npx http-server docs -p 8080
```

- Open a browser (or use `curl` if headless) to `http://localhost:8080`
- Confirm the interactive documentation loads: title, endpoints, and schemas visible
- If the page is blank, open browser dev tools console and check for a 404 on `openapi.yaml` or a YAML parse error

---

### Task 6: 🧪 Test an endpoint with Try-It-Out

- In the Swagger UI page, expand `GET /tasks`
- Click **Try it out** → **Execute**

> **TODO:** Capture the response by taking a screenshot or copying the response body and status code into a file:

```bash
# 📝 Save your observed response manually
nano ~/api-docs-lab/test-response.txt
```

Record: HTTP status code, response headers, and response body.

---

### Task 7: 📤 Export static HTML documentation

Since Swagger UI dist is already static HTML/JS/CSS, package the `docs` folder as your deliverable:

```bash
# 📦 Archive the docs folder as the deliverable
cd ~/api-docs-lab
tar -czvf task-tracker-api-docs.tar.gz docs/

# 📏 Confirm the archive was created
ls -lh task-tracker-api-docs.tar.gz
```

> **TODO:** Verify the archive contains `index.html`, `openapi.yaml`, and the Swagger UI assets by extracting it into a temp folder and reopening in a browser.

---

## ✅ Verification

Confirm lab completion on the same machine:

```bash
# 1️⃣ Spec validates without errors
redocly lint openapi.yaml

# 2️⃣ Server is running and responding
curl -I http://localhost:8080

# 3️⃣ Spec file is reachable via the server
curl http://localhost:8080/openapi.yaml | head -20

# 4️⃣ Archive exists and is non-empty
tar -tzvf task-tracker-api-docs.tar.gz | head
```

**Expected outcomes:**
- `redocly lint` returns no errors
- Browser shows four documented operations (GET, POST, PUT, DELETE) under `/tasks`
- Security scheme `ApiKeyAuth` appears in the Authorize button dialog
- `test-response.txt` contains a captured 200 response
- `.tar.gz` archive extracts into a working static site

---

## 🛠️ Troubleshooting

<details>
<summary>Click to expand common issues and fixes</summary>

- **Blank Swagger UI page:** check browser console for YAML syntax errors or wrong file path in `swagger-initializer.js`.
- **Port already in use:** change `-p 8080` to another port, e.g., `-p 8081`.
- **`redocly` command not found:** re-run global npm install or use `npx @redocly/cli lint openapi.yaml`.
- **Try-It-Out fails with CORS error:** this is expected since there is no real backend — treat it as documentation-only; note this in your captured response file.

</details>

---

## 📚 Key Concepts

| Concept | Description |
|---|---|
| **OpenAPI Specification** | A machine-readable YAML/JSON contract describing an API's endpoints, schemas, and auth |
| **Swagger UI** | An interactive HTML/JS renderer that turns an OpenAPI spec into browsable, testable docs |
| **Path & Operation** | A `path` (e.g. `/tasks/{taskId}`) groups HTTP `operations` (GET, POST, PUT, DELETE) |
| **Component Schema** | A reusable object definition (e.g. `Task`) referenced via `$ref` to avoid duplication |
| **Security Scheme** | Declares how an API is authenticated (here, an `apiKey` sent via the `X-API-KEY` header) |
| **Spec Linting** | Automated validation (e.g. Redocly CLI) that catches YAML and schema errors before serving |

---

## 🎯 Conclusion

In this lab, you installed Node.js and Swagger UI tooling on a Linux machine, authored a complete OpenAPI 3.0 specification for a task-tracker API covering four HTTP methods, request/response schemas, and API key security. You validated the spec, served it locally through Swagger UI, tested an endpoint interactively, and packaged the documentation as a static HTML site.

**Key Accomplishments:**
- ✅ Installed Node.js, Swagger UI assets, and a local static file server
- ✅ Authored an OpenAPI 3.0 spec covering GET, POST, PUT, and DELETE operations
- ✅ Documented request/response schemas and API key security
- ✅ Validated the spec with the Redocly CLI linter
- ✅ Served and interactively tested the API docs with Swagger UI
- ✅ Packaged the rendered documentation as a static, shareable archive

**Real-World Applications:**
These skills directly support API documentation workflows used by Technical Writers and API Documentation Specialists, and align with OpenAPI Specification and STC CPTC practitioner competencies — directly transferable to documenting internal microservices, public developer APIs, and integration partner contracts.

---

<div align="center">

**🔐 Al Nafi Cybersecurity Education Platform**

</div>
