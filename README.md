# Softy Pinko Docker Project

A comprehensive Docker containerization project that builds a scalable web application infrastructure with reverse proxy, load balancing, and horizontal scaling capabilities.

## Project Overview

This project demonstrates the progression from a simple containerized application to a sophisticated multi-container architecture featuring:

- **Backend API Server**: Flask application with CORS support
- **Frontend Static Server**: Nginx serving HTML/CSS/JS content
- **Reverse Proxy**: Nginx proxy routing requests to appropriate services
- **Load Balancing**: Round-robin distribution across multiple backend instances
- **Horizontal Scaling**: Dynamic scaling of API servers

## Architecture

```text
Client Request → Proxy Server (Port 80) → Frontend (Port 9000) or Backend (Port 5252)
                                      ↓
                               Load Balancer distributes to multiple Backend instances
```

## Prerequisites

- Docker Desktop installed and running
- Git for cloning repositories
- Basic understanding of Docker commands

## Project Structure

```text
holbertonschool-softy-pinko-docker/
├── task0/          # Basic Docker image
├── task1/          # Flask backend
├── task2/          # Frontend + Backend separation
├── task3/          # Frontend-Backend communication
├── task4/          # Docker Compose orchestration
├── task5/          # Reverse proxy implementation
└── task6/          # Horizontal scaling
```

## Tasks Overview

### Task 0: First Docker Image

Creates a basic Ubuntu container that outputs "Hello, World!"

**Build and Run:**

```bash
cd task0
sudo docker build -f ./Dockerfile -t softy-pinko:task0 .
sudo docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
```

### Task 1: Backend API

Flask application serving a REST API endpoint.

**Build and Run:**

```bash
cd task1
sudo docker build -f ./Dockerfile -t softy-pinko:task1 .
sudo docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
```

**Test:** Visit `http://localhost:5252/api/hello`

### Task 2: Frontend Static Server

Nginx server hosting static HTML content.

**Setup:**

```bash
cd task2/front-end
git clone https://github.com/atlas-school/softy-pinko-front-end.git
```

**Build and Run Frontend:**

```bash
sudo docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
sudo docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task2 softy-pinko-front-end:task2
```

**Test:** Visit `http://localhost:9000`

### Task 3: Frontend-Backend Communication

Enables AJAX communication between frontend and backend with CORS support.

**Requirements:**

- Add CORS support to Flask backend
- Modify HTML to include dynamic content from API
- Add JavaScript for API calls

**Run both services in separate terminals:**

```bash
# Terminal 1 - Backend
sudo docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
sudo docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3

# Terminal 2 - Frontend
sudo docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
sudo docker run -p 9000:9000 -it --rm --name softy-pinko-front-end-task3 softy-pinko-front-end:task3
```

### Task 4: Docker Compose

Orchestrates multiple containers with a single command.

**Run:**

```bash
cd task4
sudo docker-compose build
sudo docker-compose up
```

**Services:**

- Backend: `http://localhost:5252`
- Frontend: `http://localhost:9000`

### Task 5: Reverse Proxy

Implements Nginx reverse proxy for unified client access point.

**Architecture:**

- All client requests go through proxy on port 80
- Proxy routes `/` to frontend service
- Proxy routes `/api` to backend service

**Run:**

```bash
cd task5
sudo docker-compose build
sudo docker-compose up
```

**Test:** Visit `http://localhost` (port 80)

### Task 6: Horizontal Scaling

Demonstrates load balancing across multiple backend instances.

**Scale to 2 backend servers:**

```bash
cd task6
sudo docker-compose up --scale back-end=2
```

**Scale to 5 backend servers:**

```bash
sudo docker-compose up --scale back-end=5
```

**Observe:** Refresh the webpage multiple times and watch terminal output to see round-robin load distribution.

## Key Learning Concepts

### Docker Fundamentals

- Container creation and management
- Dockerfile best practices
- Port mapping and networking
- Volume management

### Microservices Architecture

- Service separation and independence
- Inter-service communication
- Container orchestration
- Scaling strategies

### Networking & Load Balancing

- Reverse proxy configuration
- Round-robin load balancing
- Docker internal DNS
- Port exposure vs. mapping

### DevOps Practices

- Infrastructure as Code (docker-compose.yml)
- Container orchestration
- Horizontal scaling
- Service dependencies

## Troubleshooting

### Permission Issues

If you encounter permission errors with Docker:

```bash
sudo usermod -aG docker $USER
# Then log out and back in
```

### Port Conflicts

Ensure no other services are running on required ports:

- Port 80 (proxy)
- Port 5252 (backend)
- Port 9000 (frontend)

### Build Context Errors

Always include the build context (dot) at the end:

```bash
sudo docker build -f ./Dockerfile -t image-name .
```

## Performance Considerations

- **Development vs Production**: This setup uses development servers (Flask's built-in server)
- **Security**: CORS is configured to allow all origins (not production-ready)
- **Scaling**: Docker Compose scaling is suitable for learning; production environments typically use Kubernetes or similar orchestration platforms

## Files Overview

### Dockerfiles

- Based on Ubuntu (backend) and Nginx (frontend/proxy)
- Include necessary dependencies and configurations
- Set appropriate working directories and commands

### Configuration Files

- `softy-pinko-front-end.conf`: Nginx configuration for static content
- `proxy.conf`: Nginx reverse proxy configuration
- `docker-compose.yml`: Multi-container orchestration

### Application Code

- `api.py`: Flask REST API with CORS support
- Modified `index.html`: Includes AJAX calls for dynamic content

## Next Steps

For production deployment, consider:

- Using production-grade WSGI servers (e.g., Gunicorn)
- Implementing proper security configurations
- Adding SSL/TLS termination
- Using container orchestration platforms (Kubernetes)
- Implementing health checks and monitoring
- Database integration and persistence

## Commands Reference

```bash
# Build images
sudo docker build -f ./Dockerfile -t image-name .

# Run containers
sudo docker run -p HOST_PORT:CONTAINER_PORT -it --rm --name container-name image-name

# Docker Compose
sudo docker-compose build
sudo docker-compose up
sudo docker-compose up --scale service-name=N

# Cleanup
sudo docker-compose down
sudo docker system prune
```
