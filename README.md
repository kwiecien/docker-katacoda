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
