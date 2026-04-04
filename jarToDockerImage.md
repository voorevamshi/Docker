
## 1. Updated Dockerfile

Change your `COPY` line to match your actual filename:

Dockerfile

```
FROM eclipse-temurin:17-jdk-jammy  
COPY target/Inventory-0.0.1-SNAPSHOT.jar app.jar  
ENTRYPOINT ["java","-jar","/app.jar"]

```

----------

## 2. Updated Build and Push Commands

I recommend using a simpler "tag" name for the image itself (like `inventory-api`) even if the jar file name is long. This makes typing commands much easier.

### Step A: Build the Image

Run this in your terminal at the project root:

Bash

```
docker build -t your-dockerhub-username/inventory-api:v1 .

```

### Step B: Push to Docker Hub

Bash

```
docker push your-dockerhub-username/inventory-api:v1

```

----------

## Important Checklist

Before you run the build command, double-check these two things:

1.  **The Extension:** Ensure the file in your `target` folder is actually named `Inventory-0.0.1-SNAPSHOT.jar` (don't forget the `.jar` at the end).
    
2.  **The Path:** If you are running the docker command from the root of your project, the `target/` folder must be right there. If you use Gradle, you might need to change `target/` to `build/libs/` in the Dockerfile.
    

### Pro-Tip for Spring Boot

If you want to avoid changing your Dockerfile every time the version number changes (e.g., when you move to `0.0.2`), you can use a **wildcard** in your Dockerfile like this:

`COPY target/Inventory-*.jar app.jar`

This way, as long as the file starts with "Inventory-", Docker will find it and rename it to `app.jar` inside the container automatically!
