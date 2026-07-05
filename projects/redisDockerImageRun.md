
[← Back to Docker Projects](dockerImagesRun.md)

### Run Redis locally (for prod profile testing)

Docker is the right way — no installation, one command, throw it away when done.

#### Step 1 — Install Docker Desktop

Download from [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop) if you don't have it. Verify:
```
docker --version
```
#### Step 2 — Start Redis container
```
docker run -d \
  --name redis-local \
  -p 6379:6379 \
  redis:7-alpine
  ```
  Verify it's running:
  ```
  docker ps
   should show redis-local  redis:7-alpine  0.0.0.0:6379->6379/tcp
 ```
Verify Redis responds:
```
docker exec -it redis-local redis-cli ping
# should print: PONG
```

#### Step 3 — Start your app pointing to Redis
```
java -jar target/product-service-1.0.0.jar \
  --spring.profiles.active=prod \
  --spring.data.redis.host=localhost \
  --spring.data.redis.port=6379
  ```

#### Step 4 — Watch Redis in real-time during k6 test

Open a second terminal and monitor what's being cached:
```
# Live command monitor — see every GET/SET/DEL as k6 runs
docker exec -it redis-local redis-cli monitor

# Sample output during load test:
# 1234567.123 [0 127.0.0.1:51234] "GET" "products::1"        ← cache lookup
# 1234567.124 [0 127.0.0.1:51234] "SET" "products::1" "..."  ← cache write (miss)
# 1234567.125 [0 127.0.0.1:51234] "GET" "products::1"        ← cache hit (no SET follows)
# 1234567.126 [0 127.0.0.1:51234] "DEL" "products::1"        ← eviction on update
```

Check what keys are cached:
```
docker exec -it redis-local redis-cli keys "*"
# products::1
# products::sku:LP-001
# product-lists::page:0:size:20:cat:null:...
```
Check a cached value:
```
docker exec -it redis-local redis-cli get "products::1"
```
#### Step 5 — Stop Redis when done
```
docker stop redis-local
docker rm redis-local
```
