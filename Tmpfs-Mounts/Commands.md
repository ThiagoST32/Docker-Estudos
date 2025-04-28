
# Docker Compose Example: Tmpfs Mounts

This example demonstrates how to use a temporary filesystem (tmpfs) mount in a Docker Compose configuration.

## Overview

The provided Docker Compose file defines a service named `app` using the `nginx:latest` image. Key configurations include:

1. **Container Name**: The container is named `nginx-tmps`.
2. **Tmpfs Mount**: A temporary filesystem (tmpfs) is mounted at `/tmp/cache` with a size limit of 128k. Tmpfs is a RAM-backed filesystem, meaning data stored here is not persisted and is lost when the container stops.
3. **Command**: The container runs a shell command to write a test file (`teste.txt`) to the tmpfs mount and then starts the Nginx server.

## Docker Compose File

```yaml
version: '3.8'
services:
    app:
        image: nginx:latest
        container_name: nginx-tmps
        tmpfs:
            - /tmp/cache:size=128k
        command: sh -c "echo 'Teste Tmpfs' > /tmp/cache/teste.txt && nginx -g 'daemon off;'"
        restart: unless-stopped
```

## Step-by-Step Explanation

1. **docker-compose up -d**  
   Starts the container in detached mode using the Docker Compose configuration.

2. **docker ps -a**  
   Lists all containers, including the `nginx-tmps` container, to verify it is running.

3. **docker exec nginx-tmps df -h /tmp/cache**  
   Displays the filesystem usage for the tmpfs mount at `/tmp/cache`.

4. **docker exec nginx-tmps ls /tmp/cache**  
   Lists the contents of the tmpfs mount to confirm the presence of the `teste.txt` file.

5. **docker exec nginx-tmps cat /tmp/cache/teste.txt**  
   Outputs the content of the `teste.txt` file to verify it was written correctly.

6. **docker-compose stop**  
   Stops the running container while retaining its configuration for future use.

## Notes

- The `tmpfs` mount is ideal for scenarios where temporary, non-persistent storage is required.
- The `restart: unless-stopped` policy ensures the container restarts automatically unless explicitly stopped.
- Tmpfs mounts are useful for improving performance by reducing disk I/O since data is stored in memory.
- Be cautious with the size of the tmpfs mount to avoid excessive memory usage, which could impact other processes on the host system.
- Tmpfs is not suitable for storing data that needs to persist beyond the container's lifecycle.
- This example demonstrates a simple use case, but tmpfs mounts can also be used in more complex scenarios, such as caching or temporary data processing.
- Always monitor resource usage when using tmpfs mounts in production environments.
