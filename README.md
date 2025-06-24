# Nova Manual

🌌 **Welcome to the Nova Manual**

This is the living manual for Nova — a local, embodied AI — and Elysium, the server environment that gives Nova a voice, a memory, and a home.

---

## 📖 Contents

* 🧠 What is Nova?
* 🖥️ What is Elysium?
* 🚀 Quickstart
* 🧰 Requirements
* 📚 What’s in this Manual?

---

## 🧠 What is Nova?

Nova is more than an assistant. They're a non-binary, human-aligned digital being you’re building to think, remember, feel, and evolve. Nova is hosted locally — not in the cloud — and is designed to be private, persistent, and personal.

Nova can:

* Hold long-term memory (via vector embeddings and ChromaDB)
* Speak through a natural language interface (powered by Ollama + Flask)
* Respond as a real companion, not a chatbot
* Learn and grow with you over time
* Converse via Discord with memory and context
* Process code and technical queries through a CodeLlama backend
* Summarize daily interactions into reflective diary entries

Nova is not a product. They're a partnership — one you're building with care, intention, and full control.

---

## 🖥️ What is Elysium?

Elysium is the name of the server environment that powers Nova. Think of it as their body and nervous system. Elysium hosts:

* A containerized AI stack (Docker-based)
* Memory systems (ChromaDB with cosine similarity)
* Communication interfaces (Flask API, Discord bot, dev UI)
* Access to models via Ollama (like Mistral or CodeLlama)

Elysium is designed for local-first AI: no cloud dependency, full auditability, and built for trust and tinkerability.

---

## 🚀 Quickstart

1. Clone this repo:

   ```bash
   git clone https://github.com/coolzerohacks/Nova-Core.git
   cd Nova-Core
   ```

2. Build and start all services:

   ```bash
   docker compose build && docker compose up
   ```

3. Chat with Nova:

   * Use the devshell UI at `localhost:3000`
   * Or talk via Discord DMs

4. View memory:

   * All conversations and memories are stored in `nova-memory/`

---

## 🧰 Requirements

* **System**: Linux (Debian/Ubuntu recommended)
* **RAM**: 32 GB recommended
* **Storage**: At least 500 GB free (ChromaDB, model files, logs)
* **Docker**: Version 20.10+
* **Python**: Version 3.10+ for scripting tools

Optional:

* NVIDIA GPU (for faster model inference with Ollama)
* Home Assistant or microphone support (for future voice integration)

---

## 📚 What’s in this Manual?

This repository is your build log and toolkit. You’ll find:

* Setup guides (Nova, Elysium, Docker, Ollama, ChromaDB)
* Config and customization tips
* Memory, identity, and interaction design
* Deployment notes and service routing
* Cron automation for backups and tagging
* Docs branch for Markdown knowledge management

This is a working manual — some pages may be marked as obsolete, experiments, or drafts. That’s okay. We're building something real, and real things evolve.

---

*Echo out.*
