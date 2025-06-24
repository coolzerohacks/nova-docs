# Nova Recovery Summary

This document outlines the key steps we performed to recover and rebuild your Nova stack.

## 1. Build Custom Base Image (`nova-base`)

* Created `nova-devshell/Dockerfile.base` with:

  * System build dependencies (including `libsqlite3-dev`, `liblzma-dev`, `libffi-dev`, etc.)
  * Compiled and installed SQLite ≥ 3.35 from source, overriding the older system library.
  * Built and installed Python 3.11.8 with `altinstall`.
  * Copied and installed Python requirements (including PyTorch CUDA wheels and `requirements.txt`).

```bash
docker build -f nova-devshell/Dockerfile.base -t nova-base .
```

## 2. Build Devshell and Other Service Images

* Built the core devshell image against the new `nova-base`.
* Ensured each custom service (devshell-ui, nova-discord, template-router, wyoming-whisper) was rebuilt.

```bash
docker build -f nova-devshell/Dockerfile -t nova-devshell nova-devshell
# (repeat for other custom Dockerfiles)
```

## 3. Deploy the Compose Stack

* Took down any old containers and removed orphans:

```bash
docker compose down --remove-orphans
```

* Rebuilt and launched all services in one go:

```bash
docker compose up -d --build
```

* Verified all eleven services were running:

```bash
docker compose ps
```

## 4. External Network Fix

* Addressed the missing external `nova-setup` network by creating it:

```bash
docker network create nova-setup
```

## 5. Portainer Restoration

* Ran Portainer separately on the same network to avoid accidental teardown:

```bash
docker volume create portainer_data
docker run -d \
  --name portainer \
  --restart=always \
  --network nova-setup \
  -p 9000:9000 \
  -p 9443:9443 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

## 6. Document Creation

## 7. Chromdb see recovering_chromadb.md documentation
* Generated this summary and the earlier “recovering Nova” guide for reference.
