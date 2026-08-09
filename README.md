# ROS 2 + Fast DDS Discovery Server on Docker Bridge Networks

Docker networks using the `bridge` driver do not reliably support UDP multicast communication between containers. This can be a significant problem when running **ROS 2 nodes in isolated containers**, since ROS 2 relies on DDS for node discovery and DDS commonly uses multicast for discovery.

This repository provides a working setup based on **eProsima Fast DDS Discovery Server** that allows ROS 2 nodes running in separate containers to communicate over a standard Docker `bridge` network.

Instead of relying on multicast discovery, the **Fast DDS Discovery Server** acts as a centralized discovery mechanism. This allows the DDS discovery traffic to be handled through **unicast UDP communication** between the ROS 2 nodes and the discovery server, avoiding the multicast limitations of Docker bridge networks.

The setup is designed to be easily reusable: you can start from this repository and modify the services, containers, and ROS 2 nodes according to your needs without having to deal with the Fast DDS Discovery Server configuration from scratch.

---

## Requirements

- [Docker](https://docs.docker.com/get-docker/)
- Docker Compose
- At least **~20 GB of free disk space**

---

## How to Use

### 1. Allow Docker to access the X server

Before starting the containers, run:

```bash
xhost +local:root
```
Otherwise the screen of Gazebo won't show up

<br>

### 2. Build and run the project

Start the containers:

```bash
docker compose build && docker compose up
```

You should see the screen of Gazebo showing the drones. If drones didn't spawn immediately, just wait about 30 seconds, because the graphical models need to be downloaded from internet. So even if in the terminal you read "drones are spawned" but you don't actually see them, don't worry, you just need to wait.
