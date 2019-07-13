# docker-katacoda
https://www.katacoda.com/courses/docker/

* [Deploying Your First Docker Container](#deploying-your-first-docker-container)
* [Deploy Static HTML Website as Container](#deploy-static-html-website-as-container)
* [Building Container Images](#building-container-images)
* [Dockerizing Node.js applications](#dockerizing-nodejs-applications)
* [Optimising Dockerfile with OnBuild](#optimising-dockerfile-with-onbuild)
* [Ignoring Files](#ignoring-files)
* [Data Containers](#data-containers)
  
<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## Deploying Your First Docker Container
#### Step 1 - Running A Container
```bash
docker search redis
docker run -d redis
```

#### Step 2 - Finding Running Containers
```bash
docker ps
docker inspect agitated_mendeleev
docker logs agitated_mendeleev
```

#### Step 3 - Accessing Redis
```bash
docker run -d --name redisHostPort -p 6379:6379 redis:latest
```

#### Step 4 - Accessing Redis
```bash
docker run -d --name redisDynamic -p 6379 redis:latest
docker port redisDynamic 6379
docker ps
```

#### Step 5 - Persisting Data
```bash
docker run -d --name redisMapped -v /opt/docker/data/redis:/data redis
docker run -d --name redisMappedPwd -v "$PWD/data":/data redis
```

#### Step 6 - Running A Container In The Foreground
```bash
docker run ubuntu ps
docker run -it ubuntu bash
```

## Deploy Static HTML Website as Container
#### Step 1 - Create Dockerfile
```
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

#### Step 2 - Build Docker Image
```
docker build -t webserver-image:v1 .
docker images
```

#### Step 3 - Run
```
docker run -d -p 80:80 webserver-image:v1
curl docker
```

## Building Container Images
#### Step 1 - Base Images
```
FROM nginx:1.11-alpine
```

#### Step 2 - Running Commands
```
COPY index.html /usr/share/nginx/html/index.html
```

#### Step 3 - Exposing Ports
```
EXPOSE 80
```

#### Step 4 - Default Commands
```
CMD ["nginx", "-g", "daemon off;"]
```

#### Step 5 - Building Containers
```
docker build -t my-nginx-image:latest .
docker images
```

#### Step 6 - Launching New Image
```
docker run -d -p 80:80 my-nginx-image:latest
curl -i http://docker
docker ps
```

## Dockerizing Node.js applications
#### Step 1 - Base Image
```
FROM node:10-alpine
RUN mkdir -p /src/app
WORKDIR /src/app
```

#### Step 2 - NPM Install
```
COPY package.json /src/app/package.json
RUN npm install
```

#### Step 3 - Configuring Application
```
COPY . /src/app
EXPOSE 3000
CMD ["npm", "start"]
```

#### Step 4 - Building & Launching Container
```
docker build -t my-nodejs-app .
docker run -d --name my-running-app -p 3000:3000 my-nodejs-app
curl http://docker:3000
```

#### Step 5 - Environment Variables
```
docker run -d --name my-production-running-app -e NODE_ENV=production -p 3000:3000 my-nodejs-app
```

## Optimising Dockerfile with OnBuild
#### Step 1 - OnBuild
```
FROM node:7
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
ONBUILD COPY package.json /usr/src/app/
ONBUILD RUN npm install
ONBUILD COPY . /usr/src/app
CMD [ "npm", "start" ]
```

#### Step 2 - Application Dockerfile
```
FROM node:7-onbuild
EXPOSE 3000
```

#### Step 3 - Building & Launching Container
```
docker build -t my-nodejs-app .

docker run -d --name my-running-app -p 3000:3000 my-nodejs-app

curl http://docker:3000
```

## Ignoring Files
#### Step 1 - Docker Ignore
```
cat Dockerfile
docker build -t password .
docker run password ls /app

echo passwords.txt >> .dockerignore

docker build -t nopassword .
docker run nopassword ls /app
```

#### Step 2 - Docker Build Context
```
docker build -t large-file-context .
```

#### Step 3 - Optimised Build
```
echo big-temp-file.img >> .dockerignore
docker build -t no-large-file-context .
```

## Data Containers
#### Step 1 - Create Container
```
docker create -v /config --name dataContainer busybox
```

#### Step 2 - Copy Files
```
docker cp config.conf dataContainer:/config/
```

#### Step 3 - Mount Volumes From
```
docker run --volumes-from dataContainer ubuntu ls /config
```

#### Step 4 - Export / Import Containers
```
docker export dataContainer > dataContainer.tar
ls
docker import dataContainer.tar
```

## Communicating Between Containers
#### Step 1 - Start Redis
```
docker run -d --name redis-server redis
```

#### Step 2 - Create Link
```
docker run --link redis-server:redis alpine env
docker run --link redis-server:redis alpine cat /etc/hosts
docker run --link redis-server:redis alpine ping -c 1 redis
```

#### Step 3 - Connect To App
```
docker run -d -p 3000:3000 --link redis-server:redis katacoda/redis-node-docker-example
curl docker:3000
```

#### Step 4 - Connect to Redis CLI
```
docker run -it --link redis-server:redis redis redis-cli -h redis
KEYS *
QUIT
```

##
####
```
```
