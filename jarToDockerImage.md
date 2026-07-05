
## 1. Updated Dockerfile

Change your `COPY` line to match your actual filename:

Dockerfile

```
FROM eclipse-temurin:21-jdk-jammy  
COPY target/inventory-service-0.0.1-SNAPSHOT.jar inventory-app.jar  
ENTRYPOINT ["java","-jar","/inventory-app.jar"]


```
-   **`eclipse-temurin:17`**: This specifies the version of the Eclipse Temurin JDK base image. The `:17` tag means Java 17.
-   **`jdk`**: This ensures the full Java Development Kit is installed, rather than just the JRE (Java Runtime Environment).
-   **`jammy`**: This indicates the base operating system is Ubuntu 22.04 LTS (codenamed "Jammy Jellyfish").

Things to watch out for:

While your **Docker container** runs Java 17, you must ensure that your local development environment matches.

If your local Maven/Gradle setup builds the `inventory-service-0.0.1.jar` using **Java 21**, but this Dockerfile attempts to run it using **Java 17**, the application will crash on startup with a `java.lang.UnsupportedClassVersionError`.

----------

## 2. Updated Build and Push Commands

I recommend using a simpler "tag" name for the image itself (like `inventory-api`) even if the jar file name is long. This makes typing commands much easier.

### Step A: Build the Image

Run this in your terminal at the project root:



```
docker build -t your-dockerhub-username/inventory-api:v1 .

```
After creating docker image check docker image in images tab of docker desktop.
```
docker run -p 8080:8080 your-dockerhub-username/inventory-api:v1
```
In Containers tab. You will see your app running. You can click the "logs" to see your Spring Boot startup sequence.
**When you run docker run, Docker follows a specific logic:**
1.  Check Locally: It looks for the image name in your Docker Desktop list.
2.  Check Cloud: If it's not local, it tries to download it from Docker Hub.
3.  Fail: If it's not in either place, it gives you the failed to resolve error.
To verify images in docker use this command **docker images**

### Step B: Push to Docker Hub
In your terminal, type:
```
docker login
```
Now, send it to the cloud:
```
docker push your-dockerhub-username/inventory-api:v1
```

----------

## Important Checklist

Before you run the build command, double-check these two things:

1.  **The Extension:** Ensure the file in your `target` folder is actually named `inventory-service-0.0.1-SNAPSHOT.jar` (don't forget the `.jar` at the end).
    
2.  **The Path:** If you are running the docker command from the root of your project, the `target/` folder must be right there. If you use Gradle, you might need to change `target/` to `build/libs/` in the Dockerfile.
    

### Pro-Tip for Spring Boot

If you want to avoid changing your Dockerfile every time the version number changes (e.g., when you move to `0.0.2`), you can use a **wildcard** in your Dockerfile like this:

`COPY target/inventory-*.jar inventory-api.jar`

This way, as long as the file starts with "Inventory-", Docker will find it and rename it to `inventory-api.jar` inside the container automatically!
