
[← Back to Docker Projects](dockerImagesRun.md)


Docker image directly from your local command prompt (or terminal), you use the **`docker run`** command.

The format for port mapping in Docker is always **`HOST:CONTAINER`** (External:Internal).

Here is how your two commands actually map out:

Bash

```
docker run -d -p 8080:8080 --name inventory-service your-dockerhub-username/inventory-service:latest

```

-   **First `8080` (HOST/Outside):** The port on your laptop or EC2 machine that you type into the browser (e.g., `localhost:8080`).
    
-   **Second `8080` (CONTAINER/Inside):** The port Tomcat/Spring Boot is internally listening on inside the container.

```
Ex:
docker run -d -p 8081:8080 --name inventory-service vamshivoore/inventory-service:latest
--> inventory-service connects h2 database no dependecy
docker run -d -p 8082:8080 --name product-service-loadtest vamshivoore/product-service-loadtest:latest
--> product-service-loadtest connects h2 database no dependecy
docker run -d -p 8083:8080 --name spring-order-service vamshivoore/spring-order-service:latest
--> spring-order-service connects mysql database so need to connect first mysql database
docker run -d -p 8084:8080 --name memory-leak-prometheus vamshivoore/memory-leak-prometheus:latest
--> memory-leak-prometheus connects prometheus and Graphana those are not mandatory it will not break
docker run -d -p 8085:8080 --name springboot-crud-k8s vamshivoore/springboot-crud-k8s:latest
--> springboot-crud-k8s connects mysql database so need to connect first mysql database
```

- [Database dependency](databaseDependency.md)

_(Be sure to replace `your-dockerhub-username` with your actual Docker Hub username, e.g., `vamshivoore`)._

### What this command does:

1.  **Checks Locally:** Docker first looks to see if you have `inventory-service:latest` on your machine.
    
2.  **Pulls Automatically:** Since it's on Docker Hub, if Docker can't find it locally, it will automatically download (pull) it for you before starting.
    
3.  **`-d` (Detached Mode):** Runs the container in the background so your command prompt stays free.
    
4.  **`-p 8080:8080` (Port Mapping):** Connects port `8080` on your Windows machine to port `8080` inside the container so you can access your Spring Boot app in your browser at `http://localhost:8080`.
    
5.  **`--name inventory-service`:** Gives your container a clean name so you don't have to refer to it by a random auto-generated ID.
    

### Useful Commands Once It's Running:

-   **View running containers:**
    
    
    ```
    docker ps
    
    ```
-   **If you don't need to pull a new image version and just want to turn that stopped container back on, start it directly:**

```
    docker start inventory-service
    docker start spring-order-service
```
    
-   **View the Spring Boot logs:**
    
    ```
    docker logs -f inventory-service
    docker logs -f product-service-loadtest
    docker logs -f memory-leak-prometheus
    docker logs -f spring-order-service
    docker logs -f springboot-crud-k8s
    ```
    
-   **Stop the container:**
    
    ```
    docker stop inventory-service
    
    ```
    
-   **Force-Remove the Stuck Container **
Since docker stop failed, force Docker to tear down the container and its resources:
```
    docker rm -f inventory-service
    docker rm -f spring-order-service
    docker rm -f springboot-crud-k8s
```    
If docker rm -f hangs or gives an error, restart your local Docker Engine/Desktop to clean up the orphaned process
    ```

