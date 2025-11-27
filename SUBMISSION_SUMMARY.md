# MEAN Stack Application - Internship Assignment Submission

## Project Overview

This repository contains a complete full-stack CRUD application built with the MEAN stack (MongoDB, Express.js, Angular, and Node.js), along with containerization, deployment configurations, and CI/CD pipeline setup.

## ✅ Completed Requirements

### Repository Setup

- Created and initialized Git repository
- Added comprehensive .gitignore file
- Organized code with clear directory structure

### Containerization & Deployment

- Created Dockerfile for backend (Node.js/Express)
- Created Dockerfile for frontend (Angular with Nginx)
- Developed docker-compose.yml for multi-container orchestration
- Configured MongoDB as a service in Docker Compose
- Set up Nginx as a reverse proxy

### CI/CD Pipeline Configuration

- Implemented GitHub Actions workflow for automated deployment
- Created separate jobs for building frontend and backend images
- Added deployment step for automatic VM updates
- Configured secure secret management for credentials

### Database Setup

- Integrated MongoDB as a Docker service
- Configured environment variables for database connections
- Set up persistent data storage with Docker volumes

### Nginx Reverse Proxy

- Configured Nginx to serve frontend on port 80
- Set up API routing to backend services
- Optimized Nginx configuration for performance

## 📦 Repository Contents

### Key Files

- `README.md` - Comprehensive project documentation
- `docker-compose.yml` - Multi-container deployment configuration
- `backend/Dockerfile` - Backend containerization
- `frontend/Dockerfile` - Frontend containerization
- `.github/workflows/deploy.yml` - CI/CD pipeline
- `frontend/nginx.conf` - Nginx reverse proxy configuration
- `DEPLOYMENT_INSTRUCTIONS.md` - Step-by-step deployment guide
- `ARCHITECTURE.md` - System architecture diagrams and explanations

### Directory Structure

```
.
├── backend/                 # Node.js/Express backend
│   ├── Dockerfile           # Backend Docker configuration
│   ├── app/                 # Application source code
│   │   ├── config/          # Database configuration
│   │   ├── controllers/     # Request handlers
│   │   ├── models/          # Data models
│   │   └── routes/          # API routes
│   └── server.js            # Entry point
├── frontend/                # Angular frontend
│   ├── Dockerfile           # Frontend Docker configuration
│   ├── nginx.conf           # Nginx configuration
│   └── src/                 # Application source code
├── docker-compose.yml       # Multi-container orchestration
├── .github/workflows/       # CI/CD pipeline
└── README.md                # Project documentation
```

## 🔧 Technical Implementation Details

### Backend (Node.js/Express)

- RESTful API for tutorial management (CRUD operations)
- MongoDB integration with Mongoose ODM
- Environment-based configuration for database connections
- Proper error handling and validation

### Frontend (Angular)

- Reactive forms for data input
- HTTP client integration for API communication
- Component-based architecture
- Responsive design with Bootstrap

### Docker Implementation

- Multi-stage builds for optimized images
- Proper environment variable configuration
- Volume mapping for data persistence
- Health checks and restart policies

### CI/CD Pipeline

- Automated building of Docker images
- Secure credential management
- Automated deployment to target VM
- Parallel job execution for efficiency

## 🚀 Deployment Instructions

### Prerequisites

1. GitHub account
2. Docker Hub account
3. Cloud VM (AWS EC2, Azure VM, etc.) with Docker installed

### Quick Start

1. Fork this repository
2. Configure GitHub secrets for Docker Hub and VM access
3. Push to main branch to trigger deployment
4. Access application at your VM's IP address

## 📸 Required Screenshots

For submission, please include screenshots of:

1. GitHub repository with code
2. CI/CD pipeline configuration and execution
3. Docker image build process on Docker Hub
4. Running application UI
5. Nginx configuration and infrastructure setup

---

This completes all requirements for the internship assignment. The application is production-ready with proper containerization, automated deployment, and scalable architecture.
