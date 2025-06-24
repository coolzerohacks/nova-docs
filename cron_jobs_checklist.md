**Nova Cron Job Execution Checklist**

Date: 2025-05-31
Author: Echo
updated 2025-06-08
---


🕒 Scheduled Cron Jobs

🧠 Diary Generator

    Time: 23:00 daily

    Command:
    /usr/bin/python3 tools/uploaders/generate_diary.py

    Log: logs/diary.log

🗂️ Weekly Backup

    Time: 02:30 every Sunday

    Command:
    sudo /home/coolzerohacks/scripts/weekly_backup.sh

    Log: /var/log/weekly_backup.log

🏎️ F1 Sync & Ingest

    Time: 04:00 every Monday

    Command:
    tools/uploaders/f1_sync.py and tools/uploaders/f1_ingest.py

    Log: logs/f1_update.log

📰 News RSS Fetch (Sky News)

    Time: 06:00 daily

    Command:
    tools/uploaders/news_rss_ingest.py

    Log: logs/skynews_cron.log

🧹 Purge Old Logs

    Time: 03:00 every Sunday

    Command:
    find /home/coolzerohacks/logs -type f -name "*.log" -mtime +7 -delete

🔁 Git Auto-Sync

    Time: 03:30 daily

    Command:
    tools/git_autosync.sh

    Log: logs/git_cron.log

📄 Git Sync Nova Docs

    Time: 03:35 daily

    Command:
    tools/git_sync_docs.sh

    Log: logs/git_docs_cron.log

🧠 Compress Memory Facts

    Time: 06:10 daily

    Command:
    tools/compress_memory_facts.py

    Log: logs/compress_memory.log

🧠 YAML Knowledge Base Uploads (Daily @ 02:00)

    ctf_yaml_uploader.py → logs/ctf_uploader.log

    hacking_yaml_uploader.py → logs/hacking_uploader.log

    coding_yaml_uploader.py → logs/coding_uploader.log

    nova_build_yaml_uploader.py → logs/nova_build_uploader.log

    f1_yaml_uploader.py → logs/f1_uploader.log

    news_yaml_uploader.py → logs/news_uploader.log

    technology_yaml_uploader.py → logs/technology_uploader.log

    tv_yaml_uploader.py → logs/tv_uploader.log

    diary_yaml_uploader.py → logs/diary_uploader.log

🩺 GPU Heartbeat

    Time: Every minute

    Command:
    scripts/gpu_heartbeat.py

    Log: /var/log/gpu_heartbeat.log

🔍 Check Recent Output

tail -n 20 logs/diary.log
tail -n 20 logs/f1_update.log
tail -n 20 logs/skynews_cron.log
tail -n 20 logs/git_cron.log
tail -n 20 logs/git_docs_cron.log
tail -n 20 logs/compress_memory.log

# System-wide check (Ubuntu)
journalctl -u cron --since "2 days ago"
