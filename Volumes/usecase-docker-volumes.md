# 📦 Docker Volumes – Complete Guide

Docker volumes provide persistent data storage for containers. When a container stops or is removed, its internal filesystem is deleted—but volumes allow important data to survive.

---

## 🚀 What Are Docker Volumes?

Docker volumes are storage locations **outside the container filesystem** managed by Docker. They ensure that data is **persistent** and not deleted when containers restart.

---

## 🧠 Why Are Volumes Needed?

Containers are ephemeral. Any data stored inside a container is lost when:

* The container stops
* The container is recreated
* The container is removed

Volumes solve this by storing data on the **host machine**.

---

## 📌 Use Cases of Docker Volumes

### ✔️ 1. Databases

Ensures DB files persist:

```
docker run -v mydbdata:/var/lib/mysql mysql
```

### ✔️ 2. Logs

Store logs outside containers.

### ✔️ 3. Configuration Files

Keep configs outside the container image.

### ✔️ 4. Development

Live code changes without rebuilding:

```
docker run -v $(pwd):/app node
```

### ✔️ 5. Sharing Data Between Containers

```
docker run -v shared:/data container1
```

```
docker run -v shared:/data container2
```

---

## 🔍 Types of Docker Volumes

### 1️⃣ Named Volumes (Managed by Docker)

Created automatically or manually:

```
docker volume create mydata
```

Used like:

```
docker run -v mydata:/data ubuntu
```

### 2️⃣ Bind Mounts (Host directory → Container directory)

```
docker run -v /host/path:/container/path ubuntu
```


