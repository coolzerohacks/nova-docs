✅ Nova To-Do Checklist
🔧 Core System Tasks

Improve Codellama memory filtering and result relevance

Remove any remaining memory logic duplication between models

Confirm new Discord logging is readable and complete

Add /status or /logs command to Discord bot

Audit autosync behavior and lock down .gitignore if needed

Tune system prompts for emotional tone and diary alignment

Standardize Python logging format across files

Check Codellama template system: template file detection, autofill response, and chat interface

    Validate Codellama Markdown templates work end-to-end

🧠 Memory + Prompt

Integrate Rasa actions into ChatMistral flow

Test Rasa intent handling with existing actions.py

    Sync Rasa response with Nova memory injection pipeline

🗣️ Voice Setup

Choose TTS engine: Coqui TTS / Piper / ElevenLabs

Test local TTS server or API for voice output

    Integrate voice playback into Nova response flow

🏠 Home Assistant

Decide on integration layer: Flask route vs WebSocket

Inventory supported actions (lights, music, sleep, etc.)

    Build endpoint and test Nova-initiated triggers

🧪 Testing + Debug Tools

Add /context command for memory injection debugging

Extend bot error logging for all endpoints

    Auto-prune unused templates, models, and scripts from legacy nova-brain

📄 Docs + Manual

Finalize setup.md with all ENV vars

Add ingestion.md with F1/diary vector steps

Add commands.md listing CLI and API utilities
