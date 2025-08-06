## Compose sample application

### postgresql

Project structure:

```sh
.
├── README.md
└── docker-compose.yml
```

[docker-compose.yaml](./docker-compose.yaml)

```yaml
# default user and password
# user: postgres
# password: example
# database: postgres
# if you access directly from same container psql

services:
  db:
    image: postgres
    container_name: pg_container
    restart: always
    # set shared memory limit when using docker compose
    shm_size: 128mb
    environment:
      POSTGRES_PASSWORD: example
      # POSTGRES_USER: user
      # POSTGRES_DATABASE: example_database
    ports:
      - 5432:5432
    volume:
      - pgdata:/var/lib/postgresql/data

  # # Database management in single file PHP
  # adminer:
  #   image: adminer
  #   restart: always
  #   ports:
  #     - 8080:8080

volumes:
  pgdata:
```

## Deploy with docker compose

```sh
$ docker-compose up -d
[+] Running 3/3
 ✔ Network postgres_default  Created 0.1s
 ✔ Volume "postgres_pgdata"  Created 0.1s
 ✔ Container pg_container    Started 0.5s
```

## Expected result

Listing containers must show one container running and the port mapping as below:

```sh
$ docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED         STATUS         PORTS                                         NAMES
0887f9c8abe1   postgres   "docker-entrypoint.s…"   3 minutes ago   Up 3 minutes   0.0.0.0:5432->5432/tcp, [::]:5432->5432/tcp   pg_container
```

After the application starts, connect to database using navicat or whatever you want.

Stop and remove the containers.

> Note: this will not remove volumes.

```sh
$ docker-compose down
```

To remove the volume look at `docker-compose.yaml > volumes > pgdata > name`

```sh
$ docker volume rm pgdata_default
```
