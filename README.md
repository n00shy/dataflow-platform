# 🚀 DataFlow — Full-Stack Data Management System

A production-ready web application for managing and entering data, built with modern technologies.

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite + Tailwind CSS |
| Backend | Node.js + Express |
| Database | MongoDB + Mongoose |
| Auth | JWT (Access + Refresh Tokens) + bcrypt |
| Containers | Docker + Docker Compose |

## ✨ Features

- **Authentication**: Register, Login, Logout with JWT refresh token rotation
- **Role-based Access Control**: Admin and User roles
- **Records Management**: Full CRUD with search, filter, sort, pagination
- **Date Range Filtering**: Filter records by creation date
- **CSV Export**: Export all records to CSV
- **Activity Logs**: Track all user actions
- **User Management** (Admin): Activate/deactivate users, change roles
- **Dark Mode**: System-aware + manual toggle
- **Responsive Design**: Works on mobile, tablet, desktop

## 📁 Project Structure


dataflow/
├── backend/
│ ├── src/
│ ├── package.json
│ ├── package-lock.json
│ ├── Dockerfile
│
├── frontend/
│ ├── src/
│ ├── package.json
│ ├── package-lock.json
│ ├── Dockerfile
│ ├── nginx.conf
│
├── docker-compose.yml
├── docker-compose.dev.yml
└── README.md


---

## 🚀 CI/CD Pipeline (GitHub Actions + Docker Hub)

This project uses automated CI/CD with GitHub Actions.

### ⚙️ Pipeline Flow
On every push to `main`:

- Install dependencies (frontend + backend)
- Build project
- Build Docker images
- Push images to Docker Hub

### 🔐 Required Secrets

Add in GitHub:

- `DOCKER_USERNAME`
- `DOCKER_PASSWORD`

### 🐳 Docker Images

After pipeline success:

- `your-dockerhub/workflow-backend:latest`
- `your-dockerhub/workflow-frontend:latest`

### 📦 Workflow File


.github/workflows/cicd.yml


---

## 🚀 Quick Start

### 1. Clone project
```bash
git clone <repo-url>
cd dataflow
2. Run with Docker
docker-compose up -d --build

Frontend:
http://localhost:3000

Backend:
http://localhost:5000/api

🔐 API Overview
Auth
POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh
Records
GET /api/records
POST /api/records
PUT /api/records/:id
DELETE /api/records/:id
🧹 Useful Commands
docker-compose up -d --build
docker-compose logs -f
docker-compose down
