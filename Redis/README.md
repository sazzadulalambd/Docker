
---

# Docker Compose for Redis with Redis Commander (GUI)

This setup provides a Redis instance along with Redis Commander, a web-based GUI for managing Redis. The services are defined in the `docker-compose.yml` file, making it easy to spin up the environment.

## Prerequisites

Ensure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Services

### 1. Redis Service

- **Image:** `redis:latest`
- **Port:** `6379` (Default Redis port)
- **Volume:** Redis data is persisted in a Docker volume (`redis_data`).

### 2. Redis Commander (Admin Panel)

- **Image:** `rediscommander/redis-commander:latest`
- **Port:** `8081` (Accessible via browser)
- **Depends on:** The Redis service, ensuring Redis starts before the admin panel.
- **Environment Variable:** `REDIS_HOSTS` is used to point Redis Commander to the Redis service.

## How to Run

1. Clone the repository or copy the `docker-compose.yml` file.
2. Open a terminal and navigate to the directory where the file is located.
3. Run the following command to start the services in detached mode:

    ```bash
    docker-compose up -d
    ```

4. This will start both Redis and the Redis Commander admin panel.

## Access the Redis Admin Panel

After running the services, open your browser and go to:

- **URL:** `http://localhost:8081`

You will see the Redis Commander interface, where you can manage your Redis database.

If you're running this on a remote server, replace `localhost` with your server's IP address:

- **URL:** `http://<your-server-ip>:8081`

## Data Persistence

The Redis service uses a volume (`redis_data`) to persist data. This ensures that your data will not be lost when the containers are stopped or restarted.

## Stopping the Services

To stop the services, run:

```bash
docker-compose down
```

This will stop and remove the containers but keep the volume data intact. If you want to remove the volume as well, you can run:

```bash
docker-compose down --volumes
```

## Additional Notes

- You can customize the Redis and Redis Commander settings by modifying the `docker-compose.yml` file.
- For advanced configurations, refer to the official documentation of [Redis](https://redis.io/documentation) and [Redis Commander](https://github.com/joeferner/redis-commander).

---
