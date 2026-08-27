# Network Testing & Validation Framework

[![Python Version](https://img.shields.io/badge/Python-3.11%2B-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![Playwright](https://img.shields.io/badge/Playwright-E2E%20Testing-2EAD33?style=flat&logo=playwright&logoColor=white)](https://playwright.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-REST%20API-009688?style=flat&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18%20SPA-61DAFB?style=flat&logo=react&logoColor=black)](https://react.dev/)
[![MongoDB](https://img.shields.io/badge/MongoDB-7.0-47A248?style=flat&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![PyATS](https://img.shields.io/badge/Cisco-PyATS%20%2F%20Genie-049fd9?style=flat&logo=cisco&logoColor=white)](https://developer.cisco.com/pyats/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

An enterprise-grade, multi-tier test automation framework built to validate modern web applications, REST APIs, databases, and network infrastructure.

---

## 📌 Overview

This framework provides end-to-end quality engineering and test automation for **NetMonitor**, a full-stack network monitoring and management platform:

- **Backend Application:** FastAPI + Async MongoDB (Motor) with JWT authentication, device registry, alert generation, and health check endpoints.
- **Frontend Application:** React 18 SPA built with Vite and Material-UI (MUI) for real-time device status and alert management.
- **Multi-Tier Test Suite:** Comprehensive test coverage covering API, UI, Database, E2E Integration, and Cisco network device validation.

---

## 🚀 Key Features & Test Coverage

### 1. 🔌 REST API Testing
- Full CRUD validation for `/api/devices`, `/api/alerts`, `/api/auth`, and `/api/health`.
- JWT authentication and token verification scenarios.
- Strict Pydantic schema validation for request/response payloads.
- Parameterized data-driven testing (`@pytest.mark.parametrize` with external JSON datasets).
- Robust edge case, boundary, pagination, filtering, and negative error handling tests (400, 401, 403, 404, 422).

### 2. 🖥️ Web UI Automation (Playwright)
- Implemented with **Page Object Model (POM)** architecture (`BasePage`, `LoginPage`, `DashboardPage`, `DevicesPage`, `AlertsPage`).
- Resilient `data-testid` element locator strategy.
- **Cross-Browser Matrix:** Automated validation across Chromium, Firefox, and WebKit engines.
- **Responsive Viewport Testing:** Automated verification across Desktop, Tablet, and Mobile layouts.
- **Visual Regression Testing:** Screenshot comparison against baseline references with Pillow pixel diffing.
- **Accessibility Checks:** Automated WCAG standards and keyboard navigation auditing.
- **Network Interception:** Client-side API request/response mocking and latency simulation.

### 3. 🗄️ Database & State Integrity Testing
- Direct MongoDB assertions with PyMongo to verify CRUD persistence, field types, and document counts.
- Automated cleanup fixtures ensuring total test isolation without residual test data.

### 4. 🔄 End-to-End Integration Testing
- Full user journey testing: UI user actions $\rightarrow$ API request processing $\rightarrow$ MongoDB state persistence and event reflection.

### 5. 🌐 Network Device Automation (PyATS / Genie)
- Cisco IOS-XE DevNet Sandbox integration.
- Automated execution and parsing of network CLI commands (`show version`, `show ip interface brief`).
- Socket-level TCP connectivity validation with graceful fallback for offline environments.

### 6. 📊 Rich Reporting & Observability
- Self-contained HTML test execution reports (`pytest-html`).
- Comprehensive Allure dashboard reports with suites, timeline, and trend analytics.
- Automatic full-page screenshot capture on test failure.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Backend API** | FastAPI, Uvicorn, Motor (Async Mongo), Pydantic v2, PyJWT, Passlib (Bcrypt) |
| **Frontend UI** | React 18, Vite, Material-UI (MUI), Axios, React Router v6 |
| **Database** | MongoDB 7.0, Mongo Express |
| **Test Automation** | pytest, Playwright, requests, httpx, Pillow, Faker, PyATS, Genie |
| **Reporting** | Allure Framework, pytest-html, pytest-cov |
| **DevOps & Infra** | Docker, Docker Compose, GitHub Actions CI/CD, Node.js 22, Python 3.11+ |

---

## 📂 Project Structure

```text
├── backend/                  # FastAPI Application
│   ├── app/
│   │   ├── database/         # MongoDB connection & collections
│   │   ├── models/           # Pydantic data models & schemas
│   │   ├── routes/           # API route handlers (auth, devices, alerts, health)
│   │   └── config.py         # Application settings & environment loader
│   ├── Dockerfile
│   └── requirements.txt
│
├── frontend/                 # React 18 + Vite SPA
│   ├── src/
│   │   ├── components/       # Reusable UI components (Navbar, Sidebar, Tables)
│   │   ├── pages/            # View pages (Login, Dashboard, Devices, Alerts)
│   │   ├── services/         # Axios API client & interceptors
│   │   └── context/          # Authentication & state context
│   ├── Dockerfile
│   └── package.json
│
├── pages/                    # Playwright Page Object Model (POM)
│   ├── base_page.py          # Core page interactions, waits, and assertions
│   ├── login_page.py
│   ├── dashboard_page.py
│   ├── devices_page.py
│   └── alerts_page.py
│
├── services/                 # API client wrapper services for tests
│   ├── auth_service.py
│   └── device_service.py
│
├── tests/                    # Multi-tier Test Automation Suites
│   ├── api/                  # API tests (CRUD, Auth, Schema, Data-Driven)
│   ├── ui/                   # Playwright UI tests (POM, Cross-Browser, Visual)
│   ├── database/             # MongoDB integrity & consistency tests
│   ├── integration/          # Full-journey E2E integration tests
│   ├── network/              # PyATS Cisco device tests
│   ├── baselines/            # Visual regression reference screenshots
│   └── conftest.py           # Pytest fixtures, hooks, setup & teardown
│
├── utils/                    # Test utilities & helper modules
│   ├── database_helper.py    # Direct MongoDB test helper
│   ├── network_helper.py     # Socket checks & PyATS wrappers
│   ├── flaky_handler.py      # Flaky test decorators & retry logic
│   └── logger.py             # Custom colored test execution logger
│
├── config/                   # Configuration & Test Assets
│   ├── environments/         # .env.dev, .env.qa, .env.staging profiles
│   ├── test_data/            # Static JSON test fixtures & datasets
│   └── testbeds/             # Cisco DevNet PyATS YAML testbed topology
│
├── .github/workflows/ci.yml  # GitHub Actions CI/CD multi-job pipeline
├── docker-compose.yml        # Multi-container orchestration (App + DB)
├── pytest.ini               # Pytest configuration & markers
└── requirements.txt          # Python test framework dependencies
```

---

## ⚡ Quick Start

### Prerequisites
- **Python:** 3.11 or higher
- **Node.js:** 20+ / 22+ & npm
- **Docker & Docker Compose:** Installed and running

---

### Option A: Run with Docker Compose (Recommended)

Start the entire stack (FastAPI backend, React frontend, MongoDB, and Mongo Express) with a single command:

```bash
# 1. Clone the repository
git clone https://github.com/Shiva-129/Network-Testing-Validation-Framework.git
cd Network-Testing-Validation-Framework

# 2. Launch all services in the background
docker-compose up -d

# 3. Verify running containers
docker-compose ps
```

**Service Endpoints:**
- 🌐 **Frontend UI:** [http://localhost:3001](http://localhost:3001)
- 🔌 **Backend API:** [http://localhost:5001/api](http://localhost:5001/api)
- 📖 **Interactive Swagger Docs:** [http://localhost:5001/api/docs](http://localhost:5001/api/docs)
- 🗃️ **Mongo Express UI (Dev):** [http://localhost:8081](http://localhost:8081)

---

### Option B: Local Manual Setup

#### 1. Setup Python Virtual Environment
```bash
# Create and activate virtual environment
python -m venv venv

# Windows:
venv\Scripts\activate

# Linux/macOS:
# source venv/bin/activate

# Install test dependencies
pip install -r requirements.txt
pip install -r backend/requirements.txt

# Install Playwright browser binaries
playwright install chromium firefox webkit
```

#### 2. Start MongoDB (via Docker)
```bash
docker run -d -p 27017:27017 --name mongodb mongo:7
```

#### 3. Start Backend Server
```bash
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 5000
```

#### 4. Start Frontend Client (in a separate terminal)
```bash
cd frontend
npm install
npm run dev
```

---

## 🧪 Running Tests

### 1. Execute by Test Layer

```bash
# Run all API tests
pytest tests/api/ -v

# Run all Playwright UI tests
pytest tests/ui/ -v

# Run Database consistency tests
pytest tests/database/ -v

# Run E2E Integration tests
pytest tests/integration/ -v

# Run Cisco Network tests (PyATS DevNet)
pytest tests/network/ -m network -v

# Run the complete test suite
pytest -v
```

### 2. Execute by Pytest Markers

```bash
# Smoke tests (critical paths, quick feedback)
pytest -m smoke -v

# Full regression suite
pytest -m regression -v

# Visual regression tests (screenshot diffs)
pytest -m visual -v

# Accessibility compliance checks (WCAG)
pytest -m accessibility -v

# Cross-browser layout verification
pytest -m crossbrowser -v
```

### 3. Browser Selection & UI Options

```bash
# Target specific browser
pytest tests/ui/ --browser chromium
pytest tests/ui/ --browser firefox
pytest tests/ui/ --browser webkit

# Run with visible UI (headed mode)
pytest tests/ui/ --browser chromium --headed

# Retry flaky UI tests automatically
pytest tests/ui/ --reruns 3 --reruns-delay 1
```

### 4. Parallel Test Execution

```bash
# Execute independent test suites in parallel
pytest tests/api/ -n 4
```

---

## ⚙️ Environment Configuration

The framework supports multiple environment profiles using the `--env` flag:

```bash
# Run against QA environment
pytest --env=qa -m smoke -v

# Run against Staging environment
pytest --env=staging -m regression -v
```

### Environment Variables

| Variable | Description | Default (Dev) |
|---|---|---|
| `API_BASE_URL` | Base URL for REST API endpoints | `http://localhost:5001/api` |
| `FRONTEND_BASE_URL` | Base URL for Frontend UI | `http://localhost:3001` |
| `MONGODB_URI` | MongoDB Connection String | `mongodb://localhost:27017/` |
| `MONGODB_DATABASE` | Target Database Name | `network_monitoring` |
| `JWT_SECRET` | Secret key for JWT signing | `dev-secret-key` |
| `PYATS_TESTBED` | Path to PyATS network testbed YAML | `config/testbeds/devnet_sandbox.yaml` |

---

## 📈 Reporting & Test Artifacts

### 1. Pytest HTML Report
Generate a self-contained HTML report with test durations, outputs, and status:
```bash
pytest --html=reports/report.html --self-contained-html
```

### 2. Allure Interactive Dashboard
Generate and serve rich interactive reports with trends, attachments, and failure analytics:
```bash
# Collect Allure results
pytest --alluredir=reports/allure-results

# Generate and open report in browser
allure serve reports/allure-results
```

### 3. Failure Screenshots
When any Playwright UI test fails, a full-page screenshot is automatically captured and saved to:
`test-results/screenshots/`

---

## 🔄 CI/CD Pipeline

The framework is configured with a GitHub Actions workflow (`.github/workflows/ci.yml`):

- 🔍 **Code Quality:** Automated linting with `flake8`, `black`, and `isort`.
- 🧪 **Backend Testing:** Spins up MongoDB service container, seeds test data, and runs API & Database test suites.
- 🌐 **UI Matrix Testing:** Executes Playwright tests across multiple browsers (`chromium`, `firefox`).
- 🔗 **E2E Integration:** Validates full integration workflows in containerized environments.
- 📡 **Network Automation:** Automated PyATS runs against Cisco DevNet Sandboxes on scheduled builds.
- 🐳 **Docker Validation:** Validates container builds for Backend and Frontend.
- 📊 **Report Publishing:** Automatically merges Allure test results and publishes reports.

---

## 👤 Author

**Shiva Sathwik**
- GitHub: [@Shiva-129](https://github.com/Shiva-129)
- Repository: [Network-Testing-Validation-Framework](https://github.com/Shiva-129/Network-Testing-Validation-Framework)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) - see the [LICENSE](LICENSE) file for details.
