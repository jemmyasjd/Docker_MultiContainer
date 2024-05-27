# Dockerized Multi-Container Application ⚒️

This repository demonstrates how to set up a Dockerized environment for a multi-container application consisting of a frontend (React), backend (Node.js), and a MySQL database. Follow the steps below to clone the repository, build Docker images, and run the application.

## Prerequisites
Before you begin, ensure you have the following installed:
- Docker Desktop
- Basic understanding of Docker concepts
- Knowledge of frontend and backend technologies

**Note** : _For more information you can visit my docker repo_ [click here](https://github.com/jemmyasjd/Docker)

## Installation Steps

### Step 1: Clone the Repository
Clone the repository to your local machine:
```sh
git clone https://github.com/jemmyasjd/Docker_MultiContainer.git
cd Docker_MultiContainer
```

### Step 2: Docker Setup

#### Installing Docker
If Docker is not already installed, download and install Docker Desktop from the [Docker website](https://docs.docker.com/desktop/install/windows-install/).

Verify the installation by running:
```sh
docker --version
```

### Step 3: Docker Basics

#### Docker Concepts
- **Image**: A self-sufficient software bundle that contains everything needed to run a piece of software, including the code, runtime, libraries, and dependencies.
- **Container**: A portable package that includes the application and its dependencies. Containers run in isolation from each other.
- **Dockerfile**: A text file containing commands to assemble a Docker image.


### Step 4: Setting Up MySQL Container

Create a Docker network:
```sh
docker network create Docker_Assignment
```

Run the MySQL container:
```sh
docker run -d --name jd_mysql_db --network Docker_Assignment -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:8.0
```

Access the MySQL container to create a database and table:
```sh
docker exec -it jd_mysql_db mysql -u root -p
# Enter the password: 123456
```

Run the following SQL queries to set up the database:
```sql
CREATE DATABASE studentsdb;
USE studentsdb;
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL
);
```

### Step 6: Building Docker Images

Ensure you are in the root directory of the project and follow the file structure as shown:

```
Docker_MultiContainer/
├── backend/
│   ├── Dockerfile
│   └── ...
├── frontend/
│   ├── Dockerfile
│   └── ...
```

Build the frontend image:
```sh
cd frontend
docker build -t frontend_image_21bcp319 .
```

Build the backend image:
```sh
cd ../backend
docker build -t backend_image_21bcp319 .
```

### Step 7: Running the Containers

Run the frontend container:
```sh
docker run -d --name jd_frontend --network Docker_Assignment -p 3000:3000 frontend_image_21bcp319
```

Run the backend container:
```sh
docker run -d --name jd_backend --network Docker_Assignment -p 5000:5000 backend_image_21bcp319
```

### Step 8: Verify the Setup

Open the following URLs in your browser to verify the setup:
- Frontend React app: [http://localhost:3000](http://localhost:3000)
- Backend API: [http://localhost:5000/students](http://localhost:5000/students)

To check if the application is running correctly, query the database in the MySQL container:
```sh
docker exec -it jd_mysql_db mysql -u root -p
# Enter the password: 123456
USE studentsdb;
SELECT * FROM students;
```

## Conclusion
By following these steps, you have successfully set up a Dockerized environment for a multi-container application. Docker ensures a consistent and reliable deployment process, making your application run smoothly across different environments.

For any issues or further assistance, feel free to open an issue on the GitHub repository.

---

Happy Dockerizing!✨
