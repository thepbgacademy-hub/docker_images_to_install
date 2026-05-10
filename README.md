# SGT Mini App Docker Image

This repository contains everything needed for the VPS to build and run the current `SGT` Self Guided Tour Mini App as a Docker container.

## Contents

- `Dockerfile`
- `nginx.conf`
- `dist/` production build output

The container serves the static app with `nginx` on port `80` and exposes a health endpoint at `/healthz`.

## VPS Build And Run

Clone the repository:

```bash
git clone https://github.com/thepbgacademy-hub/docker_images_to_install.git /opt/docker_images_to_install
cd /opt/docker_images_to_install
```

Build the image:

```bash
docker build -t sgt-mini-app:latest .
```

Run the container:

```bash
docker rm -f sgt-mini-app 2>/dev/null || true
docker run -d --name sgt-mini-app --restart unless-stopped -p 127.0.0.1:8080:80 sgt-mini-app:latest
```

## Reverse Proxy Target

Point the VPS reverse proxy for:

```text
https://sgt.spyderbyte.cloud
```

to:

```text
http://127.0.0.1:8080
```

## Health Check

The container returns:

```text
GET /healthz -> 200 OK
```

