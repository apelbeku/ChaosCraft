## Compose sample application
### PHP application with Nginx

Project structure:
```
.
├── README.md
├── docker
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── nginx
│       └── nginx.conf
└── src
    └── public
        └── index.php
```

## Deploy with docker compose

```
$ docker-compose up --build -d
[+] Building 2.4s (10/10) FINISHED docker:default
 => [php internal] load build definition from Dockerfile 0.0s
 ...
 ...
[+] Running 4/4
 ✔ php                         Built 0.0s 
 ✔ Network docker_app-network  Created 0.1s 
 ✔ Container nginx-php         Started 0.7s 
 ✔ Container nginx-web-php     Started 0.7s 
```

## Expected result

Listing containers must show one container running and the port mapping as below:
```
$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                                  NAMES
9b4c61ea8da2   nginx-web-php   "docker-php-entrypoi…"   7 minutes ago    Up 7 minutes    9000/tcp                                               nginx-web-php
c08bfb0c45ba   nginx:latest    "/docker-entrypoint.…"   7 minutes ago    Up 7 minutes    0.0.0.0:80->80/tcp, :::80->80/tcp                      nginx-php

```

After the application starts, navigate to `http://localhost:80` in your web browser:

Stop and remove the containers
```
$ docker compose down
```
