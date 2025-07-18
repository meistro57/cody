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

2. **Copy and edit the environment file:**
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

## Interface Highlights

- **Welcome Banner**: ASCII art logo and tagline on startup.
- **Colorful Prompts**: Distinct colors for prompts, responses, and sections.
- **Status Bar**: Model, endpoint, and working directory shown in the header.
- **Animated Typing**: "Thinking..." animation with dots.
- **Command Hints**: `/help` shows all available commands.

---

## Safety

- Dangerous shell commands are blocked by default.
- Self-modification creates backups (see `MAX_BACKUPS`).
- Cody will prompt before executing most actions.

---

## Extending

- Cody is a single Bash script for easy hacking and extension.
- You can add more commands or customize its behavior.

---

## License

MIT License

---

*Created by Mark Hubrich*
