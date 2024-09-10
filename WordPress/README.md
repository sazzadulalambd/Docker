

---
# WordPress Docker Setup

This Docker Compose configuration allows you to run a WordPress site with a MySQL database and phpMyAdmin for database management. The setup consists of three services:

1. **WordPress**: The main WordPress application.
2. **MySQL**: A MySQL 5.7 database for WordPress.
3. **phpMyAdmin**: A web-based database management tool for MySQL.

## Prerequisites

- Docker installed on your machine.
- Docker Compose installed.

## Getting Started

To start the services, navigate to the directory where the `docker-compose.yml` file is located and run the following command:

```bash
docker-compose up -d
```

This will pull the necessary images (if not already present) and start the services in detached mode.

### Accessing Services

Once the containers are running, you can access the following:

- **WordPress**: [http://localhost:8080](http://localhost:8080)
  - This will bring you to the WordPress setup page.
  
- **phpMyAdmin**: [http://localhost:8081](http://localhost:8081)
  - You can log in using the following credentials:
    - Server: `db`
    - Username: `root`
    - Password: `root_password`

### Stopping the Services

To stop the running services, execute:

```bash
docker-compose down
```

This will stop and remove the containers but will preserve the volumes for persistent data.

## Configuration Details

### WordPress Service

- **Image**: Built from the Dockerfile located in the same directory as the `docker-compose.yml`.
- **Ports**: The WordPress service is accessible on port `8080`.
- **Environment Variables**:
  - `WORDPRESS_DB_HOST`: Database host, pointing to the `db` container on port `3306`.
  - `WORDPRESS_DB_USER`: Username for the WordPress database.
  - `WORDPRESS_DB_PASSWORD`: Password for the WordPress database user.
  - `WORDPRESS_DB_NAME`: Name of the WordPress database.
- **Volumes**: `wordpress_data` is mounted to `/var/www/html` to persist WordPress files.

### MySQL Service

- **Image**: `mysql:5.7`
- **Ports**: MySQL runs internally and is only accessible by linked services.
- **Environment Variables**:
  - `MYSQL_ROOT_PASSWORD`: Root password for MySQL.
  - `MYSQL_DATABASE`: The WordPress database name.
  - `MYSQL_USER`: Username for the WordPress database.
  - `MYSQL_PASSWORD`: Password for the WordPress database user.
- **Volumes**: `db_data` is mounted to `/var/lib/mysql` for data persistence.

### phpMyAdmin Service

- **Image**: `phpmyadmin/phpmyadmin`
- **Ports**: The phpMyAdmin service is accessible on port `8081`.
- **Environment Variables**:
  - `PMA_HOST`: The MySQL service hostname, set to `db`.
  - `MYSQL_ROOT_PASSWORD`: The root password for MySQL to log into phpMyAdmin.

## Data Persistence

- **WordPress Data**: Stored in the `wordpress_data` volume.
- **MySQL Data**: Stored in the `db_data` volume.

## Customization

If you need to customize the database or WordPress configurations, you can modify the environment variables in the `docker-compose.yml` file.

- For WordPress, update the `WORDPRESS_DB_*` variables.
- For MySQL, update the `MYSQL_*` variables.

## Troubleshooting

- If the WordPress site is not accessible, ensure that the containers are running:
  
  ```bash
  docker-compose ps
  ```

- Check the logs for any errors:

  ```bash
  docker-compose logs
  ```

## Clean Up

To completely remove all services and their associated volumes (data will be lost), run:

```bash
docker-compose down -v
```

This will stop the services and delete the volumes used for WordPress and MySQL.

---


