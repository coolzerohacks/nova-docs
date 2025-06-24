🧠 Recovering ChromaDB (Nova Memory)

If ./chroma/ is deleted or corrupted, follow this recovery guide to restore memory persistence for Nova.
1. Stop Chroma Container

docker compose stop chromadb

2. Recreate the Host Memory Directory

Ensure correct permissions:

mkdir -p ~/nova-setup/chroma
sudo chown -R $USER:$USER ~/nova-setup/chroma
chmod -R u+rwX ~/nova-setup/chroma

3. Restart Chroma Container

docker compose restart chromadb

4. Verify Chroma Is Running

docker logs -f chromadb

Look for: Listening on 0.0.0.0:8000
5. Rebuild Memory Using Nova Tools

From the tools/uploaders/ directory:

    Diary Entries

python3 tools/uploaders/generate_diary.py

Manual Conversation Imports

python3 tools/uploaders/diary_yaml_uploader.py

News RSS Feed

python3 tools/uploaders/news_rss_ingest.py

F1 Knowledge

python3 tools/uploaders/f1_ingest.py
python3 tools/uploaders/f1_sync.py

Other Topical Knowledge

    python3 tools/uploaders/technology_yaml_uploader.py
    python3 tools/uploaders/hacking_yaml_uploader.py
    python3 tools/uploaders/coding_yaml_uploader.py
    python3 tools/uploaders/tv_yaml_uploader.py
    python3 tools/uploaders/news_yaml_uploader.py
    python3 tools/uploaders/ctf_yaml_uploader.py
    python3 tools/uploaders/nova_build_yaml_uploader.py
    python3 tools/uploaders/template_yaml_uploader.py

✅ Done

Nova’s embedded ChromaDB is now rebuilt and synced with your local tools and containers.
