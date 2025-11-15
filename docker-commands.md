

# 🐳 Docker & Linux Commands 

A quick reference for commonly used **Docker** and **Linux** commands.

---

## 🔹 Container & Image Commands
| Command | Description |
|----------|--------------|
| `sudo docker container ls` | Lists **running containers**. |
| `sudo docker container ls -a` | Lists **all containers** (running + stopped). |
| `sudo docker ps` | Lists **active containers** (same as above). |
| `sudo docker images` | Shows all **downloaded Docker images**. |
| `docker images` | Lists available images (no `sudo` version). |
| `sudo docker pull nginx` | Downloads the **nginx image** from Docker Hub. |
| `sudo docker run --name=webapp -d nginx` | Runs an **nginx container** in background. |
| `sudo docker run --name=blog -d -p 7575:80 --link mydb wordpress` | Runs a **WordPress container** linked to `mydb`, exposed on port 7575. |
| `docker run --name=C1 -d busybox` | Starts a **BusyBox** container in detached mode. |
| `sudo docker run --name=ubuntu-container -d -it ubuntu` | Runs an Ubuntu container in interactive mode in the background with the name ubuntu-container. |
| `docker run --name=mydb -d -e MYSQL_ROOT_PASSWORD=vamshi mysql` | Runs a **MySQL** container with root password. |
| `sudo docker run -P -d nginx` | Runs nginx with **random port mapping**. |
| `sudo docker exec -it 10722a792356 /bin/sh` | Opens an **interactive shell** inside a running container. |
| `sudo docker container start 0a0dfab178d5` | Starts a **stopped container**. |
| `sudo docker start 66ee6fbbf475` | Starts another stopped container. |
| `sudo docker logs blog` | Displays **logs** of the `blog` container. |

---

## ⚙️ Docker Service & System Management
| Command | Description |
|----------|--------------|
| `sudo systemctl start docker` | **Starts** the Docker service. |
| `sudo systemctl status docker` | **Checks** Docker service status (active/inactive). |
| `sudo yum install docker -y` | Installs Docker using **YUM package manager** (CentOS/RHEL). |
| `systemctl status docker` | Checks service status (same as above). |
| `docker -version` | Displays the **Docker version**. |

---

## 🌐 Network & Port Checking
| Command | Description |
|----------|--------------|
| `sudo netstat -tuln or grep 7575` | Checks if **port 7575** is listening (using netstat). |
| `sudo ss -tuln or grep 7575` | Checks if **port 7575** is listening (using ss). |
| `curl -I http://13.60.62.67:7575` | Sends an **HTTP HEAD request** to verify server response. |
| `curl -s http://169.254.169.254/latest/meta-data/security-groups` | Fetches **AWS EC2 security group info**. |
| `curl ifconfig.me` | Displays your **public IP address**. |
| `ping http://13.60.62.67:7575` | Tests **network connectivity** (use IP instead of URL). |

---

## 🧩 Database & Miscellaneous
| Command | Description |
|----------|--------------|
| `SHOW DATABASES;` | MySQL command to list databases. |
| `history` | Displays your **command history**. |
| `whoami` | Shows the **current logged-in username**. |


---

📘 **Tip:**  
Use `history | grep docker` to quickly find all previously used Docker commands.

