## **12. Docker**

### **Beginner:**

1. **What is Docker, and how does it differ from a virtual machine?**
   - Docker is a platform for developing, shipping, and running applications in containers. Unlike virtual machines (VMs), which virtualize hardware, Docker containers share the host system's kernel, making them more lightweight and efficient.

2. **What is a Docker container, and how does it work?**
   - A Docker container is a lightweight, standalone, executable package that includes everything needed to run a piece of software, including code, runtime, libraries, and system tools.

3. **What is a Docker image, and how do you build one?**
   - A Docker image is a read-only template used to create containers. You can build a Docker image by writing a `Dockerfile` and using the `docker build` command.

4. **How do you run a Docker container from an image?**
   - You can run a Docker container using the `docker run` command, followed by the image name. For example: `docker run -d myimage`.

5. **What is the purpose of a `Dockerfile`, and what are its basic components?**
   - A `Dockerfile` is a text file containing a series of instructions on how to build a Docker image. Basic components include:
     - `FROM`: Specifies the base image.
     - `RUN`: Executes commands in the container.
     - `COPY`/`ADD`: Copies files into the container.
     - `CMD`: Defines the default command to run when the container starts.

6. **How do you expose ports when running a Docker container?**
   - You can expose ports with the `-p` flag in the `docker run` command, like this: `docker run -p 8080:80 myimage`.

7. **How do you view the logs of a running Docker container?**
   - You can view the logs using the `docker logs <container_id>` command.

8. **What is the difference between `docker run` and `docker exec`?**
   - `docker run` starts a new container from an image, while `docker exec` runs a command in a running container.

9. **What is the role of Docker Compose, and how does it help in multi-container applications?**
   - Docker Compose is a tool for defining and running multi-container Docker applications. With a `docker-compose.yml` file, you can define services, networks, and volumes, and then manage the entire application with a single command.

10. **How do you manage container networking in Docker?**
    - Docker provides networking options such as bridge, host, and overlay networks to manage communication between containers. You can create custom networks with `docker network create`.

### **Mid-Level:**

1. **What are Docker volumes, and how do you use them to persist data?**
   - Docker volumes are persistent storage that can be shared between containers or between a container and the host system. You can use them with the `-v` flag in the `docker run` command to mount a volume.

2. **How do you create and manage Docker networks?**
   - You can create custom Docker networks with the `docker network create` command. Containers on the same network can communicate with each other by their container name.

3. **What is Docker Swarm, and how does it differ from Kubernetes?**
   - Docker Swarm is Docker’s native clustering and orchestration tool. It allows you to manage a cluster of Docker nodes as a single virtual system. Kubernetes is a more feature-rich and widely adopted orchestration platform.

4. **How do you optimize the size of a Docker image?**
   - To optimize Docker images, you can:
     - Use smaller base images like `alpine`.
     - Remove unnecessary files with the `RUN` command.
     - Combine commands in a single `RUN` statement.

5. **How do you handle environment variables in Docker?**
   - You can pass environment variables to containers using the `-e` flag in `docker run` or define them in the `Dockerfile` with `ENV`.

6. **How do you handle multi-stage builds in a `Dockerfile`?**
   - Multi-stage builds allow you to create smaller images by using one image to build your app and a second, smaller image to run it. You can specify multiple `FROM` instructions in the `Dockerfile`.

7. **How do you implement logging and monitoring in Docker containers?**
   - You can use centralized logging systems like the ELK stack (Elasticsearch, Logstash, Kibana) or external tools like Prometheus and Grafana for monitoring Docker containers.

8. **What is the purpose of Docker health checks, and how do you configure them?**
   - Health checks allow Docker to periodically check if a container is running as expected. You can configure a health check in the `Dockerfile` using the `HEALTHCHECK` instruction.

9. **How do you deploy a multi-container application using Docker Compose?**
   - You define the services (containers) in a `docker-compose.yml` file and use `docker-compose up` to launch the entire application.

10. **How do you manage Docker container lifecycle (start, stop, restart, remove)?**
    - You can manage containers using:
      - `docker start <container_id>`
      - `docker stop <container_id>`
      - `docker restart <container_id>`
      - `docker rm <container_id>`

### **Senior-Level:**

1. **How do you design a highly available and scalable system using Docker containers?**
   - Design a system with multiple Docker containers spread across different hosts. Use orchestration tools like Docker Swarm or Kubernetes for load balancing, failover, and scaling.

2. **How would you use Docker in a CI/CD pipeline?**
   - Docker can be used to build and test applications in isolated environments. You can create Docker images in your CI pipeline and deploy them to production using Docker Compose or Kubernetes.

3. **What are the security best practices for running Docker containers in production?**
   - Security best practices include:
     - Use trusted base images.
     - Run containers with the least privileges.
     - Use Docker secrets for sensitive information.
     - Keep Docker and container images up to date.
     - Monitor containers for vulnerabilities.

4. **How do you monitor and manage Docker containers in a production environment?**
   - You can use monitoring tools like Prometheus and Grafana, as well as centralized logging systems like ELK or Fluentd. Docker’s built-in tools (`docker stats`, `docker logs`) can also be useful for container management.

5. **How do you implement rolling updates or canary deployments using Docker Swarm or Kubernetes?**
   - In Docker Swarm, use `docker service update` to perform rolling updates. Kubernetes offers more advanced deployment strategies like rolling updates and canary releases through `kubectl` commands and deployment configurations.

6. **How do you handle container orchestration using Kubernetes versus Docker Swarm?**
   - Kubernetes is more feature-rich, offering extensive support for scaling, service discovery, and automation. Docker Swarm is simpler but may lack some advanced features. Kubernetes is better suited for large-scale production environments.

7. **How would you set up a multi-environment (e.g., development, staging, production) Docker workflow?**
   - You can use different `docker-compose.yml` files for each environment or set environment-specific variables. Docker also supports multi-stage builds to create different images for different environments.

8. **What is the role of Docker in microservices architecture?**
   - Docker provides a lightweight and portable environment for microservices, allowing each service to run in its own container, ensuring isolation and scalability.

9. **How do you manage Docker container logs and centralized logging solutions (e.g., ELK stack)?**
   - You can configure Docker to output logs to standard output and error streams, which can be aggregated using centralized logging tools like the ELK stack or Fluentd.

10. **How do you handle scaling and load balancing for Docker containers in production?**
   - Use container orchestration tools like Kubernetes or Docker Swarm for automatic scaling and load balancing of containers in production environments. Kubernetes can scale pods based on resource utilization, and Swarm has built-in load balancing for services.
