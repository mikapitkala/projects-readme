# Match-Me

<div align="center">
  <img src="art/main.png" alt="Match-Me Dashboard" width="100%">
  <br>
  
  ![Go](https://img.shields.io/badge/Go-1.23+-00ADD8?style=for-the-badge&logo=go&logoColor=white)
  ![React](https://img.shields.io/badge/React-18.2+-61DAFB?style=for-the-badge&logo=react&logoColor=black)
  ![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
  ![PostgreSQL](https://img.shields.io/badge/PostGIS-3.3+-336791?style=for-the-badge&logo=postgresql&logoColor=white)
  ![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker&logoColor=white)

  <p align="center">
    <b>A modern recommendation platform built for real-time connections.</b>
    <br />
    <a href="#-quick-start">Quick Start</a>
    ·
    <a href="docs/API_SPEC.md">API Spec</a>
    ·
    <a href="docs/FRONTEND_GUIDE.md">Frontend Guide</a>
    ·
    <a href="database/schema/ERD.md">Database Schema</a>
  </p>
</div>

---

## 🎯 Overview

**Match-Me** is a full-stack social platform that connects users based on intelligent compatibility scoring. By leveraging **PostGIS** for location services and a weighted algorithm for interests, it delivers personalized recommendations in real-time.

### Key Features
*   **🧠 Intelligent Matching**: Dynamic scoring based on bio, interests, and location.
*   **🌍 Geospatial Discovery**: Find connections nearby using PostGIS.
*   **💬 Real-Time Chat**: Instant messaging powered by WebSockets.
*   **🔐 Robust Auth**: JWT-based authentication with secure session handling.
*   **🎨 Interactive UI**: A responsive, "watercolor" themed React interface.

---

## 🚀 Quick Start

Get the entire stack (Database, Backend, Frontend) running with a single command using our custom launcher.

### Prerequisites
*   **Go** (1.23+)
*   **Docker & Docker Compose**
*   **Node.js** (18+)

### Installation

1.  **Start the Launcher:**
    You can run the pre-compiled binary for your OS (no Go required):

    *   **Windows**: `match-me-launcher-windows.exe`
    *   **Linux**: `./match-me-launcher-linux`
    *   **macOS (Apple Silicon)**: `./match-me-launcher-macos-arm64`
    *   **macOS (Intel)**: `./match-me-launcher-macos-amd64`

    *(Or for developers: `go run launcher.go`)*

    > **Note:** The launcher will automatically check for all system requirements (like Docker) and provide step-by-step instructions if anything is missing.

    This launches the **Developer Console**:
    *   🐳 PostgreSQL + PostGIS (Docker)
    *   🔌 Backend API (:8080)
    *   🎨 Frontend (:5173)

2.  **Initialize Data:**
    Inside the launcher menu, type:
    *   `s` to **Seed** the database with 100 fake users (Reset + Clean + Seed).
    *   `r` to **Reset** the database to a clean slate.

### Advanced Usage (Backend Makefile)

For granular control over the database/seed data, you can use the backend makefile targets (run from `backend/` folder):

```bash
cd backend
make db-clean  # Clean uploads folder (keep static assets)
make reseed    # Add 100 users without wiping the DB
```

---

## 📂 Documentation

| Topic | Description | Link |
|-------|-------------|------|
| **API** | Endpoints, Models, and Auth | [API Specification](docs/API_SPEC.md) |
| **Logic** | How the scoring algorithm works | [Algorithm Docs](docs/RECOMMENDATION_ALGORITHM.md) |
| **Schema** | Visual ERD and Table definitions | [ERD Diagram](database/schema/ERD.md) |
| **Frontend** | Component structure and styling | [Frontend Guide](docs/FRONTEND_GUIDE.md) |
| **Database** | Architecture, Migrations & Setup | [Database Guide](database/README.md) |
| **Examples** | Example API requests/responses | [API Examples](docs/API_EXAMPLES.md) |

---

## 🛠️ Tech Stack

*   **Backend**: Go (Chi Router), `lib/pq`
*   **Database**: PostgreSQL 15, PostGIS 3.3
*   **Frontend**: React, TypeScript, Vite, CSS Modules
*   **DevOps**: Docker Compose, Makefiles

## 📝 Configuration

Environment variables are managed via `.env` files.
See `backend/.env.example` for the default configuration.

```env
DATABASE_URL=postgres://matchme:matchme_dev_password@localhost:5433/matchme?sslmode=disable
PORT=8080
JWT_SECRET=your-secret-key
```

---

<div align="center">
  <sub>Built with ❤️ by the Match-Me Team</sub>
</div>
