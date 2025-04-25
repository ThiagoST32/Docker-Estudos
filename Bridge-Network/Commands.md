# Documentation for Docker Commands

## Overview
This document demonstrates the creation of a Docker bridge network, building a Docker image, running multiple containers on the same network, and testing communication between the containers.

This script demonstrates how to build and run a Docker container using the bridge network mode. Below is a breakdown of the commands:

## Commands Explanation

1. **Create a Docker Bridge Network**:
    - `docker network create --driver=bridge my-net`
    - Creates a custom bridge network named `my-net` to allow containers to communicate with each other.

2. **Build a Docker Image**:
    - `docker build -t my-app .`
    - Builds a Docker image from the current directory (`.`) and tags it as `my-app`.

3. **Run Containers on the Custom Network**:
    - `docker run -d --name=app1 --network=my-net my-app`
    - Runs a container named `app1` in detached mode (`-d`) using the `my-app` image and connects it to the `my-net` network.
    - `docker run -d --name=app2 --network=my-net my-app`
    - Runs another container named `app2` in detached mode using the same image and network.

4. **Access a Running Container**:
    - `docker exec -it app1 /bin/bash`
    - Opens an interactive terminal session inside the `app1` container.

5. **Install Required Tools**:
    - `apt-get update`
    - Updates the package list inside the container.
    - `apt-get install curl -y`
    - Installs the `curl` utility inside the container.

6. **Test Communication Between Containers**:
    - `curl http://app2:8000`
    - Sends an HTTP request from `app1` to `app2` on port `8000` to verify inter-container communication.

7. **Stop and Remove Container**:
    - The `docker stop` command stops the running container (`<your-name-container> `).
    - The `docker rm` command removes the stopped container to free up resources.
    - docker stop <your-name-container> 
    - docker rm <your-name-container> 

## Notes
    - Ensure Docker is installed and running on your system.
    - Replace `8000` with the appropriate port if the application in `app2` listens on a different port.
    - The `apt-get` commands assume the container is based on a Debian/Ubuntu image. Adjust commands for other base images as needed.