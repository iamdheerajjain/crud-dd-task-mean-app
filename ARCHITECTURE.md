# Application Architecture

```mermaid
graph TD
    A[User Browser] --> B[Nginx Proxy - Port 80]
    B --> C[Frontend - Angular App]
    B --> D[Backend API - Node.js/Express - Port 8080]
    D --> E[MongoDB - Port 27017]

    subgraph Docker Container
        B
        C
        D
        E
    end

    subgraph GitHub Actions
        F[Build Backend Image]
        G[Build Frontend Image]
        H[Push to Docker Hub]
        I[Deploy to VM]
    end

    J[Docker Hub] --> K[VM Deployment]

    F --> H
    G --> H
    H --> J
    I --> K
```

## Component Descriptions

### User Browser

- Accesses the application through a web browser
- Connects to port 80 of the deployed VM

### Nginx Proxy

- Serves as the entry point for all requests
- Routes static content requests to the frontend
- Routes API requests (/api/\*) to the backend

### Frontend (Angular)

- Single-page application built with Angular 15
- Communicates with backend through HTTP requests
- Served by Nginx within its container

### Backend API (Node.js/Express)

- Provides RESTful API endpoints for tutorial management
- Connects to MongoDB for data persistence
- Handles CRUD operations for tutorials

### MongoDB

- Stores tutorial data with fields: ID, title, description, published status
- Uses volume mapping for persistent data storage

### CI/CD Pipeline

- Automated workflow triggered on code pushes to main branch
- Builds separate Docker images for frontend and backend
- Pushes images to Docker Hub
- Deploys latest images to VM through SSH
