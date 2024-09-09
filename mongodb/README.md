
---

# MongoDB and Mongo Express Docker Setup

This setup uses Docker Compose to deploy MongoDB and Mongo Express services. Mongo Express is a web-based MongoDB admin interface.

## Docker Compose Configuration

The `docker-compose.yml` file defines two services:

1. **MongoDB**:
   - **Image**: `mongo:latest`
   - **Container Name**: `mongodb_container`
   - **Ports**: Exposes MongoDB on port 27017
   - **Volumes**: Persists data using the `mongo_data` volume
   - **Environment Variables**:
     - `MONGO_INITDB_ROOT_USERNAME`: root
     - `MONGO_INITDB_ROOT_PASSWORD`: password

2. **Mongo Express**:
   - **Image**: `mongo-express:latest`
   - **Container Name**: `mongo_express`
   - **Ports**: Exposes Mongo Express on port 8081
   - **Depends On**: Waits for MongoDB to be available
   - **Environment Variables**:
     - `ME_CONFIG_MONGODB_ADMINUSERNAME`: root
     - `ME_CONFIG_MONGODB_ADMINPASSWORD`: password
     - `ME_CONFIG_MONGODB_SERVER`: mongodb_container
     - `ME_CONFIG_BASICAUTH_USERNAME`: root
     - `ME_CONFIG_BASICAUTH_PASSWORD`: password

## Commands

### Start Services

To start the services defined in `docker-compose.yml`, run:

```sh
docker-compose up -d
```

The `-d` flag runs the containers in detached mode, allowing you to continue using your terminal.

### Stop Services

To stop the services and remove the containers, run:

```sh
docker-compose down
```

### Restart Services

To restart the services, you can use:

```sh
docker-compose down
docker-compose up -d
```

## Accessing Mongo Express

Once the services are running, you can access Mongo Express by opening your web browser and navigating to:

```
http://localhost:8081
```

**Basic Authentication**: Use the following credentials to log in:
- **Username**: root
- **Password**: password

## Volume

The MongoDB data is persisted using a Docker volume named `mongo_data`. This ensures that your data persists across container restarts.

To inspect the volume, you can use:

```sh
docker volume inspect mongo_data
```

## Additional Information

- **MongoDB**: A NoSQL database that stores data in flexible, JSON-like documents.
- **Mongo Express**: A web-based admin interface for MongoDB.



