## Author : Sanskriti Bahl
# Docker_045050

<img width="1440" alt="Screenshot 2024-12-08 at 00 00 19" src="https://github.com/user-attachments/assets/ff754a63-0696-4b36-8d38-b699ed685af0">


# Deploying WordPress using Docker Desktop

## Objective  
Deploy WordPress using **MariaDB** as the database backend with Docker Desktop.

---

## Prerequisites  
1. **Docker Desktop** must be installed and running on your MacBook.  
2. Verify Docker is working by running the command:  
   ```bash
   docker --version
   ```

---

## Steps to Deploy WordPress  

### 1. Pull the Required Images  
Run the following commands to pull the necessary Docker images:  
```bash
docker pull wordpress
docker pull mariadb
```

### 2. Create a Docker Network  
Create a Docker network to enable communication between the WordPress and MariaDB containers:  
```bash
docker network create wordpress-network
```

### 3. Run the MariaDB Container  
Start a MariaDB container with the required environment variables:  
```bash
docker run -d \
--name wordpress-mariadb \
--network wordpress-network \
-e MYSQL_ROOT_PASSWORD=rootpassword \
-e MYSQL_DATABASE=wordpress \
-e MYSQL_USER=wordpressuser \
-e MYSQL_PASSWORD=wordpresspass \
mariadb
```

### 4. Run the WordPress Container  
Run a WordPress container, expose it on port **8080**, and connect it to the same Docker network:  
```bash
docker run -d \
--name wordpress-container \
--network wordpress-network \
-p 8080:80 \
-e WORDPRESS_DB_HOST=wordpress-mariadb \
-e WORDPRESS_DB_USER=wordpressuser \
-e WORDPRESS_DB_PASSWORD=wordpresspass \
-e WORDPRESS_DB_NAME=wordpress \
wordpress
```

### 5. Access WordPress  
Open a web browser and navigate to:  
   ```
   http://localhost:8080
   ```

### 6. Verify Containers are Running  
Ensure the containers are running with the following command:  
```bash
docker ps
```



