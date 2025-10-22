# Tap2Serve - Microservices Architecture

A microservices-based application built with FastAPI, Docker, and nginx reverse proxy. This project demonstrates a scalable architecture with separate authentication and admin services.

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐
│   nginx-gateway │    │   auth-service  │
│   (Port 8080)   │────│   (Port 8001)   │
└─────────────────┘    └─────────────────┘
         │
         └──────────────┐
                        │
                ┌─────────────────┐
                │  admin-service  │
                │   (Port 8002)   │
                └─────────────────┘
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Git (for cloning the repository)

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd tap2serve
   ```

2. **Build the Docker images**
   ```bash
   # Build auth service
   docker build -t auth-service ./auth-service/
   
   # Build admin service  
   docker build -t admin-service ./admin-service/
   ```

3. **Start all services with Docker Compose**
   ```bash
   cd core
   docker compose up -d
   ```

4. **Access the services**
   - **Auth Service API Docs**: http://localhost:8080/auth/docs
   - **Admin Service API Docs**: http://localhost:8080/admin/docs

## 📋 Services Overview

### 🔐 Auth Service (Port 8001)
- Handles user authentication and authorization
- FastAPI-based service
- Accessible via `/auth/` endpoint through nginx gateway

### 👨‍💼 Admin Service (Port 8002)  
- Administrative functionality and management
- FastAPI-based service
- Accessible via `/admin/` endpoint through nginx gateway

### 🌐 Nginx Gateway (Port 8080)
- Reverse proxy for routing requests to appropriate services
- Load balancing and request forwarding
- Single entry point for all services

## 🛠️ Development Commands

### Docker Management

```bash
# Check Docker status
sudo systemctl status docker
sudo systemctl start docker

# View running containers
docker ps

# Stop and remove containers
docker compose down

# Start services in background
docker compose up -d

# View logs
docker compose logs -f
```

### Individual Service Management

```bash
# Build specific service
docker build -t auth-service ./auth-service/
docker build -t admin-service ./admin-service/

# Run individual service
docker run -d -p 8001:8001 auth-service
docker run -d -p 8002:8002 admin-service

# Stop specific container
docker ps                    # Find container ID
docker stop <container_id>
docker rm <container_id>
```

## 🔧 Configuration

### Nginx Configuration
The nginx gateway is configured via `default.conf`:
- Routes `/auth/` requests to auth-service:8001
- Routes `/admin/` requests to admin-service:8002
- Handles proper headers for proxy forwarding

### Docker Compose
The `docker-compose.yml` defines:
- Service dependencies
- Port mappings
- Volume mounts for nginx configuration
- Network connectivity between services

## 📁 Project Structure

```
tap2serve/
├── core/
│   ├── docker-compose.yml    # Multi-service orchestration
│   ├── default.conf          # Nginx configuration
│   └── README.md            # This file
├── auth-service/
│   ├── app/
│   │   └── main.py          # FastAPI application
│   ├── Dockerfile           # Auth service container
│   └── requirements.txt     # Python dependencies
├── admin-service/
│   ├── app/
│   │   └── main.py          # FastAPI application  
│   ├── Dockerfile           # Admin service container
│   └── requirements.txt     # Python dependencies
└── venv/                    # Python virtual environment
```

## 🐛 Troubleshooting

### Common Issues

1. **Port conflicts**: Ensure ports 8080, 8001, and 8002 are available
2. **Docker not running**: Start Docker service with `sudo systemctl start docker`
3. **Build failures**: Check Dockerfile syntax and dependencies
4. **Service not accessible**: Verify nginx configuration and service health

### Debugging Commands

```bash
# Check service logs
docker compose logs auth-service
docker compose logs admin-service
docker compose logs nginx-gateway

# Inspect container status
docker compose ps

# Test service connectivity
curl http://localhost:8080/auth/docs
curl http://localhost:8080/admin/docs
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with Docker Compose
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Note**: This is a development setup. For production deployment, consider additional security measures, environment variables, and monitoring solutions.




MONGO db start command in local

cd /usr/local/mongodb/bin

sudo ./mongod --dbpath /usr/local/mongodb/data --logpath /usr/local/mongodb/log/mongod.log



create dockerFile for each service
docker build .


