# Docker Named Volumes Commands

This file contains commands related to Docker named volumes. Below is an explanation of each step:

## 1. Create a Named Volume
```bash
docker volume create mysql-data
```
- This command creates a named volume called `mysql-data` for persistent data storage. Named volumes allow data to persist even if the container is removed.

## 2. Run a MySQL Container with the Named Volume
```bash
docker run -d --name=mysql-volume -e MYSQL_ROOT_PASSWORD=123 -v mysql-data:/var/lib/mysql mysql:8.0
```
- This command runs a MySQL container in detached mode (`-d`) with the name `mysql-volume`.
- The `-e MYSQL_ROOT_PASSWORD=123` sets the root password for MySQL.
- The `-v mysql-data:/var/lib/mysql` mounts the named volume `mysql-data` to the MySQL data directory inside the container.

## 3. Remove the MySQL Container
```bash
docker rm -f mysql-volume
```
- This command forcefully removes the running MySQL container named `mysql-volume`.

## 4. Re-run the MySQL Container with the Same Named Volume
```bash
docker run -d --name=mysql-volume -e MYSQL_ROOT_PASSWORD=123 -v mysql-data:/var/lib/mysql mysql:8.0
```
- This step demonstrates how to re-run the MySQL container using the same named volume `mysql-data`. The data persists because it is stored in the named volume.

By following these steps, you can create, use, and reuse Docker named volumes for persistent data storage in containers.

## 5. Access the MySQL Database in the Container
```bash
docker exec -it mysql-volume mysql -u root -p
```
- This command allows you to access the MySQL database running inside the container.
- The `docker exec -it mysql-volume` part specifies that you want to execute a command interactively inside the container named `mysql-volume`.
- The `mysql -u root -p` part runs the MySQL client as the root user. You will be prompted to enter the root password (`123` in this case) to access the database.
- Once inside, you can execute SQL commands to interact with the database.
