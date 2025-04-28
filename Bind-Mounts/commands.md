# Docker Compose MySQL Service with Named Volumes

This repository contains a Docker Compose configuration for setting up a MySQL database service with named volumes.

## Overview

This setup uses Docker Compose file format version 3.8 to define a MySQL service.

### Features

- **MySQL Version**: Runs a MySQL 8.0 container.
- **Container Name**: The container is named `mysql-volume`.
- **Environment Variable**: Sets the root password for MySQL to `123456` using the `MYSQL_ROOT_PASSWORD` environment variable.
- **Volume Mounting**: 
    - Maps the local directory `./mysql-data` to the container's `/var/lib/mysql` directory, which is where MySQL stores its data files.

## Usage

1. Ensure Docker and Docker Compose are installed on your system.
2. Clone this repository and navigate to the directory.
3. Run the following command to start the MySQL service:
     ```bash
     docker-compose up -d
     ```
4. The MySQL database will persist its data in the `./mysql-data` directory.

## Notes

- Modify the `MYSQL_ROOT_PASSWORD` in the Docker Compose file if a different root password is required.
- Ensure the `./mysql-data` directory has the appropriate permissions for Docker to write data.

