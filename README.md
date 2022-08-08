### 1. Docker Compose Golang API and postgres database
### 1.1 Applcation structure
    backend
        src
        tests
        Dockerfile
        go.mod
        go.sum
        main.go
    database
    web-proxy
    docker-compose.yml
    README.md

- backend: containes golang backend code
- database: Postgres files
- web-proxy: nginx files and serves as reverse server to backend application
- docker-compose.yml: docker commands to configure and run the whole system applications.

### 2 Run the system

#### 2.1. Start the system using `docker-compose.yml` file
Start the created docker images as per `docker-compose.yml` file.
```bash
sudo docker-compose up -d
```
This command starts all services and exposes port 80.

#### 2.1. Verify docker images were created and running
List all containers running by docker-compose command.
```bash
sudo docker-compose ps
```


#### 2.2. Stop the system by stopping docker containers
Stop the running docker containers as per `docker-compose.yml` file.
```bash
sudo docker-compose stop backend-api database web-proxy
```


#### 2.3. Stop and remove the services, Rebuild the system and restart
Delete existing containers.
```bash
sudo docker-compose down backend-api database web-proxy
```

Rebuild docker images as per `docker-compose.yml` file.
```bash
sudo docker-compose up -d
```





