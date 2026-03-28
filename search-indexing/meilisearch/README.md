# Search & Indexing: Meilisearch

This example sets up [Meilisearch](https://www.meilisearch.com/) — a lightning-fast, open-source search engine that is easy to use and deploy. It provides typo-tolerant, relevant search results out of the box with zero configuration.

## Why Meilisearch?

| Feature | Meilisearch | Elasticsearch |
| :--- | :--- | :--- |
| Setup complexity | Minimal — single binary | Complex — JVM, clusters |
| Memory footprint | ~50MB idle | ~1GB+ idle |
| Typo tolerance | Built-in | Requires configuration |
| Web dashboard | Built-in (Mini Dashboard) | Requires Kibana |
| Best for | Apps, e-commerce, docs search | Log analytics, big data |

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Quick Start

1. Start Meilisearch:

    ```bash
    docker compose up -d
    ```

2. Open the built-in **Mini Dashboard** in your browser:

    [`http://localhost:7700`](http://localhost:7700)

3. When prompted for an API key, enter:

    ```
    meilisearch_master_key
    ```

## Adding Sample Data

You can index data instantly using `curl`. Here's an example that creates a "movies" index:

```bash
curl -X POST 'http://localhost:7700/indexes/movies/documents' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer meilisearch_master_key' \
  --data-binary '[
    { "id": 1, "title": "The Dark Knight", "genre": "Action" },
    { "id": 2, "title": "Inception", "genre": "Sci-Fi" },
    { "id": 3, "title": "Interstellar", "genre": "Sci-Fi" },
    { "id": 4, "title": "The Prestige", "genre": "Drama" }
  ]'
```

Then search for a movie (even with a typo!):

```bash
curl 'http://localhost:7700/indexes/movies/search' \
  -H 'Authorization: Bearer meilisearch_master_key' \
  -d '{ "q": "dark nigt" }'
```

Meilisearch will correctly return "The Dark Knight" thanks to built-in typo tolerance.

## Configuration

| Setting | Value | Description |
| :--- | :--- | :--- |
| Port | `7700` | HTTP API and Mini Dashboard |
| Master Key | `meilisearch_master_key` | Required for all API calls |
| Environment | `development` | Enables the Mini Dashboard |

> [!WARNING]
> The default master key is for **development only**. In production, set `MEILI_ENV: production` and use a strong, random master key stored in a `.env` file.

> [!TIP]
> In `development` mode, Meilisearch serves a built-in Mini Dashboard at the root URL. In `production` mode, only the API is available.

## Stopping the Service

```bash
docker compose down
```

> [!NOTE]
> Indexed data is persisted in the `meilisearch_data` volume. Use `docker compose down -v` to delete all indexes and data.
