# Docker Compose Example for MongoDB

Welcome to the Docker Compose example for MongoDB! This example demonstrates how to set up a MongoDB database using Docker Compose. By containerizing MongoDB, you can easily create isolated development environments for your MongoDB-based applications.


[MongoDB](https://www.mongodb.com/) is a popular NoSQL database that provides high performance, high availability, and easy scalability. Docker Compose allows you to define and run multi-container Docker applications, making it an excellent tool for managing MongoDB instances in development environments.

This example sets up a MongoDB database using Docker Compose. It includes configurations for a single MongoDB instance and exposes the default MongoDB port for connecting to the database.


## Usage

To use this example, follow these steps:

1. Clone the repository to your local machine:

    ```bash
    git clone https://github.com/tamer-dev/docker-compose-examples.git
    ```

2. Navigate to the MongoDB example directory:

    ```bash
    cd docker-compose-examples/databases/mongodb
    ```

3. Navigate to the MongoDB example directory:

    ```bash
    docker compose up -d
    ```

## Configuration

The Docker Compose configuration for MongoDB is defined in the `docker-compose.yml` file. You can customize the configuration according to your requirements by modifying this file. The default configuration includes the following services:

- **mongodb**: Container for the MongoDB database.
- **mongo-express**: Container for the web-based administrative interface for MongoDB.
## Customization

You can customize this example according to your requirements by modifying the following files:

- **docker-compose.yml**: Customize service names, ports, volumes, etc., according to your preferences.
