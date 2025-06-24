# 🧠 Nova Memory System — Embedded DuckDB Mode (No REST)

This document outlines how Nova’s memory architecture works using a fully local, embedded ChromaDB setup powered by DuckDB. No external APIs. No REST. All memory is stored, recalled, and evolved within your local environment.

---

## 💾 Storage Architecture

Nova’s memory is managed through a local DuckDB database. It lives at:

```
./chroma/
```

This folder is shared between your host and the Nova container to ensure synchronized access to memory data.

---

## 🔗 Shared Volume (Docker Mount)

The Docker Compose config mounts the memory directory like so:

```yaml
volumes:
  ./chroma:/app/chroma
```

This allows:

* Host-side tools to write memory
* Nova (in Docker) to read that same memory in real-time

---

## 📍 Memory Insertion (Host Scripts)

Memory entries (e.g. diary entries, F1 updates, conversation summaries) are embedded and stored into Chroma via:

```python
from chromadb import Client
from chromadb.config import Settings

client = Client(Settings(
    chroma_db_impl="duckdb+parquet",
    persist_directory="./chroma/"
))
```

Each document is stored with metadata and a vector embedding, allowing semantic search and recall.

---

## 🗃 Memory Access (Nova)

Nova runs inside Docker, but because of the volume mount, it has real-time access to memory stored in DuckDB.

* Memory is pulled during response generation.
* A function like `get_relevant_snippets()` finds semantically similar past entries.
* These snippets are injected into system prompts sent to Mistral.

---

## 🧠 Memory Sources

### 📝 1. Conversation Logs

* Saved to `nova-memory/conversations/`
* Uploaded via `nova_memory_uploader.py`

### 🐶 2. Manual Facts (e.g. dog pack)

* Inserted via `insert_dog_memories.py`

### 🏎️ 3. F1 Knowledge

* Synced using `f1_sync.py`
* Embedded via `f1_ingest.py`

---

## 🧹 Memory Cleanup & Control

* Memory can be removed by ID or filtered keyword using tools like `clean_memory.py`
* Uploaded files (if any) are deleted or archived post-processing to avoid duplication

---

## 🔄 Cron Jobs (Optional)

* Conversation upload: every 10 min
* Diary entry: daily at 11PM
* Full Nova backup: weekly to `/mnt/nova-backup`

---

## ✅ Summary

* All memory is embedded via DuckDB, stored locally
* No HTTP, no external services
* Nova thinks from the same brain as your tools
* Fast, private, and totally yours
1~# 🧠 Nova Memory System — Embedded DuckDB Mode (No REST)

This document outlines how Nova’s memory architecture works using a fully local, embedded ChromaDB setup powered by DuckDB. No external APIs. No REST. All memory is stored, recalled, and evolved within your local environment.

---

## 💾 Storage Architecture

Nova’s memory is managed through a local DuckDB database. It lives at:

```
./chroma/
```

This folder is shared between your host and the Nova container to ensure synchronized access to memory data.

---

## 🔗 Shared Volume (Docker Mount)

The Docker Compose config mounts the memory directory like so:

```yaml
volumes:
  ./chroma:/app/chroma
```

This allows:

* Host-side tools to write memory
* Nova (in Docker) to read that same memory in real-time

---

## 📍 Memory Insertion (Host Scripts)

Memory entries (e.g. diary entries, F1 updates, conversation summaries) are embedded and stored into Chroma via:

```python
from chromadb import Client
from chromadb.config import Settings

client = Client(Settings(
    chroma_db_impl="duckdb+parquet",
    persist_directory="./chroma/"
))
```

Each document is stored with metadata and a vector embedding, allowing semantic search and recall.

---

## 🗃 Memory Access (Nova)

Nova runs inside Docker, but because of the volume mount, it has real-time access to memory stored in DuckDB.

* Memory is pulled during response generation.
* A function like `get_relevant_snippets()` finds semantically similar past entries.
* These snippets are injected into system prompts sent to Mistral.

---

## 🧠 Memory Sources

### 📝 1. Conversation Logs

* Saved to `nova-memory/conversations/`
* Uploaded via `nova_memory_uploader.py`

### 🐶 2. Manual Facts (e.g. dog pack)

* Inserted via `insert_dog_memories.py`

### 🏎️ 3. F1 Knowledge

* Synced using `f1_sync.py`
* Embedded via `f1_ingest.py`

---

## 🧹 Memory Cleanup & Control

* Memory can be removed by ID or filtered keyword using tools like `clean_memory.py`
* Uploaded files (if any) are deleted or archived post-processing to avoid duplication

---

## 🔄 Cron Jobs (Optional)

* Conversation upload: every 10 min
* Diary entry: daily at 11PM
* Full Nova backup: weekly to `/mnt/nova-backup`

---

## ✅ Summary

* All memory is embedded via DuckDB, stored locally
* No HTTP, no external services
* Nova thinks from the same brain as your tools
* Fast, private, and totally yours
