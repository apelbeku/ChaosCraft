## Compose sample application

### MySQL

Project structure:

```sh
.
├── README.md
└── docker-compose.yml
```

[docker-compose.yml](./docker-compose.yml)

```yaml
services:
  mysql:
    image: mysql:latest
    container_name: mysql_container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      # MYSQL_DATABASE: my_database # Optional: Create a default database
      MYSQL_USER: anna
      MYSQL_PASSWORD: anna
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql # Persist data in a named volume

volumes:
  mysql_data:
    name: mysql_default
```

## Deploy with docker compose

```sh
$ docker-compose up -d
[+] Running 3/3
 ✔ Network mysql_default      Created 0.1s
 ✔ Volume "mysql_default"     Created 0.0s
 ✔ Container mysql_container  Started 0.3s
```

## Expected result

Listing containers must show one container running and the port mapping as below:

```sh
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                    NAMES
c636b61c9b42   mysql:latest   "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   0.0.0.0:3306->3306/tcp, [::]:3306->3306/tcp, 33060/tcp   mysql_container
```

After the application starts, connect to database using navicat or whatever you want.

Stop and remove the containers.

> Note: this will not remove volumes.

```sh
$ docker-compose down
```

To remove the volume look at `docker-compose.yaml > volumes > mysql_data > name`

```sh
$ docker volume rm mysql_default
```
