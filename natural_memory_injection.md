# 🧠 Nova Natural Memory Injection — YAML Knowledge Base Insertion

**Author:** Echo  
**Date:** 2025‑06‑08

---

## 📌 Purpose

Nova supports a natural-language memory injection command:

> Here is some <tv> info — please add it to your <tv> knowledge base:

Use this to feed structured content directly into Nova’s knowledge system — no manual file moves required. Nova will:

- Detect the `<category>` (e.g. tv, coding, news)
- Extract relevant YAML fields using Mistral
- Save the file to `knowledge/<category>/...`
- Let cron-based uploaders embed it into Chroma

---

## ✅ Command Format

Here is some <category> info — please add it to your <category> knowledge base:
<your content here>


- The tag inside `< >` must be a valid category
- Text should be concise, structured, and well-formed

---

## 🗂 Supported Categories

| Domain            | Tag in Command | Saved To Folder     | Embedded To Chroma Collection |
|-------------------|----------------|----------------------|-------------------------------|
| F1 Racing         | `<f1>`         | knowledge/f1         | f1                            |
| Capture The Flag  | `<ctf>`        | knowledge/ctf        | ctf                           |
| TV Shows          | `<tv>`         | knowledge/tv         | tv                            |
| News              | `<news>`       | knowledge/news       | news                          |
| Politics*         | `<politics>`   | knowledge/news       | news                          |
| Technology        | `<technology>` | knowledge/technology | technology                    |
| Hacking           | `<hacking>`    | knowledge/hacking    | hacking                       |
| Coding            | `<coding>`     | knowledge/coding     | coding                        |
| Nova Build        | `<nova>`       | knowledge/nova_build | nova_build                    |
| Diary Entries     | `<diary>`      | knowledge/diary      | nova-memory                   |
| User Facts        | `<user_fact>`  | knowledge/user_facts | nova-memory                   |

*Note: Politics is merged into the **news** base.

---

## 📁 Workflow Summary

1. **Detection:** Nova detects natural memory injection by regex pattern.
2. **Extraction:** Content is parsed and transformed into valid YAML using `extract_structured_fields()`.
3. **Storage:** Saved to `knowledge/<category>/<category>_<timestamp>.yaml`
4. **Upload:** A cron job runs the appropriate `tools/uploaders/<category>_yaml_uploader.py` nightly at 02:00.

---

## 📥 Example Usages

### TV Domain

Here is some <tv> info — please add it to your <tv> knowledge base:
“Severance” is a sci-fi TV series by Apple TV+, exploring work-life balance through memory separation.


- Saved to: `knowledge/tv/tv_<timestamp>.yaml`
- Uploaded by: `tv_yaml_uploader.py`
- Indexed to Chroma: `tv`

---

### Coding Domain

Here is some <coding> info — please add it to your <coding> knowledge base:
“List comprehensions in Python offer a concise way to create lists using a single expression.”


- Saved to: `knowledge/coding/coding_<timestamp>.yaml`
- Uploaded by: `coding_yaml_uploader.py`
- Indexed to Chroma: `coding`

---

### Nova Build Domain

Here is some <nova> info — please add it to your <nova> knowledge base:
“Nova’s memory uses embedded DuckDB mode for full offline persistence.”


- Saved to: `knowledge/nova_build/nova_<timestamp>.yaml`
- Uploaded by: `nova_build_yaml_uploader.py`
- Indexed to Chroma: `nova_build`

---

## 🧾 Notes

- Tag names are **case-sensitive** — use `<tv>`, not `<TV>`
- If you see `Unknown category: <x>`, it means the category isn’t in `category_map`
- You can manually inspect or edit files in the `knowledge/` directory
- View cron uploader logs at `logs/<category>_uploader.log`

---

Would you like this saved to `nova-docs/natural_memory_injection.md` now?
