## Compose sample application
### MySQL

Project structure:
```
.
├── README.md
└── docker-compose.yml
```

[_compose.yaml_](compose.yaml)
```
services:
  mysql:
    image: mysql:latest
    container_name: mysql_container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: anna
      MYSQL_PASSWORD: anna
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql # Persist data in a named volume

volumes:
  mysql_data:
```

## Deploy with docker compose

```
$ docker-compose up -d
[+] Running 2/2
 ✔ Network mysql_default      Created 0.1s 
 ✔ Container mysql_container  Started 0.4s 
```

## Expected result

Listing containers must show one container running and the port mapping as below:
```
$ docker ps
CONTAINER ID   IMAGE             COMMAND                  CREATED         STATUS         PORTS                                                  NAMES
245d4f95e7ff   mysql:latest      "docker-entrypoint.s…"   3 seconds ago   Up 2 seconds   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysql_container
```

After the application starts, connect to database using navicat or whatever you want.

Stop and remove the containers.
> Note: this will not remove volumes.
```
$ docker compose down
```
