# Run Django with Docker Compose<br>
# Usage<br>

Run services in the background:
`docker-compose up -d` <br>

Run services in the foreground:
`docker-compose up --build` <br>

Inspect volume:
`docker volume ls`
and
`docker volume inspect <volume name>` <br>

Prune unused volumes:
`docker volume prune` <br>

View networks:
`docker network ls` <br>

Bring services down:
`docker-compose down` <br>

Open a bash session in a running container:
`docker exec -it <container ID> /bin/sh` <br>


# Flow <br>

1. The docker-compose yaml file will first spin up the Gunicorn container that will run the Django project at port 8000 <br>

2. The entrypoint to the *django_gunicorn* service is *entrypoint.sh*. This script will do a database migration and it will also collect the static files used by the Django project. <br>

3. The static files will be collected in *STATIC_ROOT*. This is the */static* directory in the container. <br>

4. This directory is mounted to a Docker volume <br>

5. The next container that will be spin is Nginx. The Dockerfile for this container is in the */nginx* folder. The Nginx configuration will interact with the Gunicorn service at port 8000 and it will also serve the static files in */static* also mounted to the same volume. <br>


# Endpoints <br>

* You will be able to reach the Django project at <pulic-ip-of-instance>:80. This is the Nginx endpoint that interacts with Gunicorn at <pulic-ip-of-instance>:8000. <br>
Admin page <pulic-ip-of-instance>:8000/admin
