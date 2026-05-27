# beProductive

A team project management platform built with the MERN stack. Manage workspaces, projects, tasks, and team members with role-based access control.

## Tech Stack

**Backend** — Node.js, Express, TypeScript, MongoDB (Mongoose), Passport.js, cookie-session

**Frontend** — React 18, TypeScript, Vite, TailwindCSS, shadcn/ui, TanStack Query, React Router v7

## Features

- Email & password authentication
- Multiple workspaces per user
- Invite members via shareable invite links
- Role-based permissions — Owner, Admin, Member
- Project and task management (create, edit, delete)
- Task status and priority tracking with filters
- Analytics dashboard per workspace and project
- Paginated task tables with search and filtering

## Local Setup

### Prerequisites

- Node.js v18+
- A [MongoDB Atlas](https://cloud.mongodb.com) cluster (free tier works)

### 1. Clone the repo

```bash
git clone <repo-url>
cd team-task-manager
```

### 2. Configure the backend

```bash
cp backend/.env.example backend/.env
```

Edit `backend/.env`:

```env
PORT=8000
NODE_ENV=development
MONGO_URI="mongodb+srv://<username>:<password>@<cluster>.mongodb.net/teamsync_db"
SESSION_SECRET="your-random-secret-here"
SESSION_EXPIRES_IN="1d"
FRONTEND_ORIGIN=http://localhost:3000
```

### 3. Configure the frontend

```bash
cp client/.env.example client/.env
```

`client/.env` should contain:

```env
VITE_API_BASE_URL="http://localhost:8000/api"
```

### 4. Install dependencies

```bash
cd backend && npm install
cd ../client && npm install
```

### 5. Seed the database

Run once to insert the required roles (Owner, Admin, Member):

```bash
cd backend && npm run seed
```

### 6. Start the dev servers

**Terminal 1 — Backend:**
```bash
cd backend && npm run dev
```

**Terminal 2 — Frontend:**
```bash
cd client && npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Deployment (Railway)

### Backend service

- Root directory: `backend`
- Build command: `npm run build`
- Start command: `npm start`

Environment variables to set:

```env
NODE_ENV=production
PORT=8000
MONGO_URI=<your atlas uri>
SESSION_SECRET=<random secret>
SESSION_EXPIRES_IN=1d
FRONTEND_ORIGIN=https://<your-frontend-domain>
```

### Frontend service

- Root directory: `client`
- Build command: `npm run build`
- Start command: `npm start`

Environment variables to set:

```env
VITE_API_BASE_URL=https://<your-backend-domain>/api
```

> After both services are deployed, update `FRONTEND_ORIGIN` in the backend service to match the frontend's Railway domain.

## Project Structure

```
team-task-manager/
├── backend/
│   ├── src/
│   │   ├── config/        # App, DB, session, passport config
│   │   ├── controllers/   # Route handlers
│   │   ├── middlewares/   # Auth, error handling
│   │   ├── models/        # Mongoose models
│   │   ├── routes/        # Express routers
│   │   ├── services/      # Business logic
│   │   ├── utils/         # Helpers and guards
│   │   └── index.ts       # Entry point
│   └── package.json
└── client/
    ├── src/
    │   ├── components/    # UI components
    │   ├── context/       # Auth and query providers
    │   ├── hooks/         # Custom React hooks
    │   ├── lib/           # API client and utilities
    │   ├── page/          # Route pages
    │   └── routes/        # Router configuration
    └── package.json
```
