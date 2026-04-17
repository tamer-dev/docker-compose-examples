# DevTools: Hoppscotch — Open-Source API Development Platform

[Hoppscotch](https://hoppscotch.io/) is a lightweight, fast, and beautiful open-source API development ecosystem. It's a modern alternative to Postman that runs in your browser with a clean, minimalist interface for testing REST, GraphQL, WebSocket, and other API protocols.

## What Can You Do With Hoppscotch?

- 🚀 **Test APIs** with support for REST, GraphQL, WebSocket, SSE, MQTT, and SocketIO
- 📝 **Organize requests** into collections and workspaces
- 🔐 **Authentication** support for OAuth 2.0, Bearer tokens, Basic Auth, and more
- 📊 **Environment variables** for managing different configurations (dev, staging, prod)
- 🎨 **Beautiful UI** with dark mode and customizable themes
- 👥 **Team collaboration** with shared collections and workspaces
- 📜 **Request history** to track all your API calls
- 🔄 **Import/Export** collections from Postman, Insomnia, and OpenAPI specs

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Quick Start

1. Start Hoppscotch and PostgreSQL:

    ```bash
    docker compose up -d
    ```

2. Open Hoppscotch in your browser:

    - **Web App**: [`http://localhost:3000`](http://localhost:3000)
    - **Backend API**: [`http://localhost:3170`](http://localhost:3170)
    - **Admin Dashboard**: [`http://localhost:3100`](http://localhost:3100)

3. Start testing your APIs immediately — no account required for basic usage!

## Configuration

| Service | Port | Description |
| :--- | :--- | :--- |
| Hoppscotch Web App | `3000` | Main web UI for API testing |
| Hoppscotch Backend API | `3170` | Backend API server |
| Hoppscotch Admin Dashboard | `3100` | Admin dashboard for management |
| PostgreSQL | `5432` | Database for storing collections and user data |

### Environment Variables

The following environment variables are configured in the `docker-compose.yml`:

| Variable | Value | Description |
| :--- | :--- | :--- |
| `PRODUCTION` | `true` | Run in production mode |
| `ALLOW_SECURE_COOKIES` | `false` | Allow cookies over HTTP (for local development) |
| `VITE_ALLOWED_AUTH_PROVIDERS` | `GITHUB,GOOGLE,MICROSOFT,EMAIL` | Enabled authentication providers |

> [!TIP]
> For production deployments, you should configure proper authentication providers and use HTTPS with secure cookies enabled.

## Use Cases

### Testing a REST API

1. Open Hoppscotch at `http://localhost:3000`
2. Enter your API endpoint URL
3. Select the HTTP method (GET, POST, PUT, DELETE, etc.)
4. Add headers, query parameters, or request body as needed
5. Click **Send** to execute the request
6. View the response with syntax highlighting and formatting

### Creating Collections

1. Click on **Collections** in the sidebar
2. Click **New Collection** and give it a name
3. Add requests to your collection by clicking **Add Request**
4. Organize related API calls together for easy access

### Using Environment Variables

1. Click on **Environments** in the sidebar
2. Create a new environment (e.g., "Development", "Production")
3. Add variables like `base_url`, `api_key`, etc.
4. Use variables in requests with `<<variable_name>>` syntax
5. Switch between environments to test different configurations

### Testing GraphQL APIs

1. Select **GraphQL** from the request type dropdown
2. Enter your GraphQL endpoint URL
3. Write your query or mutation in the editor
4. Add variables if needed
5. Click **Send** to execute the GraphQL request

## Data Persistence

All your collections, environments, and settings are stored in the PostgreSQL database, which persists data in the `postgres_data` volume. Your data will be preserved even if you restart the containers.

## Stopping Hoppscotch

```bash
docker compose down
```

To remove all data including the database:

```bash
docker compose down -v
```

> [!WARNING]
> Using the `-v` flag will delete all your saved collections, environments, and user data permanently.

## Advanced Configuration

### Enabling OAuth Authentication

To enable OAuth authentication with GitHub, Google, or Microsoft:

1. Create OAuth apps in the respective provider's developer console
2. Update the `docker-compose.yml` with the OAuth credentials:

```yaml
environment:
  - GITHUB_CLIENT_ID=your_github_client_id
  - GITHUB_CLIENT_SECRET=your_github_client_secret
  - GOOGLE_CLIENT_ID=your_google_client_id
  - GOOGLE_CLIENT_SECRET=your_google_client_secret
  - MICROSOFT_CLIENT_ID=your_microsoft_client_id
  - MICROSOFT_CLIENT_SECRET=your_microsoft_client_secret
```

3. Restart the containers: `docker compose restart`

### Custom Database Configuration

To use a different PostgreSQL configuration:

```yaml
environment:
  POSTGRES_USER: your_custom_user
  POSTGRES_PASSWORD: your_secure_password
  POSTGRES_DB: your_database_name
```

Make sure to update the Hoppscotch service with the corresponding database connection string.

## Troubleshooting

### Cannot connect to the database

If Hoppscotch cannot connect to PostgreSQL, ensure both services are on the same network and the database is fully initialized:

```bash
docker compose logs postgres
docker compose logs hoppscotch
```

### Port 3000 already in use

If port 3000 is already occupied, change the port mapping in `docker-compose.yml`:

```yaml
ports:
  - "3001:3000"  # Use port 3001 instead
```

## Resources

- [Official Documentation](https://docs.hoppscotch.io/)
- [GitHub Repository](https://github.com/hoppscotch/hoppscotch)
- [Community Forum](https://github.com/hoppscotch/hoppscotch/discussions)
