# 📚 Library Management System

A full-stack web application built with **Flask**, containerised with **Docker**, and integrated with a **Jenkins CI/CD pipeline**.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python 3.11, Flask 3.0 |
| Database | SQLite (via SQLAlchemy ORM) |
| Frontend | Jinja2 Templates, Vanilla CSS/JS |
| Containerisation | Docker (multi-stage build) |
| Orchestration | Docker Compose |
| CI/CD | Jenkins Pipeline (Declarative) |
| Testing | pytest, pytest-flask |

---

## Features

- **Books** – Add, view, and delete books with ISBN, genre, and quantity tracking
- **Members** – Register and manage library members with auto-generated IDs
- **Issue / Return** – Issue books to members with a 14-day due date; one-click return
- **Dashboard** – Live stats: total books, members, active issues, and overdue count
- **REST API** – `/api/books`, `/api/members`, `/api/issues`
- **Health Check** – `/health` endpoint for Docker and Jenkins monitoring

---

## Project Structure

```
library-management-system/
├── app/
│   ├── __init__.py        # App factory
│   ├── models.py          # SQLAlchemy models (Book, Member, Issue)
│   ├── routes.py          # Flask blueprints & views
│   └── templates/         # Jinja2 HTML templates
│       ├── base.html
│       ├── index.html
│       ├── books.html
│       ├── members.html
│       └── issues.html
├── tests/
│   ├── conftest.py        # pytest fixtures
│   └── test_app.py        # Unit & integration tests
├── Dockerfile             # Multi-stage Docker build
├── docker-compose.yml     # App + Jenkins services
├── Jenkinsfile            # Declarative CI/CD pipeline
├── requirements.txt
├── run.py                 # WSGI entry point
├── .gitignore
└── .dockerignore
```

---

## Quick Start (Local)

```bash
# 1. Clone the repository
git clone <your-repo-url>
cd library-management-system

# 2. Create virtual environment
python3 -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the app
python run.py
# Open http://localhost:5000
```

---

## Docker Deployment

```bash
# Build the image
docker build -t library-ms:latest .

# Run with Docker Compose (app + Jenkins)
docker-compose up -d

# App  →  http://localhost:5000
# Jenkins  →  http://localhost:8080
```

---

## Running Tests

```bash
# Install pytest
pip install pytest pytest-flask

# Run all tests
pytest tests/ -v

# With HTML report
pytest tests/ -v --html=reports/test-report.html
```

---

## Jenkins Pipeline Stages

| Stage | Description |
|-------|-------------|
| **Checkout** | Pull source code from Git |
| **Setup Environment** | Create Python venv & install deps |
| **Lint** | Run flake8 static analysis |
| **Unit Tests** | Run pytest & publish JUnit results |
| **Docker Build** | Build multi-stage Docker image |
| **Image Verification** | Spin up container & hit `/health` |
| **Push to Registry** | Push tagged image to Docker Hub (main branch) |
| **Deploy** | `docker-compose up -d` deployment |

### Setting up Jenkins

1. Start Jenkins: `docker-compose up -d jenkins`
2. Visit `http://localhost:8080`
3. Install plugins: **Git**, **Docker Pipeline**, **JUnit**, **HTML Publisher**
4. Create a **Pipeline** job → point to this repo
5. Set branch to `main` → Build Now

---

## Git Workflow

```bash
git init
git add .
git commit -m "Initial commit – Library Management System"
git remote add origin <your-repo-url>
git push -u origin main
```

---

## API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Dashboard |
| `/books` | GET | List all books |
| `/books/add` | POST | Add a book |
| `/books/delete/<id>` | POST | Delete a book |
| `/members` | GET | List members |
| `/members/add` | POST | Register a member |
| `/issues` | GET | List all issues |
| `/issues/add` | POST | Issue a book |
| `/issues/return/<id>` | POST | Return a book |
| `/api/books` | GET | JSON – all books |
| `/api/members` | GET | JSON – all members |
| `/api/issues` | GET | JSON – all issues |
| `/health` | GET | Health check |
