### 1. Install docker and Start the Docker Service

Run these commands to start the engine and ensure it starts automatically every time you reboot the VM:

Bash

```
#Installs Docker using  YUM package manager (CentOS/RHEL).
sudo yum install docker -y

# Start the Docker daemon
sudo systemctl start docker

# Enable Docker to start on boot
sudo systemctl enable docker

```

----------

### 2. Fix the Permissions (Crucial Step)

Notice how you had to type `sudo`? By default, only the "root" user can talk to Docker. To avoid typing `sudo` every time and to fix "Permission Denied" errors, add your user (e.g., `ec2-user` or `ubuntu`) to the docker group:

Bash

```
sudo usermod -aG docker $USER

```

**IMPORTANT:** After running this, you must **log out and log back into your SSH session** for this change to take effect.

----------

### 3. Verify it's Working

Once you log back in, run this to see if the daemon is alive:

Bash

```
docker info

```

If you see a bunch of text about "Containers" and "Server Version" without an error, you are good to go!
### 1. `docker pull` (The Download)

`sudo docker pull vamshivoore/inventory-api:v1`

-   **Action:** It goes to Docker Hub, finds your repository, and downloads the image layers to your VM’s local storage.
    
-   **Result:** The image is now sitting on your hard drive, but **nothing is running**. It's just a static file (like an `.exe` or an `.installer`).
    
-   **Analogy:** You bought a IKEA bookshelf and brought the box home. It’s in your living room, but you can't put books on it yet.
    

----------

### 2. `docker run` (The Execution)

`docker run -d -p 8080:8080 --name inventory-app vamshivoore/inventory-api:v1`

This is a "super command" because it actually does three things at once:

1.  **Check:** It looks to see if you have the image locally. (If you didn't do a `pull` first, it will automatically pull it for you now).
    
2.  **Create:** It creates a writeable container layer on top of that image.
    
3.  **Start:** It executes the Spring Boot application.
    

**The Flags Explained:**

-   **`-d` (Detached):** Runs the container in the background. If you don't use this, the Spring Boot logs will take over your terminal, and if you close the terminal, the app stops.
    
-   **`-p 8080:8080` (Port Mapping):** Maps your EC2's port 8080 to the container's port 8080. Without this, you can't reach your API from a browser.
    
-   **`--name inventory-app`:** Gives your running container a friendly name so you can stop or start it easily later.
    

----------



### Pro-Tip

On your EC2 instance, you usually don't strictly _need_ to run `pull` first. You can just run the `docker run` command, and Docker is smart enough to realize "Hey, I don't have this image," download it automatically, and then start it.

Most developers only use `pull` separately when they want to pre-download a very large image before a scheduled maintenance window to save time.

Since you're running this on an EC2 instance, have you already configured your **Security Group** in the AWS Console to allow traffic on port **8080**?

### Running it on EC2

Once the pull is finished, remember that EC2 has its own "Security Groups" (firewall). When you run your container:

Bash

```
docker run -d -p 8080:8080 --name inventory-app vamshivoore/inventory-api:v1

```

You must go to your **AWS Console -> EC2 -> Security Groups** and add an **Inbound Rule** to allow **Custom TCP** on port **8080** from "Anywhere (0.0.0.0/0)", otherwise you won't be able to see your API in your browser using the EC2 Public IP.
