# Cody - Self-Modifying AI Development Assistant

```
██████╗  ██████╗ ██████╗ ██╗   ██╗
██╔════╝██╔═══██╗██╔══██╗╚██╗ ██╔╝
██║     ██║   ██║██║  ██║ ╚████╔╝
██║     ██║   ██║██║  ██║  ╚██╔╝
╚██████╗╚██████╔╝██████╔╝   ██║
 ╚═════╝ ╚═════╝ ╚═════╝    ╚═╝
```

*Customizable Open-Source Development Yoda*  
*"The force is strong in this one..."*

Cody is a command-line AI assistant that can create, edit, run, explain, and fix code files, as well as self-modify its own script. It integrates with local LLM endpoints (such as LM Studio or Ollama) and supports project context awareness.

---

<img width="1110" height="626" alt="image" src="https://github.com/user-attachments/assets/c7c00380-f11d-4735-a43e-24bc849f2a01" />

## At a Glance

- **Purpose**: An AI-powered command-line co-pilot with safe automation features.
- **Target users**: Developers who want fast local AI workflows.
- **Core strengths**: Self-modification, natural-language commands, and lightweight setup.

---

## Table of Contents

- [Features](#features)
- [Quick Start](#quick-start)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Safety](#safety)
- [Project Layout](#project-layout)
- [Troubleshooting](#troubleshooting)
- [Project Docs](#project-docs)
- [Extending](#extending)
- [License](#license)

---

## Features

- **AI-powered code generation and editing**
- **Self-modification**: Cody can update its own script
- **File operations**: create, edit, run, explain, fix, and list files
- **Shell command execution** (with safety checks)
- **Natural language command parsing** (`test hello.py`, `check app.py`)
- **Model and endpoint selection**
- **Persistent memory and history**
- **Customizable via `.env` file**

---

## Quick Start

1. **Clone or copy Cody to your project directory.**
2. **Create a configuration file:**
   ```bash
   cp env.example .env
   # Edit .env to set your endpoints and preferences
   ```
3. **Install dependencies:**
   - Bash (v4+ recommended)
   - `curl`
   - `jq`
4. **Run Cody:**
   ```bash
   ./cody
   ```

---

## Prerequisites

- A local LLM endpoint (LM Studio, Ollama, or compatible).
- Bash 4+ (macOS users may need to install a newer Bash).
- `curl` and `jq` available in `PATH`.

---

## Installation

```bash
chmod +x cody
./cody
```

If you are running from a new repo, keep `cody`, `cody_system.txt`, and your `.env` together in the project root so context injection works reliably.

---

## Configuration

Cody loads configuration from a `.env` file in your project directory (or from `$HOME/.cody_env` if not found).

Example `.env`:
```bash
GEMMA_ENDPOINT="http://10.0.0.201:1234"
OLLAMA_ENDPOINT="http://127.0.0.1:11434"
MODEL_NAME="mistralai/codestral-22b-v0.1"
MEMORY_FILE="$HOME/.cody_global_memory"
HISTORY_FILE="$HOME/.cody_history"
MAX_BACKUPS=5
```

Recommended options:
- Keep `MEMORY_FILE` and `HISTORY_FILE` in your home directory for portability.
- Set `MAX_BACKUPS` to match your storage and rollback comfort level.

You can override any of these variables in your `.env`.

---

## Usage

Type `/help` in Cody for a list of commands:

- `/create <filename> <description>` – Create a new file
- `/edit <filename>` – Edit a file (uses `$EDITOR` if set)
- `/run <filename>` – Run a script file
- `/explain <filename>` – Explain code
- `/fix <filename> <issue>` – Fix code for a specific issue
- `/files [--no-dotfiles] [--sources]` – List files (hide dotfiles or show only source files)
- `/exec <command>` – Execute a shell command (with safety checks)
- `/selfmod <description>` – Modify Cody itself
- `/model` – Select model
- `/reload` – Reload system prompt
- `/clear` – Clear memory
- `/help` – Show help
- `/exit` – Quit Cody

You can also type natural language requests:
- "create a Python script that prints hello world"
- "test hello.py" (runs the file)
- "check app.py" (runs the file)
- "rename old.py to new.py"

---

## Safety

- Dangerous shell commands are blocked by default.
- Self-modification creates backups (see `MAX_BACKUPS`).
- Cody will prompt before executing most actions.

See [DISCLAIMER.md](DISCLAIMER.md) for the full safety notice.

---

## Project Layout

- `cody` — Main executable Bash script.
- `cody_system.txt` — System prompt that defines Cody’s behaviour.
- `env.example` — Configuration template.
- `README.md` — Primary documentation.
- `CLAUDE.md` — Architecture notes and development guidance.
- `ENHANCEMENTS.md` — Suggested features and roadmap ideas.
- `DISCLAIMER.md` — Safety and liability notice.

---

## Troubleshooting

- **No models available**: check `curl -s "$GEMMA_ENDPOINT/v1/models"` or `curl -s "$OLLAMA_ENDPOINT/api/tags"`.
- **Command blocked**: Cody blocks dangerous patterns by default; try a safer alternative.
- **Missing dependencies**: run `command -v curl && command -v jq`.
- **Configuration not loading**: verify `.env` exists and uses valid shell syntax.

---

## Project Docs

- [CLAUDE.md](CLAUDE.md) – Architecture notes and development guidance.
- [DISCLAIMER.md](DISCLAIMER.md) – Safety and liability notice.
- [ENHANCEMENTS.md](ENHANCEMENTS.md) – Suggested enhancements and additional features.

---

## Extending

- Cody is a single Bash script for easy hacking and extension.
- You can add more commands or customize its behavior.

---

## License

MIT License

---

*Created by Mark Hubrich*
