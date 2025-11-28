# MEAN Stack CRUD Application with Docker Deployment

This is a full-stack MEAN (MongoDB, Express.js, Angular, Node.js) application with CRUD operations for managing tutorials.

## Features

- Create, read, update, and delete tutorials
- Search tutorials by title
- Responsive UI built with Angular
- RESTful API built with Node.js and Express
- MongoDB for data persistence

## Prerequisites

- Docker and Docker Compose
- Git
- A GitHub account
- A Docker Hub account

## Setup Instructions

### 1. Repository Setup

```bash
# Clone the repository
git clone <repository-url>
cd crud-mean-app
```

### 2. Environment Configuration

Set up the following secrets in your GitHub repository:

- `DOCKERHUB_USERNAME`: Your Docker Hub username
- `DOCKERHUB_TOKEN`: Your Docker Hub access token
- `VM_HOST`: IP address of your deployment VM
- `VM_USERNAME`: SSH username for your VM
- `VM_SSH_KEY`: Private SSH key for accessing your VM

### 3. Docker Configuration

The application uses Docker Compose with the following services:

- MongoDB: Database for storing tutorial data
- Backend: Node.js Express API server
- Frontend: Angular application served with Nginx
- Nginx: Reverse proxy for routing requests

### 4. Deployment

The application is deployed using GitHub Actions:

1. On push to main/master branch, Docker images are built and pushed to Docker Hub
2. The deployment bundle (`docker-compose.deploy.yml` + `nginx.conf`) is copied to the VM
3. Docker Compose is executed remotely to pull the latest images and restart the stack

### 5. Accessing the Application

After deployment, the application will be accessible at `http://your-vm-ip`

### 6. Preparing a New VM

1. Install Docker Engine and Docker Compose Plugin (or standalone `docker-compose`).
2. Create a working directory on the VM, e.g. `/home/ubuntu/mean-app`.
3. Make sure the VM user is in the `docker` group or run commands with `sudo`.
4. Configure the GitHub Secrets `VM_HOST`, `VM_USERNAME`, `VM_SSH_KEY`, `DOCKERHUB_USERNAME`, and `DOCKERHUB_TOKEN`.
5. The GitHub Action will copy `docker-compose.deploy.yml` and `nginx.conf` into the directory and run:

```bash
export DOCKERHUB_USERNAME=<your-dockerhub-username>
docker-compose -f docker-compose.deploy.yml pull
docker-compose -f docker-compose.deploy.yml up -d --force-recreate --remove-orphans
```

You can run the same commands manually on the VM whenever you need to redeploy. The compose file pulls the published backend (`mean-backend:latest`) and frontend (`mean-frontend:latest`) images and wires them together with MongoDB and Nginx.

## Project Structure

```
├── backend/              # Node.js Express backend
│   ├── app/
│   │   ├── controllers/  # Request handlers
│   │   ├── models/       # Mongoose models
│   │   └── routes/       # API routes
│   ├── Dockerfile        # Backend Docker configuration
│   └── server.js         # Entry point
├── frontend/             # Angular frontend
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/     # UI components
│   │   │   ├── models/         # Data models
│   │   │   └── services/       # HTTP services
│   ├── Dockerfile        # Frontend Docker configuration
│   └── nginx.conf        # Frontend Nginx configuration
├── docker-compose.yml    # Multi-container orchestration
├── nginx.conf            # Reverse proxy configuration
└── .github/workflows/    # CI/CD pipeline
```

## Development

To run locally:

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## API Endpoints

- `GET /api/tutorials` - Retrieve all tutorials
- `GET /api/tutorials/:id` - Retrieve a tutorial by ID
- `POST /api/tutorials` - Create a new tutorial
- `PUT /api/tutorials/:id` - Update a tutorial
- `DELETE /api/tutorials/:id` - Delete a tutorial
- `DELETE /api/tutorials` - Delete all tutorials
- `GET /api/tutorials?title=[title]` - Find tutorials by title
