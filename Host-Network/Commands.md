# Documentation

## Overview
This document provides a step-by-step guide to building and running a Docker container using the host network mode. The host network mode allows the container to share the same network namespace as the host, enabling direct access to the host's network interfaces. This can be useful for performance optimization or specific use cases where the container needs to interact closely with the host's network.

This script demonstrates how to build and run a Docker container using the host network mode. Below is a breakdown of the commands:

1. **Build Docker Image**:
    - The `docker build` command is used to create a Docker image from a Dockerfile located in the specified path.
    - The `-t` flag assigns a name (`net-host`) to the image for easier reference.
    - docker build -t <your-name-image> /path

2. **Run Docker Container**:
    - The `docker run` command starts a container using the previously built image (`net-host`).
    - The `-d` flag runs the container in detached mode (in the background).
    - The `--name` flag assigns a name (`nginx-host`) to the container.
    - The `--network=host` option configures the container to use the host's network stack, allowing it to share the same network namespace as the host.
    - The `net-host` select the image created
    - docker run -d --name=<your-name-container> --network=host <your-name-image>

3. **Test Connection**:
    - The `curl` command is used to test the connection to the containerized application by sending an HTTP request to `http://localhost`.
    - Since the container uses the host network, it is accessible via the host's `localhost`.
    - curl http://localhost

4. **Stop and Remove Container**:
    - The `docker stop` command stops the running container (`<your-name-container> `).
    - The `docker rm` command removes the stopped container to free up resources.
    - docker stop <your-name-container> 
    - docker rm <your-name-container> 

# Notes:
    - Ensure Docker is installed and running on your system before executing these commands.
    - Replace `<your-name-image>` and `<your-name-container>` with appropriate names for your image and container.
    - Using `--network=host` can expose the container to the host's network, which may have security implications. Use it cautiously.
    - Test the application thoroughly to ensure it behaves as expected when using the host network mode.
    - Clean up unused images and containers regularly to save disk space.

