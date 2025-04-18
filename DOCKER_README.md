# Poker Results Tracker - Docker Environment

This guide explains how to run the Poker Results Tracker application in a Docker environment, making it accessible from multiple devices on your local network.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (Docker Compose is included in modern Docker installations)

## Getting Started

1. Clone the repository (if you haven't already)
2. Navigate to the root directory of the project

## Running the Application

From the root directory of the project, run:

```bash
docker compose up -d
```

This will:
- Build and start the backend (NestJS)
- Build and start the frontend with Caddy web server
- Set up a PostgreSQL database
- Configure the network between all services

## Accessing the Application

### From your laptop:

- Frontend: `http://localhost`
- Backend API: `http://localhost:3000`

### From other devices on the same WiFi network:

1. Find your laptop's IP address:
   - On macOS: Open Terminal and run `ifconfig | grep "inet " | grep -v 127.0.0.1`
   - On Windows: Open Command Prompt and run `ipconfig`

2. Access the application:
   - Frontend: `http://<your-laptop-ip>`
   - Backend API: `http://<your-laptop-ip>:3000`

## Architecture

The Docker environment consists of three containers:

1. **poker-nestapp**: NestJS backend API running on port 3000
2. **poker-vueapp**: Vue.js frontend with Caddy web server running on port 80
3. **poker-postgres**: PostgreSQL database running on port 5433 (host) / 5432 (container)

Caddy serves the frontend application and automatically proxies API requests to the backend service.

## Stopping the Application

To stop the application:

```bash
docker compose down
```

To stop the application and remove all data (including the database):

```bash
docker compose down -v
```

## Rebuilding After Changes

If you make changes to the code, rebuild the containers:

```bash
docker compose up -d --build
```

## Data Persistence

The PostgreSQL data is persisted in a Docker volume. This means your data will remain even if you stop and restart the containers.
