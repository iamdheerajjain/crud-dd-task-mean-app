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
2. SSH connection is established with the deployment VM
3. Latest Docker images are pulled and containers are restarted

### 5. Accessing the Application

After deployment, the application will be accessible at `http://your-vm-ip`

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

## Jenkins CI/CD

