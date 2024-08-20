![image](https://github.com/user-attachments/assets/faeb7c91-dcc0-4790-be81-0562c3cb31e3) 

Docker Commands Explained:

Welcome to this GitHub repository! This guide will help you understand some basic Docker commands used in a Dockerfile. Let's break down the commands used in the Dockerfile for our project.


Dockerfile Overview:

FROM ubuntu:latest
LABEL name="sadanandak"
RUN mkdir /app
RUN groupadd appuser && useradd -r -g appuser appuser 
WORKDIR /app 
USER  appuser
ENV AWS_ACCESS_KEY_ID=DUMMYKEY \
    AWS_SECRET_KEY_ID=DUMMYKEY \
    AWS_DEFAULT_REGION=US-EAST-1A
COPY index.nginx-debian.html /var/www/html/
COPY scorekeeper.js /var/www/html
ADD  style.css /var/www/html
ADD https://releases.hashicorp.com/terraform/1.9.0/terraform_1.9.0_linux_amd64.zip /var/www/html
ARG T_VERSION='1.6.6' \
    P_VERSION='1.8.0'
EXPOSE 80
RUN apt update && apt install -y jq net-tools curl wget unzip \
    && apt install -y nginx iputils-ping 
RUN wget https://releases.hashicorp.com/terraform/${T_VERSION}/terraform_${T_VERSION}_linux_amd64.zip \
    && wget https://releases.hashicorp.com/packer/${P_VERSION}/packer_${P_VERSION}_linux_amd64.zip \
    && unzip terraform_${T_VERSION}_linux_amd64.zip && unzip packer_${P_VERSION}_linux_amd64.zip \
    && chmod 777 terraform && chmod 777 packer \
    && ./terraform version && ./packer version 
USER  appuser
CMD ["nginx","-g","daemon off;"] 

Explanation of Docker Commands:


FROM:


FROM ubuntu:latest
This command sets the base image for the Docker image. Here, we are using the latest version of Ubuntu.


LABEL:

LABEL name="sadanandak"
This command adds metadata to the image. In this case, we are labeling the image with a name.


RUN:


RUN mkdir /app
RUN groupadd appuser && useradd -r -g appuser appuser 
These commands execute commands inside the image. The first command creates a directory named /app. The second command creates a new group and a new user.

WORKDIR:


WORKDIR /app 
This command sets the working directory for the subsequent instructions. Here, it sets /app as the working directory.

USER:

USER  appuser
This command sets the user for the subsequent instructions. Here, it sets appuser as the user.

ENV:

ENV AWS_ACCESS_KEY_ID=DUMMYKEY \
    AWS_SECRET_KEY_ID=DUMMYKEY \
    AWS_DEFAULT_REGION=US-EAST-1A
This command sets environment variables inside the container.



COPY:

COPY index.nginx-debian.html /var/www/html/
COPY scorekeeper.js /var/www/html
These commands copy files from the host machine to the container. The first command copies index.nginx-debian.html to /var/www/html/, and the second copies scorekeeper.js to the same directory.


ADD:


ADD  style.css /var/www/html
ADD https://releases.hashicorp.com/terraform/1.9.0/terraform_1.9.0_linux_amd64.zip /var/www/html
These commands add files from the host machine or a URL to the container. The first command adds style.css to /var/www/html, and the second downloads and adds a file from a URL.

ARG:

ARG T_VERSION='1.6.6' \
    P_VERSION='1.8.0'
This command defines variables that users can pass at build-time to the builder with the docker build command.

EXPOSE:

EXPOSE 80
This command informs Docker that the container will listen on the specified network ports at runtime. Here, it exposes port 80.

CMD:

CMD ["nginx","-g","daemon off;"]
This command provides the default command to run when the container starts. Here, it starts the nginx server in the foreground.

Building and Running the Docker Image:

Build the Docker Image:

docker build -t my-app .

Run the Docker Container:

docker run -p 80:80 my-app
Now, your application should be up and running on port 80!

