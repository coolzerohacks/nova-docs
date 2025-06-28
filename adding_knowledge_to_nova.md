🧠 Adding Knowledge to Nova

This guide shows how to add new knowledge entries to Nova, convert them to structured YAML, and upload them into the vector store.
📌 Add Knowledge via Chat

To store new knowledge into a specific category (e.g. tv_shows), use this format inside Know's chat interface:

nova, file this under tv_shows: [your knowledge content here]

Example:

nova, file this under tv_shows: Breaking Bad Season 1 Episode 1 — Walter White begins his descent into crime after a terminal diagnosis.

🧱 Processing Pipeline

Once knowledge is added via chat, it flows through the following steps:
1. 🔄 Convert .txt files to .yaml

From the project root:

python3 tools/converters/txt_to_yaml.py

This will:

    Convert ./knowledge/<category>/raw/*.txt to .yaml

    Save the new files in ./knowledge/<category>/

    Delete the original .txt files

2. 🚀 Upload .yaml files

To upload the YAML knowledge entries:

python3 tools/uploaders/yaml_uploader.py

This will:

    Upload YAML files into Chroma

    Delete the .yaml files after successful upload

⚠️ Permissions Note

For this pipeline to work reliably, your user and the container must have write access to all ./knowledge subdirectories.

Run this once to fix ownership and permissions:

sudo chown -R $USER:docker ./knowledge
sudo chmod -R 775 ./knowledge

If your container runs with your host UID/GID (recommended), this ensures seamless access on both sides.

Cron Jobs

# Convert txt to YAML at 01:55
55 1 * * * /usr/bin/python3 /home/coolzerohacks/nova-setup/tools/converters/txt_to_yaml.py >> /home/coolzerohacks/txt_to_yaml.log 2>&1

# Upload YAML at 02:00
0 2 * * * /usr/bin/python3 /home/coolzerohacks/nova-setup/tools/uploaders/yaml_uploader.py >> /home/coolzerohacks/yaml_upload.log 2>&1
