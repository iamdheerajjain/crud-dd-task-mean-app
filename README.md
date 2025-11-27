# MEAN Stack CRUD Application with Docker Deployment

This is a full-stack CRUD application built with the MEAN stack (MongoDB, Express.js, Angular, and Node.js). The application allows users to create, read, update, and delete tutorials with title, description, and published status.

## Features

- Create, read, update, delete tutorials
- Search tutorials by title
- Responsive UI built with Angular
- RESTful API built with Node.js and Express
- MongoDB for data persistence

## Project Setup

### Prerequisites

- Node.js (v14 or higher)
- Docker and Docker Compose
- Git
- A GitHub account
- A Docker Hub account

### Local Development Setup

#### Backend (Node.js Server)

```bash
cd backend
npm install
node server.js
```

The backend will run on `http://localhost:8080`.

You can update the MongoDB credentials by modifying the `db.config.js` file located in `app/config/`.

#### Frontend (Angular Client)

```bash
cd frontend
npm install
ng serve --port 8081
```

The frontend will run on `http://localhost:8081`.

You can modify the `src/app/services/tutorial.service.ts` file to adjust how the frontend interacts with the backend.

## Docker Deployment

This application is containerized using Docker and can be deployed using Docker Compose.

### Building and Running with Docker Compose

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd crud-dd-task-mean-app
   ```

2. Build and start all services:
   ```bash
   docker-compose up -d
   ```

3. Access the application at `http://localhost`

The Docker Compose setup includes:
- MongoDB database
- Node.js backend API
- Angular frontend served by Nginx

### Docker Images

Separate Dockerfiles are provided for both frontend and backend:

- Backend: `backend/Dockerfile`
- Frontend: `frontend/Dockerfile`

## CI/CD Pipeline

This project uses GitHub Actions for continuous integration and deployment.

### Setting Up GitHub Actions

1. Fork this repository to your GitHub account
2. Set up the following secrets in your repository settings:
   - `DOCKERHUB_USERNAME`: Your Docker Hub username
   - `DOCKERHUB_TOKEN`: Your Docker Hub access token
   - `VM_HOST`: IP address of your deployment VM
   - `VM_USERNAME`: SSH username for your VM
   - `VM_SSH_KEY`: Private SSH key for accessing your VM

3. Push changes to the `main` branch to trigger the workflow

The pipeline will:
- Build Docker images for frontend and backend
- Push images to Docker Hub
- Deploy to your VM using SSH

## Nginx Configuration

Nginx is used as a reverse proxy to serve the frontend and route API requests to the backend.

Configuration file: `frontend/nginx.conf`

Key features:
- Serves Angular frontend on port 80
- Proxies `/api/` requests to the backend service
- Handles Angular routing correctly

## Directory Structure

```
.
├── backend/
│   ├── app/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── models/
│   │   └── routes/
│   ├── Dockerfile
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/
│   │   │   ├── models/
│   │   │   └── services/
│   ├── Dockerfile
│   └── nginx.conf
├── docker-compose.yml
└── README.md
```

## Deployment Architecture

The application is deployed using Docker Compose with the following services:

1. **MongoDB**: Database for storing tutorial data
2. **Backend**: Node.js Express server exposing REST API
3. **Frontend**: Angular application served by Nginx

All services are connected through Docker's internal networking, with only port 80 exposed to the host for web access.