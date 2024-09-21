# WordPress Docker Setup

This repository contains a simple Docker Compose setup for running a WordPress application with a MySQL database.

## Requirements

- Docker
- Docker Compose

## Getting Started

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/wordpress-docker-setup.git
   cd wordpress-docker-setup
   ```

2. Start the application:
   ```bash
   docker-compose up -d
   ```

3. Access your WordPress site at `http://localhost:8000`

## Docker Compose Configuration
The `docker-compose.yml` file defines the services:
   ```bash
    version: "3"
    services:
    db:
        image: mysql/mysql-server:8.0.23
        volumes:
            - db_data:/var/lib/mysql
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: root
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpress
            MYSQL_PASSWORD: wordpress
    web:
        depends_on:
        - db
        image: wordpress:latest
        ports:
        - "8000:80"
        restart: always
        environment:
            WORDPRESS_DB_HOST: db:3306
            WORDPRESS_DB_USER: wordpress
            WORDPRESS_DB_PASSWORD: wordpress
    volumes:
    db_data:
   ```
### Services Explained
- **db:** MySQL database service configured with a root password and a WordPress database.
- **web:** WordPress service that depends on the database service.

## Environment Variables
- `MYSQL_ROOT_PASSWORD:` Root password for MySQL.
- `MYSQL_DATABASE:` Name of the WordPress database.
- `MYSQL_USER:` Username for accessing the WordPress database.
- `MYSQL_PASSWORD:` Password for the WordPress database user.