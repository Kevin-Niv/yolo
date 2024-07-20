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
