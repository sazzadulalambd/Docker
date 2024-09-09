
---
# MySQL and phpMyAdmin Docker Compose Setup

This repository provides a Docker Compose setup for running MySQL along with phpMyAdmin for database management. This configuration allows you to easily deploy both MySQL and phpMyAdmin containers, facilitating a smooth database management experience.

## Configuration

The `docker-compose.yml` file defines two services:

- **MySQL**: A relational database service.
- **phpMyAdmin**: A web-based administrative tool for MySQL.

## Explanation

### MySQL Service
- **Image**: `mysql:latest`
- **Container Name**: `mysql_container`
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: `rootpassword`
  - `MYSQL_DATABASE`: `mydatabase`
  - `MYSQL_USER`: `admin`
  - `MYSQL_PASSWORD`: `adminpassword`
- **Ports**: Exposes port `3306` on the host machine.
- **Volumes**: Uses a named volume `mysql_data` to persist data.

### phpMyAdmin Service
- **Image**: `phpmyadmin/phpmyadmin:latest`
- **Container Name**: `phpmyadmin_container`
- **Environment Variables**:
  - `PMA_HOST`: `mysql` (the service name for MySQL)
  - `MYSQL_ROOT_PASSWORD`: `rootpassword` (used to connect as the root user)
- **Ports**: Exposes port `8080` on the host machine.

## Accessing phpMyAdmin

1. **URL**: [http://localhost:8080](http://localhost:8080) (or `http://<your-server-ip>:8080` if using a remote server).
2. **Login Credentials**:
   - **Server**: `mysql`
   - **Username**: `root` (or the `admin` user created in MySQL)
   - **Password**: `rootpassword` (or `adminpassword` for the `admin` user)

3. **Optional Adminer Service**
If you prefer using Adminer as an alternative administrative tool, you can uncomment the adminer service section in the docker-compose.yml file. Adminer provides a lightweight web-based interface for managing databases.


## How to Run

1. **Start the Containers**:
   ```bash
   docker compose up -d
   ```

2. **Stop and Remove Containers**:
   ```bash
   docker compose down
   ```


---