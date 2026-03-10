# Exercise 005 - Multi-container setup (Docker Compose)

### Objective
Orchestrate a full-stack environment. Use `docker-compose.yml` to launch a Node.js API, a PostgreSQL database, and a Redis cache simultaneously with a single command, ensuring they can communicate with each other over a virtual network.

### Core Concepts to Master
- **Docker Compose:** A tool for defining and running multi-container applications using a YAML configuration file.
- **Service Dependency:** Using `depends_on` to ensure the database starts before the API attempts to connect to it.
- **Environment Variables:** Securely passing database credentials and API keys into containers via the compose file.
- **Docker Networking:** Understanding how containers talk to each other using their service names (e.g., `db:5432` instead of `localhost:5432`).

### Research Topics
- "Docker Compose for Node.js and Postgres"
- "Difference between docker-compose up and build"
- "Managing Docker volumes for database persistence"

---

### The Practical Challenge

**Part 1: Defining the Compose File**
1. In a new folder, create `docker-compose.yml`.
2. Define two services: `app` (your Node.js image) and `db` (the official `postgres` image).
   ```yaml
   services:
     app:
       build: .
       ports:
         - "3000:3000"
       depends_on:
         - db
     db:
       image: postgres:15
       environment:
         POSTGRES_PASSWORD: mysecretpassword
   ```

**Part 2: Orchestration**
1. Run the entire stack: `docker-compose up`.
2. Observe the logs. You will see both the Postgres startup sequence and your Node.js app logs interlaced in the same terminal window.
3. Verify that you can reach the app at `http://localhost:3000`.

**Part 3: Inter-Service Communication**
1. Inside your Node.js app code, attempt to connect to the database.
2. IMPORTANT: Inside the Docker network, the database is NOT at `localhost`. It is at the hostname `db` (matching the service name in your YAML).
3. Update your connection string: `postgres://postgres:mysecretpassword@db:5432/postgres`.
4. Rebuild and restart: `docker-compose up --build`.

**Part 4: Data Persistence with Volumes**
1. By default, when you stop and remove containers (`docker-compose down`), your database data is wiped.
2. Add a `volumes` block to your `db` service:
   ```yaml
   volumes:
     - db-data:/var/lib/postgresql/data
   
   volumes:
     db-data:
   ```
3. Restart the stack, add a record to your database, run `docker-compose down`, and then `docker-compose up` again.
4. Verify that the database record is still there. You have successfully decoupled the "Data" from the "Container."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Ports vs Internal Ports. In `3000:3000`, the first 3000 is what YOU see on your machine. The second 3000 is the port the app is listening on inside the container. 
- **Gotcha 2:** YAML Indentation. YAML is extremely sensitive to spaces. If your `build` is not indented exactly under your service name, the file will be invalid and Docker Compose will throw a syntax error.

### Reflection Question
Why is Docker Compose better for local development than manually starting five different containers via `docker run`?