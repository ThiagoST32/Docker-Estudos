# Documentation for Docker Commands

## Overview
This document provides a step-by-step guide for managing Docker containers and networks using macvlan. It includes commands for creating Docker images, setting up macvlan networks, running containers, testing connectivity, and cleaning up resources. Follow the instructions carefully to ensure proper configuration and operation.

This script demonstrates how to build and run a Docker container using the macvlan network mode. Below is a breakdown of the commands:

1. **Create Image**:
- Builds a Docker image from a specified path. Replace `<your-name-image>` with the desired name for your image and `/path` with the path to the Dockerfile.
- Command: docker build -t <your-name-image> /path

2. **Create Network**:
- Creates a macvlan network with the specified subnet, gateway, and parent interface. Replace `<parent-interface>` with the name of the parent network interface (e.g., `eth0`) and `<your-name-network>` with the desired name for your network.
- Command: docker network create --driver=macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=<parent-interface> <your-name-network>

3. **Run Container from Image Created**:
Runs a container using the previously created image and connects it to the specified macvlan network. Replace `<your-name-container>` with the desired container name, `<your-name-network>` with the name of the network, `<your-name-image>` with the image name, and `192.168.1.100` with the desired IP address for the container.
- Command: docker run -d --name=<your-name-container> --network=<your-name-network> --ip=192.168.1.100 <your-name-image>

4. **Testing Connection to Container**:
Tests the connection to the running container by sending an HTTP request to the container's IP address. Replace `192.168.1.100` with the IP address assigned to the container.
- Command: curl http://192.168.1.100

5. **Stop and Remove Container**:
    - The `docker stop` command stops the running container (`<your-name-container> `).
    - The `docker rm` command removes the stopped container to free up resources.
    - docker stop <your-name-container> 
    - docker rm <your-name-container> 

## Notes
    - Ensure that the parent interface used in the macvlan network creation is not actively in use by the host system to avoid conflicts.
    - When assigning a static IP address to the container, make sure it is within the subnet range of the macvlan network and not already in use.
    - Use `docker network ls` to list all networks and verify the creation of the macvlan network.
    - Use `docker ps` to list all running containers and confirm the container is running as expected.
    - If you encounter issues with connectivity, check the firewall rules and ensure that the macvlan network is properly configured.