# AI Stack: Ollama + Open WebUI

This folder contains a Docker Compose configuration to spin up a fully local, private AI environment using **Ollama** and **Open WebUI**.

> [!NOTE]
> This setup provides a ChatGPT-like interface that runs entirely on your own hardware. Your data never leaves your machine.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- At least 8GB of RAM (16GB+ recommended for running larger models)

> [!TIP]
> If you have an NVIDIA GPU, you can [configure Docker to use it](https://docs.docker.com/compose/gpu-support/) for significantly faster inference times.

## Quick Start

1. Start the stack in the background:
    ```bash
    docker compose up -d
    ```

2. Wait a few moments for the containers to initialize.

3. Open your browser and navigate to the Open WebUI interface:
    [`http://localhost:3000`](http://localhost:3000)

4. Create an admin account (the first account created is automatically the administrator).

## Downloading Models

Ollama requires you to download a large language model before you can start chatting. You can do this directly from within Open WebUI.

1. In Open WebUI, click the settings icon (gear) in the bottom left.
2. Navigate to **Admin Settings** -> **Models**.
3. Under "Pull a model from Ollama.com", type the name of a model and click **Pull**.

### Popular Beginner Models:
- `llama3` - Meta's incredibly capable and fast model.
- `mistral` - A great all-around open-source model.
- `phi3` - Microsoft's very lightweight and fast model.

Alternatively, you run a command directly against the Ollama container to download a model:
```bash
docker exec -it ollama ollama run llama3
```

## Structure

- `docker-compose.yml`: Defines the Ollama backend and Open WebUI frontend services.
- Data persistence is handled via Docker named volumes (`ollama_data` and `open-webui_data`), so you won't lose your downloaded models or chat history when restarting the stack.

## Stopping the Services

To stop the containers without losing your data:
```bash
docker compose down
```

> [!WARNING]
> If you want to delete all your downloaded models and chat history, run `docker compose down -v`. **This cannot be undone!**
