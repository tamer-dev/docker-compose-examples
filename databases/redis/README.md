# Messaging & Caching: Redis + Redis Commander

This example sets up a **Redis** server with data persistence and password authentication, paired with **Redis Commander** — a web-based management tool for browsing keys, running commands, and inspecting data visually.

## Architecture

```
┌──────────────────────┐      ┌──────────────────────────┐
│       Redis          │◄─────│    Redis Commander       │
│   Port: 6379         │      │    Port: 8082            │
│   (In-memory store)  │      │    (Web UI)              │
└──────────────────────┘      └──────────────────────────┘
```

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Quick Start

1. Start the stack:
    ```bash
    docker compose up -d
    ```

2. Access the services:
   - **Redis Commander (Web UI)**: [`http://localhost:8082`](http://localhost:8082)
   - **Redis CLI** (from your terminal):
     ```bash
     docker exec -it redis redis-cli -a redis_secret
     ```

3. Try a basic command in Redis CLI:
    ```bash
    SET hello "world"
    GET hello
    ```

## Configuration

| Setting | Value | Description |
|:--------|:------|:------------|
| Redis Port | `6379` | Standard Redis port |
| Redis Password | `redis_secret` | Set via `--requirepass` flag |
| Persistence | AOF (Append Only File) | Enabled via `--appendonly yes` |
| Web UI Port | `8082` | Redis Commander interface |

> [!WARNING]
> The default password `redis_secret` is for **development only**. Always use a strong, unique password in production and store it in a `.env` file.

## Healthcheck

Redis includes a built-in healthcheck that pings the server every 10 seconds. Redis Commander will not start until Redis is confirmed healthy, preventing connection errors on startup.

## Stopping the Services

```bash
docker compose down
```

> [!NOTE]
> Data is persisted in the `redis_data` Docker volume. Use `docker compose down -v` to delete all stored data.
