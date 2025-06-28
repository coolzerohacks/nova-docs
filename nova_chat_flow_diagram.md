🧭 Nova Chat Flow Diagram — Text View

[User Message] 
     ↓
[chat_routes.py] ──→ [rasa_intent.py] → [Intent Result]
     ↓
[Intent Dispatch in chat_routes.py]
     ├─→ [intent_handlers/ (commands)]
     ├─→ [nova_live_search.py] → [Return Results] 
     └─→ [intent_utils.py]
                ↓
     [query_knowledge_base()] → [Return Memory]
                ↓
         [Return to chat_routes.py]
                ↓
[chat_memory.py] ← Stores/Retrieves Turns
                ↓
[Repeat & Hallucination Guards] ← Checks chat_memory
                ↓
[greetings_guard.py] ← Only on session start
                ↓
[build_mistral_prompt()]
                ↓
[Mistral LLM Call]
                ↓
[Store Turn → chat_memory.py]
                ↓
[Final Output to User]
