# 🗂️ Cursor Memory Bank Starter

This repository shows how to organise a **Memory Bank** for Cursor-AI so that the assistant keeps project context between sessions.

---

## 📦 Repository Structure

```
./
├── memory_bank_prompt.md   # Main prompt source (must live in repo root)
├── memory-bank/            # Appears after the first initialisation (core files + practices/…)
├── .gitignore              # Path to memory-bank/ is added here by the init step
└── README.md               # You are reading it right now
```

> `memory-bank/` can be absent before first launch; all templates will be generated automatically.

---

## 🚀 Quick Start

1. **Clone** the repository.
2. Ensure the file `memory_bank_prompt.md` is present in the repo root (it is in this repo already).
3. Open the project in Cursor and send the command:
   ```
   initialize memory bank
   ```
4. Cursor will create the `memory-bank/` directory, populate core files and generate an internal `memory-bank/README.md` with a command reference.
5. Start working: update `activeContext.md`, `progress.md`, and add docs under `practices/` as needed.

---

## 🤖 How to Load the Rules in Cursor

| Method | Steps |
|--------|-------|
| **User Rules in Settings** | 1. Open Cursor → `Settings` → `Custom Instructions`.<br>2. Copy the content of `memory_bank_prompt.md`.<br>3. Paste it into the **User Rules** field and save. |
| **File in the repository (recommended)** | Keep `memory_bank_prompt.md` in the repo root; Cursor reads it at the start of every session. |

> If both sources exist, the text in **User Rules** takes priority.

---

## 🛠️ Commands (Triggers)

| Command | What it does | When to run | Git Auto-commit? |
|---------|--------------|------------|------------------|
| `initialize memory bank` | Generates `memory-bank/`, appends the path to `.gitignore`, creates `memory-bank/README.md` | First setup or on a fresh clone | No |
| `update memory bank` | Cursor rereads every Memory Bank file and syncs its context | After significant project changes | No |
| `finalize session` | Appends/updates the **Project Status** section in this README | At the end of a work session | No |
| `plan` | Enters Planner Mode (asks clarifying questions, drafts an action plan) | Before major feature/change | No |
| *(optional)* auto-commit progress | If auto-commit is enabled, commits `progress.md` changes automatically | When auto-commit is active | Yes |

---

## 🧩 Practices & Knowledge Base

The file `memory_bank_prompt.md` already contains pattern/anti-pattern templates for DevOps, Data Engineering, Data Science and Software Development domains. After initialisation they will appear under `memory-bank/practices/...`.

> Feel free to add your own documents following the `## ✅ Pattern:` / `## ❌ …` format so Cursor can parse them easily.

---

## 🏁 Commit & CI

* You can enable auto-commit of progress through `.cursorrules` if desired.
* Otherwise commit as usual: `git add . && git commit -m "feat: update memory bank"`.

Happy hacking with Cursor! 🎉
