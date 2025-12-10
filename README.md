# Quick ClimWeb Demo Set up

Content Management System for NMHSs in Africa


## User Guide

Read more from the user guide - [climweb.readthedocs.io](https://climweb.readthedocs.io/)


## Prerequisites

Before installing ClimWeb, consider installing on your server:

1. **Docker Engine & Docker Compose Plugin :** Ensure that Docker Engine is installed and running on the machine where you plan to execute the docker-compose command https://docs.docker.com/engine/install/. Docker Engine is the runtime environment for containers.

## ClimWeb Installation Instructions

### 1. Download from source:

```sh
git clone https://github.com/Lesotho-Meteorological-Services/lesotho-climweb-docker.git climweb
```

```sh
cd climweb
```

---

### 2. Update environmental variables

Find and replace 192.168.8.30 with your PC/VM's IP address

```sh
nano .env
```

---

### 3. Build and launch a running instance of the CMS.

```sh
docker compose build
```

```sh
docker compose up -d
```

The instance can be found at `http://{PC or VM IP}`

---

### 4. Finally, create superuser to access the CMS Admin interface:

Log in to container interactive command line interface

```sh
docker exec -it climweb /bin/bash
```

Create superuser providing username, email and strong password

```sh
climweb createsuperuser
```

The admin instance can be found at `http://{PC or VM IP}/cms-admin`

---

# Some useful commands 

| Purpose           | Command |  Instructions        |                                                                                                                                                                                                      
|-------------------|-----------|-----------------------------------------------------------------------------|
| docker configurations          | `docker compose config` | validate and view the Compose file configuration               |
| login to shell          | `docker exec -it {container} /bin/bash` | interact with the container's command line and execute commands as if you were directly logged into the container |
| login to shell as root user      | `docker exec -u -0 -it {container} /bin/bash` | access a running Docker container and open a Bash shell inside it with the root user                                                                                                                                
| read docker logs            | `docker compose logs --follow {containers}` | real-time output of the containers' logs                                   |
| stop/remove docker containers       | `docker compose down --remove-orphans {containers}` | stop and remove Docker containers                                          |
| check containers status          | `docker compose  ps {containers}` | display container names, their status (running, stopped), the associated services, and their respective health states  |
| generate city forecasts from external source        | use the `login` command above and execute `python manage.py generate_forecast` | used for fetching 7-day forecast from external source (https://developer.yr.no/)       |
| setup mautic instance    | `docker compose --file docker-compose.mautic.yml --file docker-compose.yml build {containers}` followed by `docker compose --file docker-compose.mautic.yml --file docker-compose.yml {DOCKER_COMPOSE_ARGS} up -d` | setup mautic environmental variables i.e `MAUTIC_DB_USER`,`MAUTIC_DB_PASSWORD` and  `MYSQL_ROOT_PASSWORD`  then execute command |

