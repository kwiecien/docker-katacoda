# docker-katacoda
https://www.katacoda.com/courses/docker/

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
