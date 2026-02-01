# Deployment Guide

This guide covers deployment strategies for **Cyber LMS** on GitHub Codespaces, Coolify, and CloudPanel (Hostinger VPS).

## ☁️ GitHub Codespaces

GitHub Codespaces provides a complete, configurable development environment in the cloud.

1. **Open in Codespaces**:
   - Navigate to the GitHub repository.
   - Click on the **Code** button -> **Codespaces** tab.
   - Click **Create codespace on main**.

2. **Environment Configuration**:
   - The repository includes a `.devcontainer` configuration that automatically sets up the environment with Docker, Bun, and necessary extensions.
   - Once the codespace loads, Docker Compose services defined in `docker-compose.yml` should start automatically.

3. **Accessing Ports**:
   - Use the **Ports** tab in VS Code to access the Frontend (8080) and Backend (3000).

---

## 🚀 Deploying on Coolify

[Coolify](https://coolify.io/) is an open-source, self-hostable Heroku/Vercel alternative.

### Option 1: Docker Compose (Recommended)

1. **Login to Coolify Dashboard**.
2. **Create a New Service**:
   - Select **Docker Compose**.
3. **Source**:
   - Connect your GitHub repository.
   - Select the `cyber-lms` repo and branch.
4. **Configuration**:
   - Coolify will detect the `docker-compose.yml` file.
   - **Environment Variables**:
     - Add variables from `.env.example` (POSTGRES_USER, JWT_SECRET, etc.) into the Coolify Environment Variables section.
5. **Deploy**:
   - Click **Deploy**. Coolify will build the images and orchestrate the services.
6. **Domains**:
   - Assign a domain to the `frontend` service (port 80) and `backend` service (port 3000) via the Proxy settings in Coolify.

---

## 🌩 Deploying on CloudPanel (Hostinger VPS)

[CloudPanel](https://www.cloudpanel.io/) is a modern server control panel for PHP, Node.js, and Static sites.

### Prerequisites
- A VPS (e.g., Hostinger) with CloudPanel installed.
- SSH access to the server.

### Step 1: Database Setup
1. Log in to CloudPanel.
2. Go to **Databases** -> **Add Database**.
3. Create a PostgreSQL database (if supported via Docker) or use the default MySQL (Note: This project uses PostgreSQL. You may need to run Postgres via Docker manually on the VPS).

**Running Postgres via Docker on VPS:**
```bash
docker run -d --name cyber-lms-db \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=securepassword \
  -e POSTGRES_DB=cyber_lms \
  -p 5432:5432 \
  -v postgres_data:/var/lib/postgresql/data \
  postgres:15-alpine
```

### Step 2: Backend Deployment (Node.js Application)
1. Go to **Applications** -> **Add Application** -> **Node.js**.
2. **Domain**: `api.yourdomain.com`.
3. **User**: create a system user (e.g., `cyberlms`).
4. **Path**: `/home/cyberlms/htdocs/api.yourdomain.com`.
5. **Upload Code**:
   - Use git to clone the repo into the folder.
   - `git clone https://github.com/your-username/cyber-lms.git .`
6. **Install & Build**:
   ```bash
   cd backend
   # Install Bun if not present, or use npm
   npm install
   npx prisma generate
   npm run build
   ```
7. **Environment Variables**:
   - Create a `.env` file in the `backend` directory.
8. **Start Command**: `npm start` (ensure package.json scripts use node/bun appropriately).

### Step 3: Frontend Deployment (Static Site)
1. Go to **Applications** -> **Add Application** -> **Static Site**.
2. **Domain**: `yourdomain.com`.
3. **Path**: `/home/cyberlms/htdocs/yourdomain.com`.
4. **Upload Code**:
   - Clone repo locally, run build:
     ```bash
     cd frontend
     npm install
     npm run build
     ```
   - Upload the contents of `frontend/build` to the server path.
5. **Nginx Configuration**:
   - CloudPanel handles Nginx. Ensure the root points to `index.html`.

### Alternative: Docker Compose on CloudPanel
If you prefer to run everything via Docker on the VPS:
1. SSH into the server.
2. Clone the repository.
3. Run `docker-compose up -d --build`.
4. Use CloudPanel's **Reverse Proxy** feature to point domains to local ports `8080` (Frontend) and `3000` (Backend).
