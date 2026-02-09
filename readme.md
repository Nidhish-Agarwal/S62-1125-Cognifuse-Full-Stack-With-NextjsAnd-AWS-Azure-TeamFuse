## TeamFuse

**TeamFuse** is a productivity and collaboration platform that helps student and developer teams track progress, manage tasks, and visualize contributions effectively.  
It addresses the problem of **limited visibility into individual engagement**, **communication gaps**, and **unbalanced workloads** within group projects.

The platform enables:

- Real-time project updates and activity tracking
- Task assignment with performance scoring
- GitHub and Google Docs integration
- Visual dashboards for contribution analytics

By combining these, TeamFuse ensures **transparent, data-driven teamwork** and improved project outcomes.

---
## 📌 Deployment Status

> **Note:** Live deployment is currently paused due to free-tier service limits.  
> The application is fully functional and can be run locally using Docker or a manual local setup as described below.

---

## Folder Structure & Explanation

```bash
src/
├── app/          # Application routes and pages using Next.js App Router
├── components/   # Reusable UI elements like buttons, cards, and modals
├── lib/          # Utility functions, configurations, and helper logic
├── styles/       # Global styles and Tailwind configuration
├── public/       # Static assets (images, icons, and logos)
```

### Description:

- **app/** → Defines routes and page layouts for better navigation.
- **components/** → Promotes reusability and clean, consistent UI design.
- **lib/** → Contains shared logic, configurations, and API helpers.
- **styles/** → Stores Tailwind and global styling files for theme control.
- **public/** → Holds static assets accessible throughout the app.

This modular structure helps maintain **clarity**, **scalability**, and **team collaboration** throughout the development cycle.

---

## ✨ Key Features

- Real-time project updates and activity tracking
- Task assignment with contribution and performance insights
- GitHub integration using webhooks for live contribution syncing
- Visual dashboards for analytics and team performance
- Scalable backend with async job processing

---

## 🧱 Tech Stack

**Frontend**

- Next.js (App Router)
- TypeScript
- Tailwind CSS

**Backend / Infrastructure**

- PostgreSQL
- Prisma ORM
- Redis
- BullMQ
- GitHub Webhooks
- Firebase Authentication
- Docker & Docker Compose

---

## 🧩 System Requirements

TeamFuse requires the following services:

- **PostgreSQL** – Primary database
- **Redis** – Caching layer and BullMQ queues
- **Next.js App** – Main application server
- **BullMQ Workers (2 separate processes)** – Background job processing

---

## 🛠 Environment Setup

Create a `.env.local` file in the project root using `.env.example` as a reference.

```env
DATABASE_URL=postgresql://user:password@localhost:5432/teamfuse
REDIS_URL=redis://localhost:6379

JWT_SECRET=your_jwt_secret
NEXTAUTH_SECRET=your_nextauth_secret
NEXTAUTH_URL=http://localhost:3000
NEXT_PUBLIC_API_BASE_URL=http://localhost:3000

NODE_ENV=development
```

> ⚠️ Do not commit .env.local.

## ▶️ Running the Project Locally (Recommended: Docker)

### Step 1: Build Containers

```bash
docker-compose build --no-cache
```

### Step 2: Start all services

```bash
docker-compose up
```

This starts:

- Next.js app
- PostgreSQL
- Redis

## ▶️ Running Without Docker (Manual Setup)

### 1️⃣ Start PostgreSQL

Ensure PostgreSQL is running and the database exists:

```bash
createdb teamfuse
```

### 2️⃣ Start Redis

```bash
redis-server
```

### 3️⃣ Install dependencies

```bash
npm install
```

### 4️⃣ Generate Prisma Client & Run Migrations

```bash
npx prisma generate
npx prisma migrate dev
```

## 🚀 Start Application & Workers

### Terminal 1 – Start Next.js App

```bash
npm run dev
```

### Terminal 2 – Start Both BullMQ Workers

```bash
npm run start:workers
```

Each worker runs as an independent process and listens to Redis-backed job queues.

## ✅ Application Access

- App: http://localhost:3000

- PostgreSQL: http://localhost:5432

- Redis: http://localhost:6379

## 🧠 Architecture Notes (Why This Matters)

- Webhooks prevent polling GitHub APIs

- BullMQ + Redis handle async workloads without blocking requests

- Standardized API responses simplify debugging and monitoring

- Strict TypeScript + Prisma ensure runtime safety and schema consistency

- Dockerized setup ensures reproducible local development

