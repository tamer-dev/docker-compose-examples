# Messaging: RabbitMQ with Management UI

This example sets up a **RabbitMQ** message broker with the built-in **Management Plugin**, providing a powerful web dashboard for managing queues, exchanges, bindings, and monitoring message flow in real time.

## Architecture

```
┌─────────────────────────────────────────┐
│              RabbitMQ                   │
│                                         │
│   AMQP Port: 5672   (for applications) │
│   Management: 15672  (Web Dashboard)   │
└─────────────────────────────────────────┘
```

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Quick Start

1. Start RabbitMQ:
    ```bash
    docker compose up -d
    ```

2. Wait for the healthcheck to confirm the broker is ready (~30 seconds on first start):
    ```bash
    docker compose ps
    ```
    Look for `healthy` in the status column.

3. Open the Management Dashboard:
   - **URL**: [`http://localhost:15672`](http://localhost:15672)
   - **Username**: `admin`
   - **Password**: `admin_secret`

## Configuration

| Setting | Value | Description |
|:--------|:------|:------------|
| AMQP Port | `5672` | Standard protocol port — connect your apps here |
| Management Port | `15672` | Web dashboard and HTTP API |
| Default User | `admin` | Admin username |
| Default Password | `admin_secret` | Admin password |
| Virtual Host | `/` | Default vhost |

> [!WARNING]
> The default credentials are for **development only**. For production, use a `.env` file with strong passwords and consider enabling TLS.

## Connecting from an Application

Use the following connection string from any app on the same Docker network or from the host machine:

```
amqp://admin:admin_secret@localhost:5672/
```

### Example: Quick test with Python (pika)

```python
import pika

connection = pika.BlockingConnection(
    pika.ConnectionParameters(
        host='localhost',
        credentials=pika.PlainCredentials('admin', 'admin_secret')
    )
)
channel = connection.channel()
channel.queue_declare(queue='hello')
channel.basic_publish(exchange='', routing_key='hello', body='Hello World!')
print(" [x] Sent 'Hello World!'")
connection.close()
```

## Healthcheck

The container includes a healthcheck using `rabbitmq-diagnostics ping`. The `start_period` of 30 seconds gives RabbitMQ enough time to boot before checks begin, preventing false-negative restarts.

## Stopping the Services

```bash
docker compose down
```

> [!NOTE]
> Queue definitions and messages are persisted in the `rabbitmq_data` volume. Use `docker compose down -v` to wipe all data.
