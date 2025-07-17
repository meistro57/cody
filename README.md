# Cody

Cody is a command-line assistant that connects to a local LLM service and helps you generate, edit and run code directly from your terminal. It uses Bash, `curl`, and `jq` to communicate with the model endpoint.

## Requirements
- Bash on Linux or macOS
- `curl` and `jq`
- An accessible HTTP endpoint compatible with the Gemma API (default `http://192.168.1.45:1234`)

## Getting Started
1. Install the required dependencies.
2. Start your local inference server. The script will detect Ollama running on
   `localhost:11434` and prompt you to choose between it and the LM Studio
   endpoint defined by `GEMMA_ENDPOINT`.
3. Run the script:
   ```bash
   ./cody
   ```
4. Interact with Cody using natural language or the slash commands below.

## Slash Commands
- `/create <file> <description>` – generate a new file
- `/edit <file>` – open a file in your editor
- `/run <file>` – execute a script (supports `.py`, `.js`, `.sh`)
- `/explain <file>` – get an explanation of a code file
- `/fix <file> <issue>` – attempt to fix the specified issue in the file
- `/files` – list project files in the directory where Cody was launched
- `/model` – choose another available model
- `/image` – paste an image from the clipboard to include in a prompt
- `/clear` – clear the conversation memory
- `/help` – display the command help
- `/exit` – quit Cody

Conversation history is stored in `~/.cody_global_memory` and your command history in `~/.cody_history`.

## License

