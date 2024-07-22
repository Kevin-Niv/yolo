# Moringa Devop6 IP2 E-Commerce Microservice Project
![poster](/images/Yolo.png)


# Overview

This e-commerce application leverages React for the frontend and Node.js with Express for the backend, connected to a MongoDB database. Using Docker, each component (frontend, backend, MongoDB) is containerized with Dockerfiles and orchestrated with docker-compose. After building the Docker images, they are pushed to Docker Hub for deployment. This approach ensures consistency across development and production environments, facilitates easy scaling, and simplifies deployment management using containerization technologies.

## Event Format

Hands on IP2 (Dev06 IP2 Project)

## Dockerfile directives used in building and running containers 
### Node Version

+ `NODE_VERSION` =`19.0.0-alpine`

### Dockerfile Directives
 #### Build Stage

- `ARG NODE_VERSION`=`19.0.0-alpine`

- `FROM node:${NODE_VERSION} as builder`
    Use the specified Node.js version from the Docker image registry and name this stage 'builder'.

- `WORKDIR /usr/src/app`
    Set the working directory inside the container where subsequent commands will be executed.

- `COPY package*.json ./`
    Copy package.json and package-lock.json (if present) from the host to the container's working directory.
    This prepares for installing dependencies.

- `RUN npm install --production`
    Run npm install to install Node.js dependencies defined in package.json.
    The --production flag skips installation of development dependencies, optimizing the image size.

- `COPY . .`
    Copy all files from the current directory of the host into the container's working directory.
    This includes application source code and any other necessary files.

 #### Runner Stage

- `FROM node:${NODE_VERSION} as runner `
    Use the same Node.js version as the 'builder' stage and name this stage 'runner'.

- `WORKDIR /usr/src/app`
    Set the working directory inside the container where subsequent commands will be executed.

- `COPY --from=builder /usr/src/app /usr/src/app`
    Copy the built application files from the 'builder' stage into the 'runner' stage.
    This ensures that only the built application and necessary dependencies are included in the final image.

- `EXPOSE 5000`
    Container listens on port 5000 at runtime for Backend 
- `EXPOSE 3000`
    Container listens on port 5000 at runtime for Frontend    
    

- `CMD ["npm", "start"]`
    Define the command to run when the container starts.
    In this case, execute `npm start` which typically starts the Node.js application defined in package.json.

## Docker Compose Network
The Docker Compose file (docker-compose.yml) defines the networking configuration for the project. It includes the allocation of application ports. The relevant sections are as follows:


```
services:
  backend:
    # ...
    ports:
      - "5000:5000"
    networks:
      - yolo-network

  client:
    # ...
    ports:
      - "3000:3000"
    networks:
      - yolo-network
  
  mongodb:
    # ...
    ports:
      - "27017:27017"
    networks:
      - yolo-network

networks:
  yolo-network:
    driver: bridge
```
In this configuration, the backend container is mapped to port 5000 of the host, the client container is mapped to port 3000 of the host, and mongodb container is mapped to port 27017 of the host. All containers are connected to the yolo-network bridge network.

## Docker Compose Volume
The Docker Compose file includes volume definitions for MongoDB data storage.

yaml

```
volumes:
  mongodata:  # Define Docker volume for MongoDB data
    driver: local

```
The mongodata, volume is designated for storing MongoDB data. It ensures that the data remains intact and is not lost even if the container is stopped or deleted.

# Commands

### Building, Tagging, and Pushing Docker Images

Before building the Docker image, we need to navigate to the directory containing the Dockerfile. We use the `cd` command to achieve this.


# Navigate to 'backend' directory
    - cd backend

# Navigate to 'client' directory
    - cd client


# Build the Docker image and tag it

- docker build -t kevinkipkemei/imagename:version .

    e.g. - `sudo docker build -t kevinkipkemei/yolo-backend:v1.0.0 .`


# Build the Docker image, tag it, and push it to the registry

- docker build -t kevinkipkemei/imagename:version . --push

    e.g. - `sudo docker build -t kevinkipkemei/yolo-backend:v1.0.0 . --push`

### Running Containers

Running containers in Docker is done using the `docker run` command. 
However, when using Docker Compose, you can start all services defined in the `docker-compose.yml` file with a single command: `docker-compose up`.


# To Start all services
    `docker-compose up -d`

## start indivual services
 - Client service
    `docker-compose up -d client`

 - Backend service
    `docker-compose up -d backend`

## Links

### Github
1. [Github IP2 E-commerce Micro-service Project Repository](https://github.com/Kevin-Niv/yolo)

### Dockerhub
1. [Dockerhub Images Repository](https://hub.docker.com/repositories/kevinkipkemei)

## Git Workflow

- Fork the repository from the original repository.
- Clone the repo: `https://github.com/Kevin-Niv/yolo`
- Create a .gitignore file to exclude unnecessary files and directories from version control.
Added Dockerfile for the client to the repo:
- `git add client/Dockerfile`
Add Dockerfile for the backend to the repo:
- `git add backend/dockerfile`
Committed the changes:
- `git commit -m "Added Dockerfiles"`
Added docker-compose file to the repo:
- `git add docker-compose.yml`
Committed the changes:
- `git commit -m "Added docker-compose file"`
Pushed the files to github:
- `git push `
Built the client and backend images:
- `docker compose build`
Pushed the built imags to docker registry:
- `docker compose push`
Deployed the containers using docker compose:
- `docker compose up`

## Docker image tag naming standards
Use `docker image ls` to check images have tags as follows.
  Images are tagged using this versioning (`v1.0.0`):
  - `kevinkipkemei/yolo-backend:v1.0.5`
  - `kevinkipkemei/yolo-client:v1.0.0`

#### Backend Image
 Here is the link to the dockerhub for Backend image

- [Backend](https://hub.docker.com/repository/docker/kevinkipkemei/yolo-backend/general)

#### Client Image
 Here is the link to the dockerhub for Client image

- [Client](https://hub.docker.com/repository/docker/kevinkipkemei/yolo-client/general)

## Images / Screenshots
    Dockerhub Tags
        - Backend
 !["Docker tags"](/images/Dockerhub-Backend-Tag.png)

        - Frontend
 !["Docker tags"](/images/Dockerhub-Client-Tag.png)

    Image Sizes
!["Images"](/images/Image-Sizes.png)

    Containers Up/Running
!["Images"](/images/Images-Up-Running.png)

    Client Product Form
!["Images"](/images/Product-Form.png)

    Client Product Form Adding Items
!["Images"](/images/Product-Form-Data.png)

    First Item Added
!["Images"](/images/First-Product-Added.png)

    Second Item Added
!["Images"](/images/Second-Product-Added.png)

    More Items Added
!["Images"](/images/More%20Added%20Products.png)



