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

```
dataflow/
├── backend/
│   ├── src/
│   │   ├── controllers/     # Business logic
│   │   ├── middleware/      # Auth & error handling
│   │   ├── models/          # Mongoose schemas
│   │   ├── routes/          # API routes
│   │   ├── utils/           # JWT helpers
│   │   └── server.js        # Entry point
│   ├── .env                 # Environment variables
│   ├── Dockerfile
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── api/             # Axios API service
│   │   ├── components/      # Reusable components
│   │   ├── context/         # Auth & Theme context
│   │   ├── pages/           # Route pages
│   │   └── main.jsx
│   ├── Dockerfile
│   ├── nginx.conf
│   └── package.json
├── docker-compose.yml       # Production
├── docker-compose.dev.yml   # Development override
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose installed
- Git

### 1. Clone & Configure

```bash
git clone <repo-url>
cd dataflow
```

Edit `backend/.env` — change secrets for production:
```env
JWT_SECRET=your_super_secret_key
JWT_REFRESH_SECRET=your_refresh_secret
```

### 2. Run with Docker (Production)

```bash
docker-compose up -d --build
```

App available at:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000/api
- Health check: http://localhost:5000/api/health

### 3. Run for Development (Hot Reload)

```bash
# Install dependencies locally
cd backend && npm install && cd ..
cd frontend && npm install && cd ..

# Backend
cd backend && npm run dev

# Frontend (new terminal)
cd frontend && npm run dev
```

Or with Docker dev mode:
```bash
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

### 4. First Login

The **first registered user automatically becomes Admin**.

Register at http://localhost:3000/register with:
- Any name
- Any email
- Password (min 6 chars)

## 🔗 API Endpoints

### Auth
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/auth/register` | Register new user | Public |
| POST | `/api/auth/login` | Login | Public |
| POST | `/api/auth/refresh` | Refresh access token | Public |
| POST | `/api/auth/logout` | Logout | Required |
| GET | `/api/auth/me` | Get current user | Required |

### Records
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/api/records` | List records (paginated) | Required |
| GET | `/api/records/export` | Export all records | Required |
| POST | `/api/records` | Create record | Required |
| PUT | `/api/records/:id` | Update record | Required |
| DELETE | `/api/records/:id` | Delete record | Required |

**Query params for GET /api/records:**
- `page`, `limit` — pagination
- `search` — full-text search
- `status` — filter by active/inactive/pending
- `startDate`, `endDate` — date range
- `sortBy`, `sortOrder` — sorting

### Users (Admin only)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users` | List all users |
| PATCH | `/api/users/:id/toggle-status` | Activate/deactivate |
| PATCH | `/api/users/:id/role` | Change role |

### Activity
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/activity` | Get activity log |

## 🔐 Security Features

- Passwords hashed with bcrypt (12 rounds)
- Short-lived JWT access tokens (15 min)
- Refresh token rotation (7 days)
- Rate limiting (100 req/15 min)
- CORS configured
- Role-based route protection
- Users can only access their own records (admins see all)

## 🧹 Useful Commands

```bash
# View logs
docker-compose logs -f backend
docker-compose logs -f frontend

# Stop everything
docker-compose down

# Remove volumes (clears database)
docker-compose down -v

# Rebuild single service
docker-compose up -d --build backend
```

## 🌙 Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Backend port | `5000` |
| `MONGODB_URI` | MongoDB connection string | - |
| `JWT_SECRET` | Access token secret | - |
| `JWT_EXPIRES_IN` | Access token lifetime | `15m` |
| `JWT_REFRESH_SECRET` | Refresh token secret | - |
| `JWT_REFRESH_EXPIRES_IN` | Refresh token lifetime | `7d` |
| `FRONTEND_URL` | CORS allowed origin | `http://localhost:3000` |
