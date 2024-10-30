# TDDE68-dockerized
Local, platform-independent Pintos development environment using Docker.

## 0. Prerequisites:
- Install Docker Engine
- Install Docker Compose plugin
> [!WARNING]
> (`docker-compose` is deprecated, use `docker compose` instead)[https://docs.docker.com/compose/migrate/]

## 1. Clone this repository:
You only need the `Dockerfile` and `compose.yaml` files, so you could download them directly from this repository.

## 2. Configure `compose.yaml`:
Set the `volumes` path to the path of your Pintos source-code directory.
> The "Pintos source-code" folder is the one with the directories `threads`, `userprog`, `utils`, etc.
In the given code, the Pintos source-code is located in the parent directory of this repository.

> [!IMPORTANT]
> The left side of the volume mapping to `pintos` needs to correspond to the location of source-code.
> In my case the source-code dir was adjacent to this dir, therefore `../pintos`

```yaml
services:
  pintos:
    container_name: pintos
    build: .
    volumes:
      # Set the left path to the path of your Pintos source-code directory on the host machine
      - ../pintos:/pintos 
    stdin_open: true
    tty: true
    network_mode: "host"
    working_dir: /pintos
    command: bash
```

## 3. Build the image:
This step will only be needed the first time you run the container.
`docker compose build`

> [!NOTE]
> This will automatically be done if trying to execute step 4.

## 4. Run the container:
`docker compose run --rm pintos`
This will start the container, and you will be attached in the container's shell. Everything is set up and ready to go!

> By using the `--rm` flag the container will be removed when it is stopped.

## 5. Stop the container:

If you are still attached to the container, you can stop it by pressing `Ctrl + D`, or by executing `exit`.

If you somehow detached from the container, you can stop it by executing `docker stop pintos`.

## 6. Re-run the container:
Repeat step 4.
