# Two-Tier Flask Application with Docker

![Docker](https://img.shields.io/badge/Docker-20.10+-blue?logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.9+-yellow?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-green?logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.x-orange?logo=mysql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

This project demonstrates how to build and deploy a **two-tier web application** using Docker.  
The application consists of:

- **Flask Web Server (Frontend):** Handles user requests and serves the web interface.  
- **MySQL Database (Backend):** Stores and manages application data.  

Both run in separate Docker containers, communicating securely within a private Docker network.

---

## Architecture Overview

The application is structured into two tiers:

- **Web Tier (Flask App):** A Python Flask application serving the web interface.  
- **Data Tier (MySQL):** A MySQL database storing all data.  

These two tiers communicate over a **private Docker network**, preventing the database from being directly exposed to the host machine or the public internet.

---

## Getting Started

### Prerequisites
- [Docker](https://docs.docker.com/get-docker/) installed and running on your system.

---

## 1. Project Structure

.
├── app.py # The Flask application code
├── Dockerfile # Instructions to build the Flask app image
├── requirements.txt # Python dependencies for the Flask app
└── README.md # Project documentation


---

## 2. Building the Flask Application Container

Navigate to the project directory and build the Docker image:

```bash
docker build -t two-tier-backend .

•	-t two-tier-backend → Tags the image as two-tier-backend.
•	. → Uses the current directory as the build context.

3. Creating a Private Docker Network

Create a dedicated network for the Flask and MySQL containers:

docker network create two-tier

Verify:

docker network ls

4. Running the Containers
Start the MySQL Database Container

docker run -d --name mysql --network two-tier \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql

•	-d → Runs container in detached mode.

•	--name mysql → Assigns container name mysql.

•	--network two-tier → Connects it to the private network.

•	-e → Environment variables to initialize MySQL.

Start the Flask Application Container

docker run -d -p 5000:5000 --network two-tier \
  -e MYSQL_HOST=mysql -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=root -e MYSQL_DB=devops \
  two-tier-backend


•	-p 5000:5000 → Maps container port 5000 to host port 5000 (accessible in browser at http://localhost:5000).
•	--network two-tier → Connects Flask app to the same network.
•	-e → Sets environment variables for DB connection.
Note: MYSQL_HOST=mysql matches the container name. Docker’s DNS resolves it automatically.

5. Persisting Data with Docker Volumes (Recommended)

By default, database data is lost when the container is removed. Use a Docker volume for persistence.

Stop and remove the existing MySQL container:

docker stop mysql
docker rm mysql

Create a named volume and restart MySQL with persistence:

docker volume create mysql-data

docker run -d --name mysql --network two-tier \
  -v mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql


•	-v mysql-data:/var/lib/mysql → Mounts the volume to persist MySQL data.

6. Cleaning Up

To stop and remove all resources created by this project:

# Stop and remove containers
docker stop mysql two-tier-backend
docker rm mysql two-tier-backend

# Remove the network
docker network rm two-tier

# Remove the volume (⚠️ deletes all database data)
docker volume rm mysql-data

# Remove the image
docker rmi two-tier-backend



