# 📘 Nova Rasa User Manual

## ✅ Check Running Containers
Before running Rasa commands, make sure your Rasa container is running:
```bash
docker ps
```
Look under **NAMES** for your Rasa container name (for example `rasa`).

---

## 🎯 Train the Rasa Model
Run training inside your running container:
```bash
docker exec -it rasa rasa train
```
✅ Replace `rasa` with your container name if different.  
✅ This will generate a new model in the `/models` folder inside the container.

---

## ▶️ Run the Rasa Shell (Talk to your bot)
```bash
docker exec -it rasa rasa shell
```
✅ Lets you chat with your trained model in the terminal.

---

## 🔄 Run Rasa Actions Server (if using custom actions)
Make sure your actions container (often named `rasa-actions`) is running:
```bash
docker logs rasa-actions
```
✅ To start actions manually:
```bash
docker exec -it rasa-actions rasa run actions
```

---

## 🌐 Run Rasa with a Webhook (Production mode)
If exposing to other services:
```bash
docker exec -it rasa rasa run --enable-api --cors "*" --debug
```
✅ `--enable-api` allows API access.  
✅ `--cors "*"` allows requests from any frontend.  
✅ `--debug` shows detailed logs.

---

## 🛠 Common Commands Reference

| Purpose | Command |
|---------|---------|
| Train model | `docker exec -it rasa rasa train` |
| Talk to bot | `docker exec -it rasa rasa shell` |
| Run actions | `docker exec -it rasa-actions rasa run actions` |
| Run server (API) | `docker exec -it rasa rasa run --enable-api --cors "*"` |
| View logs | `docker logs rasa` |

---

## ✏️ Example Usage

**Train and test quickly:**
```bash
docker exec -it rasa rasa train
docker exec -it rasa rasa shell
```

**Start both services for development:**
```bash
docker exec -it rasa rasa run --enable-api --cors "*"
docker exec -it rasa-actions rasa run actions
```

---

*Nova Docs prepared for quick reference.*
