# Dockerized Microservices Architecture

This project contains a set of Dockerized services for local development, including relational databases, NoSQL databases, a message broker, caching, search, monitoring tools, and a reverse proxy. All services are defined in a `docker-compose.yml` file, which makes it easy to spin up the entire stack with a single command.

## Services Included

1. **PostgreSQL**: Relational database for structured data.
2. **MongoDB**: NoSQL database for flexible schema data.
3. **MySQL**: Another relational database option.
4. **Redis**: In-memory cache for high-speed data access.
5. **RabbitMQ**: Message broker for handling asynchronous communication between services.
6. **Elasticsearch**: Search engine for indexing and querying large amounts of data.
7. **Kibana**: Web interface for visualizing Elasticsearch data.
8. **Nginx**: Reverse proxy and load balancer for routing traffic to different services.
9. **Prometheus**: Monitoring system for collecting metrics.
10. **Grafana**: Dashboard for visualizing metrics from Prometheus.

## Setup and Installation

### Prerequisites

- Docker (>= 19.03)
- Docker Compose (>= 1.27)

### Getting Started

1. Clone this repository:

   ```bash
   git clone <your-repository-url>
   cd <your-repository-directory>
   ```

2. Ensure you have Docker and Docker Compose installed on your machine.

3. Build and start the containers:

   ```bash
   docker-compose up
   ```

   This will start all the defined services and you can access the services as described below.

### Accessing the Services

- **RabbitMQ Management UI**: `http://localhost:15672` (Username: `user`, Password: `password`)
- **Kibana**: `http://localhost:5601`
- **Prometheus**: `http://localhost:9090`
- **Grafana**: `http://localhost:3000` (Username: `admin`, Password: `password`)
- **PostgreSQL**: Connect to `localhost:5432` using your preferred database tool.
- **MongoDB**: Connect to `localhost:27017` using your preferred database tool.
- **MySQL**: Connect to `localhost:3306` using your preferred database tool.
- **Redis**: Connect to `localhost:6379` for caching.

### Stopping the Services

To stop the services but keep the data, run:

```bash
docker-compose down
```

To stop and remove all containers, networks, and volumes (removes data):

```bash
docker-compose down -v
```

### Configuration Files

- **nginx.conf**: Contains the configuration for the Nginx reverse proxy.
- **prometheus.yml**: Configuration file for Prometheus to scrape metrics from services.

## Architecture Overview

The following diagram shows the architecture of the Dockerized app, representing the interactions between various services.

```
                       +------------+
                       |    Nginx   |
                       | (Reverse   |
                       |  Proxy)   |
                       +-----+------+
                             |
               +-------------+-------------+
               |                           |
    +----------v----------+        +-------v-------+
    |       Prometheus     |        |   Grafana     |
    | (Monitoring Service) |        | (Dashboard)   |
    +----------+-----------+        +---------------+
               |
         +-----v-----+
         |   Rabbit  |
         |   MQ      |
         +-----------+
               |
     +---------v----------+
     |        Redis        |
     |   (Caching Service) |
     +---------------------+
               |
    +----------v-----------+
    |      PostgreSQL       |
    |   (Relational DB)     |
    +-----------------------+
               |
    +----------v-----------+
    |      MySQL           |
    |   (Relational DB)    |
    +-----------------------+
               |
    +----------v-----------+
    |      MongoDB         |
    |   (NoSQL DB)         |
    +-----------------------+
               |
    +----------v-----------+
    |   Elasticsearch      |
    |    (Search Engine)   |
    +-----------------------+
               |
    +----------v-----------+
    |    Kibana            |
    |   (Visualize Logs)   |
    +-----------------------+

```

### How the Services Interact:

- **Nginx** acts as a reverse proxy, routing incoming HTTP requests to appropriate services.
- **Prometheus** collects metrics from all services for monitoring.
- **Grafana** visualizes the metrics provided by Prometheus.
- **RabbitMQ** facilitates message passing between services asynchronously.
- **Redis** is used as an in-memory cache to speed up data retrieval.
- **PostgreSQL**, **MySQL**, and **MongoDB** handle data storage, with PostgreSQL and MySQL providing relational databases and MongoDB providing a NoSQL solution.
- **Elasticsearch** indexes and allows full-text search across large datasets.
- **Kibana** provides a UI for interacting with and visualizing data stored in Elasticsearch.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
