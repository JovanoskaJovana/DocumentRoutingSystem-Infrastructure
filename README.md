# DocumentRoutingSystem — Infrastructure

This repository contains the Docker Compose configuration to run the full
Document Routing System stack locally, including the backend, frontend and database.

## Repositories

| Service  | Repository |
|----------|-----------|
| Backend  | [DocumentRoutingSystem-Backend](https://github.com/JovanoskaJovana/DocumentRoutingSystem-Backend) |
| Frontend | [DocumentRoutingSystem-Frontend](https://github.com/JovanoskaJovana/DocumentRoutingSystem-Frontend) |

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) installed and running
- [Git](https://git-scm.com/) installed

## Setup

### 1. Clone all three repositories into the same parent folder

```bash
git clone https://github.com/JovanoskaJovana/DocumentRoutingSystem-Backend.git
git clone https://github.com/JovanoskaJovana/DocumentRoutingSystem-Frontend.git
git clone https://github.com/JovanoskaJovana/DocumentRoutingSystem-Infrastructure.git
```

Your folder structure should look like this:
(parent folder)/

├── DocumentRoutingSystem-Backend/

├── DocumentRoutingSystem-Frontend/

└── DocumentRoutingSystem-Infrastructure/

### 2. Create the `.env` file

Inside `DocumentRoutingSystem-Infrastructure/`, create a file named `.env`:

```env
DB_PASSWORD=your_password_here
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRATION_TIME_MS=86400000
```

> The `.env` file is gitignored and will never be committed. You must create it manually.

### 3. Create the database dump
Export your local PostgreSQL database into a `backup.sql` file and place it inside `DocumentRoutingSystem-Infrastructure/`:
```bash
pg_dump -U postgres -d routingSystemDB > backup.sql
```
> ⚠️ `backup.sql` is gitignored and will never be committed. You must generate it from your local database manually.

### 4. Start the full stack

```bash
cd DocumentRoutingSystem-Infrastructure
docker-compose up --build
```

### 5. Stop the stack

```bash
docker-compose down
```

## Services

| Service  | URL                   |
|----------|-----------------------|
| Frontend | http://localhost      |
| Backend  | http://localhost:8080 |
| Database | localhost:5432        |

## Environment Variables

| Variable               | Description                        |
|------------------------|------------------------------------|
| `DB_PASSWORD`          | PostgreSQL password                |
| `JWT_SECRET`           | Secret key used to sign JWT tokens |
| `JWT_EXPIRATION_TIME_MS` | JWT token expiration in milliseconds (e.g. 86400000 = 24h) |
