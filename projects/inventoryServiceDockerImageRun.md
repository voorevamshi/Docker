
[← Back to Docker Projects](dockerImagesRun.md)


Docker image directly from your local command prompt (or terminal), you use the **`docker run`** command.

Here is the exact command you need to run:

DOS

```
docker run -d -p 8080:8080 --name inventory-service your-dockerhub-username/inventory-service:latest

```

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
    
-   **View the Spring Boot logs:**
    
    ```
    docker logs -f inventory-service
    
    ```
    
-   **Stop the container:**
    
    ```
    docker stop inventory-service
    
    ```
    
-   **Start it again after stopping:**
    
    ```
    docker start inventory-service
    ```
