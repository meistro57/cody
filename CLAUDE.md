# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Cody is a self-modifying AI development assistant that operates as a bash script. It can execute commands, modify its own code, and interact with local LLM endpoints for AI functionality.

## Key Commands

### Running Cody
```bash
./cody                    # Start the interactive assistant
chmod +x cody            # Make executable if needed
```

### Configuration
- Edit the `cody` script directly to modify endpoints and settings
- System prompts are loaded from `cody_system.txt` or `~/.cody_system_prompt`
- Model preferences saved to `~/.cody_model`
- Memory stored in `~/.cody_global_memory`

### Dependencies
- `curl` - for API calls to LLM endpoints
- `jq` - for JSON processing
- Local LLM server (LM Studio, Ollama, etc.)

## Architecture

### Core Components

**Main Script (`cody`)**
- `load_system_prompt()` - Loads personality/behavior from text files
- `call_gemma()` - Makes API calls to LLM endpoints with system prompts
- `modify_self()` - Self-modification engine with automatic backups
- `execute_command()` - Command execution with safety checks
- `parse_input()` - Command parser for `/create`, `/edit`, `/run`, etc.

**Command Handlers**
- `handle_create()` - Creates files using AI generation
- `handle_edit()` - Opens files in available editors
- `handle_run()` - Executes files based on extension
- `handle_explain()` - AI-powered code explanation
- `handle_fix()` - AI-powered code fixing
- `handle_files()` - Lists project files with metadata

**Action Parser**
- `is_action_request()` - Detects natural language actions
- `execute_action()` - Converts phrases like "rename X to Y" to shell commands

### System Prompt Integration
The system prompt in `cody_system.txt` defines Cody's personality as an autonomous, action-oriented AI that executes commands instead of just suggesting them.

### Safety Features
- Automatic backups before self-modification
- Dangerous command blocking (`rm -rf`, `sudo`, etc.)
- Confirmation prompts for risky operations
- Backup management (keeps only 5 most recent)

## Development Notes

### Self-Modification
Cody can modify its own bash script code via the `/selfmod` command. This creates automatic backups and uses AI to analyze and implement changes.

### LLM Integration
- Supports multiple endpoints (LM Studio, Ollama)
- Uses OpenAI-compatible API format
- Includes project context in AI requests
- Manages conversation memory

### File Operations
- Auto-detects file types for execution
- Supports Python, JavaScript, Go, Ruby, Shell scripts
- Integrates with system editors (VS Code, nano, vim)

## Configuration Files

- `cody_system.txt` - System prompt defining AI behavior
- `DISCLAIMER.md` - Safety information
- `improvements` - Directory for enhancement tracking
- `LICENSE` - MIT license