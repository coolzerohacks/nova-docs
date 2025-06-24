# 🐳 Nova Docker Guide

This document outlines how to manage Nova’s Docker containers and build process.

---

## 📦 Setup Overview

Nova is composed of several containerized services, such as:

* `nova-core` – Mistral-based core logic
* `nova-discord` – Discord bot interface
* `nova-memory` – ChromaDB instance
* `nova-ingest` – Ingestion tools and pipelines

Make sure your `.env` file is configured correctly and Docker is installed and running.

---

## 🔄 Rebuild and Restart

Use this when you make changes to code, Dockerfiles, or dependencies:

```bash
docker compose down
docker compose build
docker compose up -d
```

This:

* Stops all containers
* Rebuilds with latest changes
* Restarts them in detached mode

---

## 🧾 Logs and Debugging

### Follow Logs for a Specific Service

```bash
docker compose logs -f nova-discord
```

Replace `nova-discord` with any service name to monitor logs live.

---

## 🛰️ Check Running Services

```bash
docker compose ps
```

Lists active containers and their states.

---

## 🧽 Full Cleanup (Optional)

Remove all unused containers, images, networks, and volumes:

```bash
docker system prune -a
```

⚠️ **Warning:** This is destructive — use only if you’re sure you want to remove all unused Docker data.

---

## 📁 Volumes and Persistence

Volumes store persistent data like Chroma memory state. To wipe and reset everything:

```bash
docker compose down -v
```

This deletes containers *and* their attached volumes.

---
