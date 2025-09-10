# Cloud Computing for Data Analysis - Assignment 1

Course: ITCS 6190/8190, Fall 2025  
Instructor: Marco Vieira  
Student: [Your Name]  


## What This Project Does

Build and run a two-container stack using Docker and Docker Compose.

One container runs PostgreSQL, the other runs a Python app.

Python app connects to the database, queries data, computes basic statistics, and saves/prints results.

Learn multi-container concepts: service networking, environment variables, and reproducible workflows

- We have a **PostgreSQL database** with a table called `trips`.  
- A **Python app** connects to this database, runs queries, and saves a summary as JSON.  
- **Docker Compose** runs both containers together easily.

## Problems I Faced

1. **Dockerfile errors** – Initially empty Dockerfiles caused build errors. Fixed by writing proper content.  
2. **Compose file not recognized** – The file was named `compose.yml` instead of `docker-compose.yml`. Renaming fixed it.  
3. **Database table missing** – `trips` table wasn’t found because the container ran before `init.sql` was added. Fixed by restarting the container.  
4. **Build errors** – Errors like `file already closed` were fixed by restarting Docker and cleaning old images/containers.

## How to Run

1. Go to project folder:

powershell
cd C:\Users\ram_w\OneDrive\Documents\Assignment1
Copy code

Build and start containers:
docker compose up --build

The app will run and create a JSON summary in:
pgsql
Copy code
./out/summary.json


