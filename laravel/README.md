
# Docker Compose Example for Laravel

Welcome to the Docker Compose example for Laravel! This example demonstrates how to set up a development environment for a Laravel application using Docker Compose. By containerizing the Laravel application and its dependencies, you can ensure consistency across different development environments and simplify the setup process for new team members.

## Table of Contents

- [Docker Compose Example for Laravel](#docker-compose-example-for-laravel)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [Usage](#usage)
  - [Directory Structure](#directory-structure)
  - [Customization](#customization)
  - [Contributing](#contributing)
  - [License](#license)

## Introduction

[Laravel](https://laravel.com/) is a popular PHP framework for building web applications. Docker Compose provides a convenient way to manage the dependencies required for running a Laravel application, such as the web server, database, and caching services.

This example sets up a development environment for a Laravel application using Docker Compose. It includes configurations for the following services:

- **laravel-app**: Container for the Laravel application.
- **mysql-db**: MySQL database container for storing application data.

## Prerequisites

Before you can use this example, ensure that you have the following prerequisites installed on your system:

- [Docker](https://docs.docker.com/get-docker/): Install Docker Engine to run Docker containers on your system.
- [Docker Compose](https://docs.docker.com/compose/install/): Install Docker Compose to define and run multi-container Docker applications using a YAML configuration file.

## Usage

To use this example, follow these steps:

1. Clone the repository to your local machine:

    ```bash
    git clone https://github.com/tamer-dev/docker-compose-examples.git
    ```

2. Navigate to the Laravel example directory:

    ```bash
    cd docker-compose-examples/laravel
    ```

3. Run `Docker Compose` :

    ```bash
    docker compose up -d
    ```

4. go to Project folder:

    ```bash
    cd src
    ```

5. make new fresh laravel project or git clone you project and skip this step:

    ```bash
    docker run --rm --interactive --tty --volume $PWD:/app composer create-project laravel/laravel .
    ```

6. or git clone you project and run:

    ```bash
    docker run --rm --interactive --tty --volume $PWD:/app composer install
    ```


## Directory Structure

The directory structure for this example is as follows:

```
laravel/
│
├── Dockerfile
├── src/
│   └── # Laravel application files
│
├── dbdata/
│   └── ... # mysql database files
│
├── docker-compose.yml
└── README.md
```

- **laravel-app/**: Contains the Dockerfile for building the Laravel application container and the source files for the Laravel application.
- **mysql-db/**: Contains configurations for the MySQL database container.
- **docker-compose.yml**: Defines the services and their configurations using Docker Compose.
- **README.md**: Provides instructions for setting up and using the Laravel example.

## Customization

You can customize this example according to your requirements by modifying the following files:

- **Dockerfile**: Customize the Dockerfile (Dockerfile8.2) for building the Laravel application container.
- **src/**: Place your Laravel application files in this directory.
- **docker-compose.yml**: Customize service names, ports, volumes, etc., according to your preferences.

## Contributing

Contributions to this repository are welcome! If you have improvements or additional features to suggest, feel free to open an issue or submit a pull request.

## License

This example is licensed under the [MIT License](../LICENSE), allowing you to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software. See the [LICENSE](../LICENSE) file for more details.

---

Feel free to adjust any details or add specific instructions relevant to your Laravel example!
