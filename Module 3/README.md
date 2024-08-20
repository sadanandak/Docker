![image](https://github.com/user-attachments/assets/79fbacbf-3a26-4a1e-bcdb-8e8fc45a1549) 

Introduction to Docker Containers:

Containers are stateless by nature, meaning if a container is deleted, all data within it is lost. This is where data persistence comes into play, ensuring your data remains intact even if the container is removed. We achieve this through Volumes and Bind Mounts.


Understanding Data Persistence:

Persistence means ensuring that even if a container is deleted, the data is not lost. There are two primary ways to achieve data persistence:

Volumes: Managed by Docker, ideal for data that needs to persist beyond the container's lifecycle.

Bind Mounts: Directly mounts a directory or file from the host system, useful for advanced scenarios.


Volumes vs Bind Mounts:

Volumes:

Managed by Docker.
Stored in a part of the host filesystem which is managed by Docker.
Preferred method for data persistence.

Bind Mounts:

Maps a file or directory on the host to a file or directory in the container.
More complex but provides flexibility to interact with the host system.

Practical Examples:

Using Volumes
List existing volumes:

docker volume ls

Create a new volume:

docker volume create mongodb

Run a MongoDB container with a volume:

docker run --rm -d --name mongodb -v mongodb:/data/db -p 27017:27017 mongo:latest

Check running containers:

docker ps

Insert some data:

docker exec -it mongodb mongosh

show dbs; Insert some data show dbs; db.hello.find();

Stop and start the container:

docker stop mongodb docker ps -a docker start mongodb exec -it mongodb mongosh


Using Bind Mounts:

Run a container without network access:

docker run --rm -d --name troubleshootingtools --network none troubleshootingtools:v10

Run a container with Docker socket mounted:

docker run --rm -d --name troubleshootingtools -v /var/run/docker.sock:/var/run/docker.sock --network none troubleshootingtools:v10

Inspect the container:

docker inspect troubleshootingtools


Docker Client and Daemon:

Docker Client:

Sends commands to the Docker daemon using the Docker socket.
Receives responses from the Docker daemon.
Docker Daemon:

Background service running on the host OS.
Manages Docker objects like images, containers, networks, and volumes.
Communicates with the Docker client.


Conclusion:

By understanding and using volumes and bind mounts, you can ensure data persistence in your Docker containers. This guide provides a solid foundation to start working with Docker and manage data effectively.

