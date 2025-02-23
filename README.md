# Flask on Docker

## Overview

This repository demonstrates how to containerize a Flask application using Docker, PostgreSQL, Gunicorn, and Nginx—following the guide from [TestDriven.io](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/). It provides separate configurations for development and production environments, allowing you to build, run, and deploy a scalable, production-ready web application.

## Build Instructions

### Prerequisites

- **Docker** and **Docker Compose** must be installed.
- Clone this repository:
  ```bash
  git clone https://github.com/your-username/flask-on-docker.git
  cd flask-on-docker
   ```

## Development

### Start the Development Environment

Use Docker Compose to start the development services:

```bash
docker compose up
```

This command will start the Flask development server, PostgreSQL, and any other services defined in `docker-compose.yml`

### Accesing the Application
Open your firefox browser and navigate to:

`http://localhost:5000`

or any other port of your choosing.

The Flask development server should now be running and accessible.

## Production

### Stop Existing Containers and Remove Volumes (if necessary)

Before starting the production environment, make sure any existing containers and volumes are removed:

```bash
docker compose -f docker-compose.prod.yml down -v
```

## Database Setup

Before using the application, initialize and seed the PostgreSQL database.

## Create the Database Schema
Run the following command to create the necessary database tables:

```bash
docker compose exec web python manage.py create_db
```
This command executes the `create_db` command defined in your Flask application to drop any existing tables and create new ones.

## Seed the Database 
Populate the database with initial data (e.g., default users) by running:

```bash
docker compose exec web python manage.py seed_db
```
