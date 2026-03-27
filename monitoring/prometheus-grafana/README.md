# Monitoring Stack: Prometheus, Grafana, Node Exporter, & cAdvisor

This example provides a full-stack open-source monitoring solution. It collects metrics from the server hardware and running Docker containers, storing them in Prometheus and displaying them in beautiful Grafana dashboards.

## Architecture

- **Prometheus**: Time-series database that scrapes and stores metrics.
- **Grafana**: Visualization platform for creating dashboards.
- **Node Exporter**: Collects hardware and OS-level metrics (CPU, Memory, Disk).
- **cAdvisor**: Collects container-level metrics (how much CPU/RAM each Docker container uses).

## Quick Start

1. Start the stack in the background:
   ```bash
   docker compose up -d
   ```

2. Access the services in your browser:

   - **Grafana**: [`http://localhost:8080`](http://localhost:8080)
      - Username: `admin`
      - Password: `admin` (You will be prompted to change this on your first login)
   - **Prometheus**: [`http://localhost:9090`](http://localhost:9090)
   - **cAdvisor Web UI**: [`http://localhost:8081`](http://localhost:8081)

## Configuring Grafana

Before you can see graphs in Grafana, you need to connect it to Prometheus:

1. Log in to Grafana.
2. Go to **Connections** -> **Data Sources**.
3. Click **Add data source** and select **Prometheus**.
4. Set the **Prometheus server URL** to: `http://prometheus:9090` (this uses the internal Docker network).
5. Scroll down to the bottom and click **Save & test**. You should see a green success message.

## Importing Dashboards

Instead of building dashboards from scratch, you can import community-created ones.

1. In Grafana, go to **Dashboards** -> **Import**.
2. To monitor your server hardware (Node Exporter), use dashboard ID `1860`.
3. To monitor your Docker containers (cAdvisor), use dashboard ID `14282` or `11600`.
4. Enter the ID, click **Load**, select your Prometheus data source, and click **Import**.

## Stopping the Services

```bash
docker compose down
```

Data is persisted via Docker volumes, so your Prometheus history and Grafana dashboards will be saved across restarts.
