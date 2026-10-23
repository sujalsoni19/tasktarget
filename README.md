# TaskTarget

A full-stack task management app with secure authentication and a personal dashboard, built with **React, Node.js, Express and MongoDB**.

> Built as a take-home assignment for a frontend developer internship. The brief asked for a web app with JWT authentication, a protected dashboard with CRUD on a sample entity, API documentation, and a note on scaling the frontend–backend integration.

<!-- Add 2-3 screenshots or a short GIF here, e.g.:
![Dashboard](docs/dashboard.png)
-->

---

## Features

- Register, log in and log out
- JWT authentication, with the token stored in an httpOnly cookie
- Protected dashboard (login required)
- Profile page with avatar upload
- Create, complete and delete tasks
- Change password

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React, Vite, Tailwind CSS |
| Backend | Node.js, Express |
| Database | MongoDB Atlas |
| Auth | JWT (httpOnly cookies) |
| File uploads | Multer |

---

## API Endpoints

### Auth / Users

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/users/register` | Create an account |
| POST | `/api/users/login` | Log in |
| POST | `/api/users/logout` | Log out |
| GET | `/api/users/me` | Get the current user's profile |
| POST | `/api/users/change-password` | Change password |

### Tasks

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/tasks` | Create a task |
| GET | `/api/tasks` | List the current user's tasks |
| PATCH | `/api/tasks/:id/toggle` | Mark a task complete / incomplete |
| DELETE | `/api/tasks/:id` | Delete a task |

---

## Getting Started

### Prerequisites

- Node.js 18 or later
- A MongoDB Atlas connection string (or a local MongoDB instance)

### 1. Clone the repository

```bash
git clone https://github.com/sujalsoni19/tasktarget.git
cd tasktarget
```

### 2. Run the backend

```bash
cd backend
npm install
cp .env.example .env   # then fill in your values
npm run dev
```

Typical environment variables (match these to your `.env.example`):

```env
PORT=
MONGODB_URL=mongodb+srv://your-username:user-password@cluster0.xhezqod.mongodb.net/

CORS_ORIGIN=http://localhost:5173

ACCESS_TOKEN_SECRET=
ACCESS_TOKEN_EXPIRY=1d
REFRESH_TOKEN_SECRET=
REFRESH_TOKEN_EXPIRY=10d
```

### 3. Run the frontend

```bash
cd frontend
npm install
npm run dev
```

Open the URL Vite prints in the terminal (usually `http://localhost:5173`).

---

## Scaling Notes (Frontend–Backend Integration)

- **Independent deployment.** The frontend and backend are separate and talk only through REST APIs, so the UI can be served from a CDN (for example Vercel or Netlify) while the API runs on its own cloud infrastructure. Each side scales on its own.
- **Stateless auth.** JWTs in httpOnly cookies mean the server keeps no session state, so the backend can run as multiple instances behind a load balancer. httpOnly cookies also keep the token out of reach of JavaScript on the page.
- **Database.** MongoDB Atlas supports indexing and horizontal scaling as the number of users and tasks grows.
- **Room to grow.** The resource-based API (`/users`, `/tasks`) makes it straightforward to add pagination, filtering and search, a Redis caching layer, rate limiting, and background jobs, and later to split services out if needed.

---

## Possible Improvements

These are not implemented yet:

- Edit task title and description
- Search and filter on the dashboard
- Pagination for large task lists
- Automated tests
- Docker setup for one-command local development

---

## Author

**Sujal Soni**
[GitHub](https://github.com/sujalsoni19) 
