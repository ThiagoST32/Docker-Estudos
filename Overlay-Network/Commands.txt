# Documentation for Docker Commands

## Overview
This document provides a step-by-step guide for managing Docker containers, images, and services. It includes commands for creating Docker images, initializing a Docker Swarm, setting up an overlay network, deploying services, testing connectivity, and cleaning up resources. Follow the instructions carefully to ensure proper configuration and operation of your Docker environment.

This script demonstrates how to build and run a Docker container using the overlay network mode. Below is a breakdown of the commands:

1. **Create Image**:
    - Build a Docker image using the `docker build` command.
    - Replace `<your-name-image>` with the desired name for your image.
    - Command: docker build -t <your-name-image.

2. **Initialize Docker Swarm**:
    - Use `docker swarm init` to initialize a Docker Swarm.
    - If you encounter an error during initialization, use `ip addr show <interface>` or `ip addr show enp64s0` to find the desired IP address 
    - And re-run the command with `--advertise-addr <desired-ip-address>`.
    - Command: docker swarm init --advertise-addr <desired-ip-address>

3. **Create Overlay Network**:
    - Create an overlay network using `docker network create`.
    - Replace `<your-network-name>` with the desired name for your network.
    - Command: docker network create --driver=overlay <your-network-name>

4. **Create Nginx Service**:
    - Use `docker service create` to create a service for Nginx.
    - Command: docker service create --name=<your-name-service> --network=my-over --replicas 2 <name-from-image-on-you-create>
    - Replace `<your-name-service>` with the desired service name.
    - Replace `<name-from-image-on-you-create>` with the name of the image you created earlier.
    - Use the `--network` flag to specify the overlay network (e.g., `my-over`).
    - Use the `--replicas` flag to specify the number of replicas (e.g., 2).

5. **Test Service Connectivity**:
    - Use `docker exec` to execute a `ping` command from a container.
    - Replace `<container-id>` with the ID of the container you want to use for testing.
    - Replace `<your-name-service>` with the name of the service to test connectivity.
    - Command: docker exec <container-id> ping <your-name-service> 

6. **Stop and Remove Container**:
    - The `docker stop` command stops the running container (`<your-name-container> `).
    - The `docker rm` command removes the stopped container to free up resources.
    - docker stop <your-name-container> 
    - docker rm <your-name-container> 

## Notes
    - Ensure Docker is installed and running on your system before executing these commands.
    - Use `docker ps` to list running containers and `docker ps -a` to list all containers.
    - Use `docker logs <container-id>` to view logs for a specific container.
    - Use `docker rm <container-id>` to remove a container and `docker rmi <image-id>` to remove an image.
    - Always verify the network and service configurations to avoid connectivity issues.
