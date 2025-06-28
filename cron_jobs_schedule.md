🕒 Nova Cron Job Schedule

This document outlines all automated cron jobs used in the Nova system. These jobs perform routine tasks such as backups, data ingestion, vector uploads, and system monitoring.
📌 Location

All cron jobs are managed via crontab -e for the user coolzerohacks.

Logs are stored in:

~/logs/
~/nova-setup/logs/

🔁 Daily Jobs
Time	Job Description	Script Location	Output Log
01:55	Convert raw .txt knowledge to YAML	tools/converters/txt_to_yaml.py	~/txt_to_yaml.log
02:00	Upload .yaml knowledge to Chroma	tools/uploaders/yaml_uploader.py	~/yaml_upload.log
02:00	Git push of all repos (daily backup)	push_daily_backup.sh (auto-commits changes with date stamp)	~/logs/git_push.log
06:00	Ingest News RSS feeds	tools/uploaders/news_rss_ingest.py	~/nova-setup/logs/rss_ingest.log
06:10	Compress memory facts	tools/compress_memory_facts.py	~/nova-setup/logs/compress_memory.log
07:05	Check all cron job health	tools/monitoring/check_cron_status.sh (email or log mode)	(emailed or log, depending on setup)
Every 15 mins	GPU availability check	scripts/gpu_heartbeat.py	Silent (/dev/null)
🗓️ Weekly Jobs
Time	Day	Job Description	Script Location	Output Log
02:30	Sunday	Full system backup	tools/backup_scripts/weekly_backup.sh	/var/log/weekly_backup.log
03:00	Sunday	Container snapshot backup	tools/backup_scripts/snapshot-all-nova.sh	tools/backup_scripts/snapshot-cron.log
🌙 Nightly Jobs
Time	Job Description	Script Location	Output Log
23:00	Generate diary entry	tools/uploaders/generate_diary.py	~/nova-setup/logs/diary.log
🧪 Monitoring

All critical jobs are tracked via:

    tools/monitoring/check_cron_status.sh

    Scheduled to run daily at 07:05

    Reports missing or late jobs

    Sends summary to: cronjob_logs@proton.me
