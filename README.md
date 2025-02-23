# Flask on Docker

## Overview
This repository demonstrates how to containerize a Flask application using Docker, PostgreSQL, Gunicorn, and Nginx. Inspired by the guide from [TestDriven.io](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/), this project includes separate configurations for development and production environments. In development, the Flask built-in server is used, while in production, Gunicorn and Nginx provide a robust and scalable setup.

## Build Instructions

### Prerequisites

- Ensure [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/install/) are installed.
- Clone this repository:
  ```bash
  git clone https://github.com/Eduardo-Mellado013/flask-on-docker
  cd flask-on-docker
  ```

## Development 

### Start the Development Environment 
Use Docker Compose to start the development services:

```bash
docker compose up
```

This command starts the Flask development server, PostgreSQL, and any other services defined in `docker-compose.yml`

### Access the Application 
Open Firefox and navigate to `http://localhost:5028` or any other port of your choosing. This is a reminder to enable port forwarding if needed. The Flask development server should now be running and accessible. There should be a `hello world` sanity check.

## Production 
For production, the configuration uses Gunicorn as a WSGI server and Nginx as a reverse proxy to efficiently serve your application.

### Stop Existing Containers and Remove Volumes
Before starting the production environment, remove any existing containers and volumes:

```
docker compose -f docker-compose.prod.yml down -v
```

### Build and Start the Production Containers
Build and run the production services (which use Gunicorn and Nginx) with the following command:

```
docker compose -f docker-compose.prod.yml up -d --build
```
Gunicorn serves your Flask application on port 5000 inside the container, and Nginx acts as a reverse proxy, mapping the external port (e.g., 1342) to the internal port.

### Access the Production Application
Open your Firefox browser and navigate to:

```bash
http://localhost:1342
```
Or a port of your choosing. You should see your production application running behind Nginx.There should be a `hello world` sanity check.

## Database Setup 
Before using the application, initialize and seed the PostgreSQL database.

### Create Database Schema
Run the following command to create the necessary database tables

```bash
docker compose exec web python manage.py create_db
```

### Seed the Database 
Populate the database with initial data:

```bash
docker compose exec web python manage.py seed_db
```

## Viewing Media

Now using `CMC.jpg` image located in this repository. Access the following port or a port of your choosing on your Firefox browser
.
```bash
http://localhost:1342/upload
```

Select the `browse` option on this link and select the `CMC.jpg` image. Now the image should be viewable at 

```bash
http://localhost:1342/media/CMC.jpg
```
View the `Image_Upload.gif` image below for a tutorial on the image uploading and viewing process: 

![Image Upload](Image_Upload.gif)
