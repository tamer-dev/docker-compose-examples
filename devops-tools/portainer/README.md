# DevTools: Portainer — Docker Management UI

[Portainer](https://www.portainer.io/) is a lightweight, open-source management UI that lets you easily manage your Docker environments through a beautiful web interface. Instead of memorizing CLI commands, you get a visual dashboard for containers, images, networks, volumes, and more.

## What Can You Do With Portainer?

- 🐳 **View & manage** all running containers, images, networks, and volumes
- 📊 **Monitor** real-time container stats (CPU, RAM, network I/O)
- 📝 **Inspect logs** from any container directly in the browser
- 🔄 **Deploy stacks** by pasting Docker Compose files into the UI
- 🖥️ **Open a console** into any running container with one click
- 🗑️ **Clean up** unused images and volumes visually

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Quick Start

1. Start Portainer:

    ```bash
    docker compose up -d
    ```

2. Open the Portainer UI in your browser:

    - **HTTPS**: [`https://localhost:9443`](https://localhost:9443) (self-signed certificate — accept the browser warning)
    - **HTTP**: [`http://localhost:9000`](http://localhost:9000)

3. On first launch, create an **admin account** with a strong password.

4. Select **"Get Started"** to connect to your local Docker environment.

## Configuration

| Setting | Value | Description |
| :--- | :--- | :--- |
| HTTPS Port | `9443` | Web UI with self-signed TLS |
| HTTP Port | `9000` | Web UI without TLS |
| Docker Socket | Mounted | Gives Portainer access to manage all containers |

> [!WARNING]
> Mounting the Docker socket (`/var/run/docker.sock`) gives Portainer **full control** over your Docker daemon. This is necessary for its functionality but should be used with caution in shared or production environments.

> [!TIP]
> After first login, you can disable the HTTP port (9000) in Portainer's settings and use only the secure HTTPS port (9443).

## Use Cases

### Deploy a Stack from the UI

1. In Portainer, go to **Stacks** → **Add stack**.
2. Give it a name and paste any `docker-compose.yml` content.
3. Click **Deploy the stack** — Portainer will pull images and start the services for you.

### Monitor Container Resources

1. Go to **Containers** and click on any running container.
2. Click the **Stats** tab to see live CPU, memory, and network usage graphs.

### Quick Terminal Access

1. Go to **Containers** and click on any running container.
2. Click the **Console** button and select `/bin/sh` or `/bin/bash`.
3. You now have a terminal session inside the container — right in your browser.

## Stopping Portainer

```bash
docker compose down
```

> [!NOTE]
> Your Portainer configuration (admin account, settings, stack definitions) is saved in the `portainer_data` volume and persists across restarts.
