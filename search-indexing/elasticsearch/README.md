# Search & Analytics: Elasticsearch + Kibana

This example sets up a single-node [Elasticsearch](https://www.elastic.co/elasticsearch) cluster with [Kibana](https://www.elastic.co/kibana) for full-text search, log analytics, and data visualization.

## Architecture

```
┌───────────────────────────┐      ┌───────────────────────────┐
│     Elasticsearch         │◄─────│         Kibana            │
│     Port: 9200            │      │         Port: 5601        │
│  (Search & Analytics)     │      │    (Visualization UI)     │
└───────────────────────────┘      └───────────────────────────┘
```

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- At least **4GB of available RAM** (Elasticsearch is memory-intensive)

> [!IMPORTANT]
> On Linux, you may need to increase the `vm.max_map_count` kernel setting:
>
> ```bash
> sudo sysctl -w vm.max_map_count=262144
> ```

## Quick Start

1. Start the stack:

    ```bash
    docker compose up -d
    ```

2. Wait for Elasticsearch to become healthy (~30-60 seconds on first start):

    ```bash
    docker compose ps
    ```

3. Access the services:

    - **Elasticsearch API**: [`http://localhost:9200`](http://localhost:9200)
    - **Kibana Dashboard**: [`http://localhost:5601`](http://localhost:5601)

## Adding Sample Data

Index a document:

```bash
curl -X POST 'http://localhost:9200/products/_doc/1' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Wireless Headphones",
    "category": "Electronics",
    "price": 79.99,
    "description": "Noise-cancelling over-ear headphones with 30h battery life"
  }'
```

Search for it:

```bash
curl 'http://localhost:9200/products/_search?pretty' \
  -H 'Content-Type: application/json' \
  -d '{ "query": { "match": { "description": "noise cancelling" } } }'
```

## Configuration

| Setting | Value | Description |
| :--- | :--- | :--- |
| Elasticsearch Port | `9200` | REST API |
| Kibana Port | `5601` | Web dashboard |
| Cluster mode | `single-node` | No clustering overhead for dev |
| Security | Disabled | For local development convenience |
| JVM Heap | `512MB` | Suitable for development workloads |

> [!WARNING]
> Security (`xpack.security`) is **disabled** for development simplicity. Never run this configuration in production without enabling authentication and TLS.

> [!TIP]
> The Elasticsearch and Kibana versions are **pinned to 8.17.0** to ensure compatibility. Always use matching versions for both services.

## Using Kibana

1. Open [`http://localhost:5601`](http://localhost:5601).
2. Go to **Management** → **Dev Tools** to run Elasticsearch queries interactively.
3. Go to **Analytics** → **Discover** to explore indexed data visually.
4. Create dashboards under **Analytics** → **Dashboard**.

## Stopping the Services

```bash
docker compose down
```

> [!NOTE]
> Indexed data is persisted in the `elasticsearch_data` volume. Use `docker compose down -v` to delete all data and start fresh.
