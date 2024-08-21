Voting App with Traefik Ingress Controller:

This repository demonstrates the setup of a voting application using Docker Swarm, Traefik as an Ingress controller, and AWS services like Route 53 and Network Load Balancer (NLB).


Architecture Overview:

![image](https://github.com/user-attachments/assets/b93d8a24-8f2d-463c-a5d3-99a3845a1599) 


Route 53: Manages DNS routing for the domain.
Network Load Balancer (NLB): Balances incoming traffic.
Traefik: Acts as an Ingress controller.
Handles HTTP to HTTPS redirection.
Manages SSL decryption and offloading.
Voting and Result Services:
Vote Service: Listens on TCP port 80.
Result Service: Listens on TCP port 80.


Setup Instructions:

Docker and Docker Swarm installed
AWS CLI configured
Traefik configured with Docker Swarm


Deploy Swarm Cluster

Configure Traefik

Ensure Traefik is configured correctly in traefik.toml or traefik.yml. 
This setup should handle:

HTTP to HTTPS redirection
SSL certificate configuration
Routing rules for the vote and result services

Set up Route 53 and NLB

Configure your Route 53 DNS to point to the NLB.
Ensure the NLB forwards traffic to Traefik.
Access the Application

Open your browser and navigate to your domain to access the voting and result services.

Conclusion:
This setup demonstrates how to use Traefik as an Ingress controller with Docker Swarm, Route 53, and NLB to manage a simple voting application. 

