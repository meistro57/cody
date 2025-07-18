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

### Non-Interactive Usage
```bash
echo "/explain file.py" | ./cody    # Process single command
echo -e "/create test.py\n/run test.py" | ./cody  # Multiple commands
```

### Configuration
```bash
cp env.example .env      # Create configuration file
# Edit .env to set endpoints and preferences
```

### Dependencies
- `curl` - for API calls to LLM endpoints
- `jq` - for JSON processing
- Local LLM server (LM Studio, Ollama, etc.)

## Architecture

### Core Script Structure
Cody uses a **monolithic bash architecture** with clear functional separation:

- **Configuration Layer** (lines 3-26): Environment loading, endpoint configuration
- **Core Engine Layer** (lines 45-393): System prompt management, API communication
- **Command Engine Layer** (lines 395-534): Command execution and action parsing
- **Handler Layer** (lines 536-769): Specific command implementations
- **Interface Layer** (lines 771-912): Input parsing, main loop, startup sequence

### Key Functions

**Configuration Management**
- `load_system_prompt()` - Loads AI behavior from `cody_system.txt` or fallback locations
- `load_model_preference()` - Restores previously selected LLM model
- `select_endpoint()` - Chooses between LM Studio and Ollama endpoints
- `manage_backups()` - Maintains backup rotation (keeps only `MAX_BACKUPS` files)

**LLM Integration**
- `call_gemma()` - Core API communication with context injection and error handling
- `get_project_context()` - Automatically includes project file information in AI requests
- `extract_code()` - Parses code blocks from AI responses using markdown syntax
- `fetch_available_models()` - Dynamically discovers available models from endpoints

**Command Processing**
- `parse_input()` - Main input router that distinguishes between commands (`/create`) and natural language
- `handle_*()` functions - Specialized handlers for each command type (`handle_create`, `handle_edit`, etc.)
- `execute_command()` - Shell command execution with safety checks and confirmation prompts

**Self-Modification System**
- `modify_self()` - Core self-modification engine with automatic backup creation
- `is_action_request()` - Natural language action detection using regex patterns
- `execute_action()` - Converts natural language to shell commands

### Command Parsing Architecture
The script uses a **two-tier parsing system**:
1. **Slash Commands**: Direct command routing (`/create`, `/edit`, `/run`, etc.)
2. **Natural Language Processing**: Action detection and conversion to shell commands

Example flow:
```
"rename test.py to main.py" → is_action_request() → execute_action() → mv "test.py" "main.py"
```

### Interactive vs Non-Interactive Modes
The script detects execution context using `[ ! -t 0 ]`:
- **Interactive Mode**: Full UI, model selection, endpoint testing
- **Non-Interactive Mode**: Streamlined processing for automation and piping

### Configuration Loading Strategy
**Hierarchical configuration system**:
1. Project-level `.env` file (highest priority)
2. User-level `~/.cody_env` file
3. Environment variables
4. Built-in defaults (lowest priority)

### Safety Features
- **Command Blacklisting**: Blocks dangerous commands using regex patterns in `execute_command()`
- **Confirmation Prompts**: User confirmation for command execution
- **Backup Management**: Automatic backup creation and rotation before self-modification
- **Context Limits**: Prevents token overflow in AI requests (files > 200 lines excluded from context)

## Development Notes

### Self-Modification System
Cody implements a **safe mutation pattern**:
1. **Backup Creation**: Automatic timestamped backups before changes via `modify_self()`
2. **AI Analysis**: LLM analyzes modification requests and generates implementation plans
3. **Code Extraction**: Parses generated code from AI responses
4. **Manual Review**: Presents changes for human review rather than automatic application

### LLM Integration Patterns
- **Context Injection**: Every AI request includes project context via `get_project_context()`
- **System Prompt Integration**: Consistent personality and behavior via `cody_system.txt`
- **Error Handling**: Graceful API failure handling with user feedback
- **Memory Management**: Conversation history with automatic truncation (400 lines max)

### File Operations
- **Auto-detection**: File types detected by extension for execution
- **Supported Types**: Python (.py), JavaScript (.js), Shell (.sh), Ruby (.rb), Go (.go)
- **Editor Integration**: Uses `$EDITOR` environment variable, falls back to code, nano, vim

### Command Safety
The `execute_command()` function blocks dangerous patterns:
- `rm -rf`, `sudo`, `chmod 777`
- Network operations (`curl http`, `wget http`)
- System commands (`shutdown`, `reboot`, `halt`)

## Configuration Files

### Environment Configuration
- `.env` - Project-level configuration (highest priority)
- `~/.cody_env` - User-level configuration
- `env.example` - Template with all available options

### Core Files
- `cody` - Main executable bash script
- `cody_system.txt` - System prompt defining AI behavior and personality
- `~/.cody_model` - Saved model preference
- `~/.cody_global_memory` - Conversation memory
- `~/.cody_history` - Command history

### Backup Files
- `cody.backup.YYYYMMDD_HHMMSS` - Timestamped backups created by self-modification
- Automatic rotation keeps only `MAX_BACKUPS` (default: 5) most recent backups

## Extension Points

### Adding New Commands
1. Create `handle_newcommand()` function following existing patterns
2. Add case in `parse_input()` function
3. Update help text in `print_header()` function

### Adding Natural Language Actions
1. Update regex patterns in `is_action_request()`
2. Add handling logic in `execute_action()`

### Configuration Options
New environment variables are automatically loaded from `.env` files during startup.

## Testing and Debugging

### Testing Commands
```bash
# Test individual commands
echo "/files" | ./cody
echo "/explain README.md" | ./cody

# Test with different models
MODEL_NAME="different-model" ./cody

# Test with different endpoints
GEMMA_ENDPOINT="http://localhost:8080" ./cody
```

### Debugging
- Check connection: `curl -s "$GEMMA_ENDPOINT/v1/models"`
- Verify dependencies: `command -v curl && command -v jq`
- Check configuration: `cat .env`
- View logs: `tail -f ~/.cody_global_memory`