# Cyber LMS

A modern, scalable, and interactive Learning Management System (LMS) built with React, Bun, Express, and PostgreSQL.

## 🚀 Features

- **Role-Based Access Control**: Student, Tutor, Admin, AI Tutor.
- **Course Management**: Video uploads, chapter structuring, and assessments.
- **Gamification**: XP points, progress tracking, and certificates.
- **AI-Powered**: AI Tutor and interactive site tour.
- **Modern UI/UX**: Built with Tailwind CSS and Framer Motion for fluid animations.

## 🛠 Tech Stack

### Frontend
- **ReactJS**: Component-based UI library.
- **Tailwind CSS**: Utility-first CSS framework.
- **Framer Motion**: Animation library.
- **Bun**: Fast JavaScript runtime and package manager.

### Backend
- **Express.js**: Web framework for Node.js/Bun.
- **Prisma**: Next-generation Node.js and TypeScript ORM.
- **PostgreSQL**: Relational database.
- **Bun**: Runtime.

### Infrastructure
- **Docker**: Containerization.
- **PgBouncer**: Lightweight connection pooler for PostgreSQL.

## 📦 Local Development

### Prerequisites
- Docker & Docker Compose
- Bun (optional, for local script execution)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/cyber-lms.git
   cd cyber-lms
   ```

2. **Environment Setup**
   Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

3. **Start the Application**
   Run the following command to build and start all services:
   ```bash
   docker-compose up --build
   ```

4. **Access the App**
   - Frontend: `http://localhost:8080`
   - Backend API: `http://localhost:3000`
   - Database: `localhost:5432`

## 📖 Documentation

For detailed deployment instructions, please refer to [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md).

## 🧪 Testing

To run tests (once implemented):
```bash
# Backend
cd backend
bun test

# Frontend
cd frontend
npm test
```
