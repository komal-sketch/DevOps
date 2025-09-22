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

2. Building the Flask Application Container

Navigate to the project directory and build the Docker image for the Flask app:

docker build -t two-tier-backend .


‑ -t two-tier-backend – Tags the resulting image with the name two-tier-backend.
‑ . – Uses the current directory as the build context.

3. Creating a Private Docker Network

Create a dedicated network for the Flask and MySQL containers so they can communicate privately:

docker network create two-tier


To confirm the network was created, list all networks:

docker network ls

4. Running the Containers
Start the MySQL Database Container

Run the official MySQL image in detached mode and attach it to the two-tier network:

docker run -d --name mysql --network two-tier \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql


‑ -d – Runs the container in detached mode (in the background).
‑ --name mysql – Assigns the container the name mysql.
‑ --network two-tier – Connects the container to the private network.
‑ -e … – Environment variables used to initialise the MySQL database.

Start the Flask Application Container

Run the Flask app image you built earlier and connect it to the same network:

docker run -d -p 5000:5000 --network two-tier \
  -e MYSQL_HOST=mysql -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=root -e MYSQL_DB=devops \
  two-tier-backend


‑ -p 5000:5000 – Maps container port 5000 to host port 5000 so you can access the app at http://localhost:5000.
‑ --network two-tier – Connects the Flask container to the private network.
‑ -e … – Sets environment variables for the Flask app to connect to the database.

Note: the MYSQL_HOST variable is set to mysql, which matches the name of the database
container. Docker’s internal DNS resolves container names to their IP addresses, so the Flask
app can reach the database using this name.

5. Persisting Data with Docker Volumes (Recommended)

By default any data in a container is lost when the container is removed. Use a Docker volume to
store the database files on the host so that data persists across container restarts.

First stop and remove the existing MySQL container:

docker stop mysql
docker rm mysql


Create a named volume and restart MySQL with the volume mounted:

docker volume create mysql-data

docker run -d --name mysql --network two-tier \
  -v mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql


‑ -v mysql-data:/var/lib/mysql – Mounts the volume mysql-data at /var/lib/mysql in the
container, which is where MySQL stores its data.

6. Cleaning Up

When you are done with the project, you can remove all resources by running:

# Stop and remove the containers
docker stop mysql two-tier-backend
docker rm mysql two-tier-backend

# Remove the network
docker network rm two-tier

# Remove the volume (⚠️ deletes all database data)
docker volume rm mysql-data

# Remove the image
docker rmi two-tier-backend


You now have a fully containerised Flask and MySQL application running in separate containers on
a private network. This setup is an example of a simple two‑tier architecture using Docker.

You said:
make one single markdown file. here it is going greyed out in github markdown file. 
ChatGPT said:
Worked for 21 seconds

Here's the single Markdown file, properly formatted for GitHub:

Two-Tier Flask Application with Docker

This guide explains how to build and run a simple two‑tier web application using Docker. The
front end is a Python Flask web server and the back end is a MySQL database. Each runs in its
own container, and the containers communicate over a private Docker network.

1. Project Structure

The repository has the following structure:

.
├── app.py              # The Flask application code
├── Dockerfile          # Instructions to build the Flask app image
├── requirements.txt    # Python dependencies for the Flask app
└── README.md           # Project documentation (this file)

2. Building the Flask Application Container

Navigate to the project directory and build the Docker image for the Flask app:

docker build -t two-tier-backend .


‑ -t two-tier-backend – Tags the resulting image with the name two-tier-backend.
‑ . – Uses the current directory as the build context.

3. Creating a Private Docker Network

Create a dedicated network for the Flask and MySQL containers so they can communicate privately:

docker network create two-tier


To confirm the network was created, list all networks:

docker network ls

4. Running the Containers
Start the MySQL Database Container

Run the official MySQL image in detached mode and attach it to the two-tier network:

docker run -d --name mysql --network two-tier \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql


‑ -d – Runs the container in detached mode (in the background).
‑ --name mysql – Assigns the container the name mysql.
‑ --network two-tier – Connects the container to the private network.
‑ -e … – Environment variables used to initialise the MySQL database.

Start the Flask Application Container

Run the Flask app image you built earlier and connect it to the same network:

docker run -d -p 5000:5000 --network two-tier \
  -e MYSQL_HOST=mysql -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=root -e MYSQL_DB=devops \
  two-tier-backend


‑ -p 5000:5000 – Maps container port 5000 to host port 5000 so you can access the app at http://localhost:5000.
‑ --network two-tier – Connects the Flask container to the private network.
‑ -e … – Sets environment variables for the Flask app to connect to the database.

Note: the MYSQL_HOST variable is set to mysql, which matches the name of the database
container. Docker’s internal DNS resolves container names to their IP addresses, so the Flask
app can reach the database using this name.

5. Persisting Data with Docker Volumes (Recommended)

By default any data in a container is lost when the container is removed. Use a Docker volume to
store the database files on the host so that data persists across container restarts.

First stop and remove the existing MySQL container:

docker stop mysql
docker rm mysql


Create a named volume and restart MySQL with the volume mounted:

docker volume create mysql-data

docker run -d --name mysql --network two-tier \
  -v mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops \
  mysql


‑ -v mysql-data:/var/lib/mysql – Mounts the volume mysql-data at /var/lib/mysql in the
container, which is where MySQL stores its data.

6. Cleaning Up

When you are done with the project, you can remove all resources by running:

# Stop and remove the containers
docker stop mysql two-tier-backend
docker rm mysql two-tier-backend

# Remove the network
docker network rm two-tier

# Remove the volume (⚠️ deletes all database data)
docker volume rm mysql-data

# Remove the image
docker rmi two-tier-backend



