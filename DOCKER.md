# Docker Setup for LLM Council

This document provides instructions for running LLM Council using Docker Compose.

## Prerequisites

- Docker Desktop (Windows/Mac) or Docker Engine + Docker Compose V2 (Linux)
- `.env` file with your `OPENROUTER_API_KEY`

## Quick Start

1. **Create your `.env` file** in the project root:
   ```bash
   OPENROUTER_API_KEY=sk-or-v1-...
   ```

2. **Start the application**:
   ```bash
   docker compose up
   ```

3. **Access the application**:
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:8001

## Docker Commands

### Start services (detached mode)
```bash
docker compose up -d
```

### Stop services
```bash
docker compose down
```

### View logs
```bash
# All services
docker compose logs -f

# Specific service
docker compose logs -f backend
docker compose logs -f frontend
```

### Rebuild containers (after code changes)
```bash
docker compose up --build
```

### Stop and remove all containers, networks, and volumes
```bash
docker compose down -v
```

## Development Workflow

The Docker Compose setup includes volume mounts for hot-reloading:

- **Backend**: `./backend` is mounted to `/app/backend`
- **Frontend**: `./frontend/src` and `./frontend/public` are mounted
- **Data**: `./data` is mounted to persist conversation data

This means you can edit your code locally and see changes reflected in the running containers without rebuilding.

## Configuration

### Customizing Models

Edit `backend/config.py` to customize the council models. Changes will be reflected after restarting the backend service:

```bash
docker compose restart backend
```

### Port Changes

To change the default ports, edit `docker-compose.yml`:

```yaml
services:
  backend:
    ports:
      - "8001:8001"  # Change left side to desired host port
  frontend:
    ports:
      - "5173:5173"  # Change left side to desired host port
```

## Troubleshooting

### Port already in use
If you get a port conflict error, either:
1. Stop the service using that port
2. Change the port mapping in `docker-compose.yml`

### Permission issues (Linux)
If you encounter permission issues with the `data` directory:
```bash
sudo chown -R $USER:$USER data/
```

### Container won't start
Check the logs:
```bash
docker compose logs backend
docker compose logs frontend
```

### Fresh start
Remove all containers and volumes:
```bash
docker compose down -v
docker compose up --build
```

## Production Deployment

For production, you should:

1. Build optimized frontend:
   - Modify `Dockerfile.frontend` to build static files
   - Serve with nginx or similar

2. Use production-grade WSGI server:
   - Already using uvicorn in the backend

3. Set proper environment variables:
   - Use `.env` file or Docker secrets
   - Never commit `.env` to version control

4. Configure reverse proxy (nginx/traefik):
   - Handle SSL/TLS
   - Route traffic to containers

5. Use docker compose production overrides:
   ```bash
   docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
   ```
