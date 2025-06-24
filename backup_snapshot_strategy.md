Nova Backup and Snapshot Strategy
🗂 System-Level Full Backup

    Frequency: Weekly

    Schedule: Every Sunday at 2:30 AM

    Script:
    /home/coolzerohacks/nova-setup/tools/backup_scripts/weekly_backup.sh

    Details:

        Performs a full backup of important host system data and configurations.

        Logs output to:
        /var/log/weekly_backup.log

📦 Docker Container Snapshots

    Frequency: Weekly

    Schedule: Every Sunday at 3:00 AM

    Script:
    /home/coolzerohacks/nova-setup/tools/backup_scripts/snapshot-all-nova.sh

    Details:

        Tags all Nova containers with a timestamped snapshot-YYYYMMDDTHHMMSS label.

        Saves each container as a .tar archive.

        Snapshot archives are stored at:
        /mnt/backup/nova-snapshots/

    Cron Log:
    /home/coolzerohacks/nova-setup/tools/backup_scripts/snapshot-cron.log

📬 Cron Job Failure Alerts

    Email Recipient: cronjob_logs@proton.me

    Mechanism:

        All cron jobs are configured to send output (stdout + stderr) via email if an error occurs.

        bsd-mailx and postfix are configured with Internet Site setup.

        Cron environment includes:
        MAILTO=cronjob_logs@proton.me
