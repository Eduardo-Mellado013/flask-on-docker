Flask on Docker

Overview
This repository demonstrates how to containerize a Flask application using Docker. The project leverages PostgreSQL as its database, Gunicorn as a production-grade WSGI server, and Nginx as a reverse proxy. Inspired by TestDriven.io’s guide on Dockerizing Flask with Postgres, Gunicorn, and Nginx, this repo includes separate configurations for development and production environments, making it easy to build and deploy the app in any setting.

Build Instructions

Prerequisites
Docker and Docker Compose must be installed.
Clone this repository:
bash
Copy
git clone https://github.com/your-username/flask-on-docker.git
cd flask-on-docker
Ensure the environment variable files (.env.dev, .env.prod, .env.prod.db) are present in the project root. (These are listed in the .gitignore file.)
Development
Bring up the development services:

bash
Copy
docker compose up
This will start the Flask app (using Flask’s built-in server), the PostgreSQL database, and any other services defined in your docker-compose.yml.

Access the application: Open your browser at http://localhost:5000 (or the port specified in your development config).

Production
Bring down any existing containers (and volumes) to avoid conflicts:

bash
Copy
docker compose -f docker-compose.prod.yml down -v
Build and start the production containers:

bash
Copy
docker compose -f docker-compose.prod.yml up -d --build
In production, Gunicorn serves your Flask application on port 5000 inside the container, and Nginx (running on port 80 inside its container) is mapped to a host port (e.g., 1337).

Verify the deployment: Open your browser at http://localhost:1337 to see your application running behind Nginx.

Database Setup
Before using the application, initialize and seed the database:

Create the database schema:

bash
Copy
docker compose exec web python manage.py create_db
Seed the database:

bash
Copy
docker compose exec web python manage.py seed_db
Verify the data (optional): Connect to the PostgreSQL container:

bash
Copy
docker compose exec db psql --username=hello_flask --dbname=hello_flask_prod
Then run:

sql
Copy
SELECT * FROM users;
This should display the seeded user data.

Additional Commands
View logs for a service (e.g., web):
bash
Copy
docker compose logs -f web
Stop the services:
bash
Copy
docker compose down
With these instructions, anyone should be able to build, deploy, and test the application in both development and production environments.
