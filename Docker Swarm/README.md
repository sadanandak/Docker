![image](https://github.com/user-attachments/assets/72b2d4b6-ca33-4a2c-aaf3-0df0f4372945) 

Docker Swarm Setup and Management:

Welcome to the Docker Swarm Setup and Management guide! This guide will walk you through setting up a Docker Swarm cluster, deploying services, and managing the cluster with simple commands.

Introduction:

Docker Swarm is a native clustering and orchestration tool for Docker containers. It allows you to manage a cluster of Docker engines as a single virtual system. This guide provides step-by-step instructions to set up and manage your Docker Swarm cluster.

Prerequisites:

Docker installed on all nodes
Access to multiple instances (machines or VMs) 

Setting Up Docker Swarm:

Initialize Docker Swarm on the first node: This command initializes the first node as the manager.

Join worker nodes: Use the worker join token on each worker node.

Join manager nodes: Use the manager join token on each additional manager node.

Verify the setup: Check the status of the Swarm and list all nodes to ensure they are correctly joined.

Check networks: View the networks available in the Swarm.


Commands:

# Initialize Docker Swarm on the first node
docker swarm init

# Join worker nodes
docker swarm join --token <worker-token> <manager-ip>:<manager-port>

# Join manager nodes
docker swarm join --token <manager-token> <manager-ip>:<manager-port>

# Check Swarm status
docker info

# List nodes
docker node ls

# Check networks
docker network ls


Deploying Services:

Deploy a sample service: Create a service with 3 replicas and publish it on port 8000.

Scale the service up and down: Adjust the number of replicas for the service.

Deploy service only on worker nodes: Ensure the service runs only on worker nodes.

Deploy a global service: Run the service on every node.


Commands:

# Deploy a sample service
docker service create --name app1 --replicas 3 --publish 8000:80 sadanandak/rollingupdate:v10

# Scale the service up
docker service scale app1=6

# Scale the service down
docker service scale app1=1

# Deploy service only on worker nodes
docker service create --name app1 --constraint node.role==worker --replicas 6 --publish 8000:80 sadanandak/rollingupdate:v10

# Deploy a global service (runs on every node)
docker service create --name monitor --publish 9100:9100 --mode global prom/node-exporter

docker service create --name cadvisor --publish 8888:8080 --mode global google/cadvisor:latest


Managing Services and Nodes:

Check service tasks: List the tasks of a service.

Put a node in maintenance mode: Drain the node to prevent it from running tasks.

Reactivate a node: Set the node back to active status.


Commands:

# Check service tasks
docker service ps app1

# Put a node in maintenance mode
docker node update <node-id> --availability drain

# Reactivate a node
docker node update <node-id> --availability active

Load Balancing:

To see load balancing in action, run the following command in a loop. This shows how requests are distributed across different nodes.

while true; do curl -sL http://<ip>:8000/ | grep -I 'IP-A'; sleep 1; done


Visualizing the Cluster:

Use Swarm Visualizer from GitHub to visualize your cluster. Access the visualizer at http://<manager-ip>:8080.

docker run -it -d -p 8080:8080 --name swarm-visualizer -e HOST=<manager-ip> -e PORT=<manager-port> dockersamples/visualizer

Conclusion:

Docker Swarm makes it easy to manage a cluster of Docker containers. With these simple commands, you can set up, deploy, and manage services across multiple nodes.
