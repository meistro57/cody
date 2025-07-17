# 🤖 Cody - Self-Modifying AI Development Assistant

*An autonomous AI assistant that writes code, executes commands, and modifies itself.*

![Cody Demo](https://img.shields.io/badge/Status-Experimental-orange)
![License](https://img.shields.io/badge/License-MIT-blue)
![Bash](https://img.shields.io/badge/Shell-Bash-green)

## ✨ What is Cody?

Cody is not just another chatbot - it's an **autonomous AI development assistant** that can:

- 🎯 **Execute actions** instead of just suggesting them
- 🔧 **Modify its own code** to improve functionality
- ⚡ **Run shell commands** and manage your project files
- 🐍 **Create complete programs** in Python, JavaScript, and more
- 🧠 **Learn from your project** context and adapt

Think of it as having a junior developer who never sleeps, never complains, and gets excited about automating everything.

## 🚀 Quick Start

### Prerequisites
- Linux/macOS terminal
- `curl` and `jq` installed
- Local LLM server ([LM Studio](https://lmstudio.ai/) or [Ollama](https://ollama.ai/))

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/cody
cd cody

# Make executable
chmod +x cody

# Create system prompt (optional)
cp cody_system.txt.example cody_system.txt

# Configuration
edit the cody file...
GEMMA_ENDPOINT="http://192.168.1.45:1234"
OLLAMA_ENDPOINT="http://127.0.0.1:11434"
MODEL_NAME="mistralai/codestral-22b-v0.1"
MEMORY_FILE="$HOME/.cody_global_memory"
HISTORY_FILE="$HOME/.cody_history"
WORK_DIR="$(pwd)"
SYSTEM_PROMPT=""
MAX_BACKUPS=5

# Run Cody
./cody
```

## 🎮 Usage Examples

### Basic Commands
```bash
❯ /create web_scraper.py script to monitor Reddit for AI news
Creating web_scraper.py...
✓ Created web_scraper.py (47 lines)

❯ /run web_scraper.py
🚀 Running web_scraper.py...
[scraper output]

❯ /files
📄 Files in: /home/user/project
  🐍 web_scraper.py (47 lines, 2KB)
  📝 README.md (120 lines, 5KB)
📊 Total: 2 files, 167 lines
```

### Natural Language Actions
```bash
❯ rename web_scraper.py to reddit_monitor.py
🎯 Action: rename web_scraper.py to reddit_monitor.py
⚡ Executing: mv "web_scraper.py" "reddit_monitor.py"
✓ Success

❯ copy README.md to backup.md
🎯 Action: copy README.md to backup.md
⚡ Executing: cp "README.md" "backup.md"
✓ Success
```

### Self-Modification
```bash
❯ /selfmod add better error handling
⚙️ Self-modification: add better error handling
✓ Backup: cody.backup.20250717_141652
Analyzing self-modification...
🤖 Modification Plan:
[Cody analyzes and suggests improvements to its own code]
```

## 🛠️ Available Commands

| Command | Description | Example |
|---------|-------------|---------|
| `/create` | Create new files | `/create app.py web server with Flask` |
| `/edit` | Edit files in your editor | `/edit app.py` |
| `/run` | Execute files | `/run app.py` |
| `/explain` | Explain code | `/explain app.py` |
| `/fix` | Fix code issues | `/fix app.py syntax error` |
| `/files` | List project files | `/files` |
| `/exec` | Execute shell commands | `/exec ls -la` |
| `/selfmod` | Modify Cody's code | `/selfmod add new feature` |
| `/reload` | Reload system prompt | `/reload` |
| `/model` | Switch AI models | `/model` |

## ⚙️ Configuration

### System Prompt
Create `cody_system.txt` to customize Cody's personality:

```
You are Cody, a confident AI development assistant.
You execute actions decisively and improve yourself continuously.
Be helpful, direct, and action-oriented.
```

### Model Configuration
Cody works with:
- **LM Studio**: Local inference server
- **Ollama**: Local model management
- **Any OpenAI-compatible API**

Models tested:
- `mistralai/codestral-22b-v0.1` (recommended)
- `google/gemma-3-12b`
- `deepseek/deepseek-r1`

### File Locations
- System prompt: `./cody_system.txt` or `~/.cody_system_prompt`
- Memory: `~/.cody_global_memory`
- History: `~/.cody_history`
- Model preference: `~/.cody_model`

## 🎯 Features

### ✅ **What Works**
- **File Operations**: Create, edit, run, explain code
- **Command Execution**: Direct shell command execution
- **Self-Modification**: Cody can improve its own code
- **Natural Language**: "rename X to Y" → actual execution
- **Project Awareness**: Understands your file structure
- **Tab Completion**: Auto-complete commands and filenames
- **Backup Management**: Automatic backup creation and cleanup
- **Multi-Model Support**: Switch between different AI models

### 🔄 **Smart Features**
- **Action Detection**: Recognizes when you want something done vs explained
- **Context Management**: Includes relevant project files in AI context
- **Safety Checks**: Blocks dangerous commands like `rm -rf`
- **Automatic Backups**: Creates backups before self-modifications
- **Word Wrapping**: Clean display of system prompts and responses

## 🧠 How It Works

1. **System Prompt**: Defines Cody's personality and behavior
2. **Action Parser**: Detects when you want actions vs explanations
3. **Command Executor**: Safely executes shell commands
4. **Self-Modifier**: Can modify its own bash script code
5. **AI Integration**: Calls local LLM for intelligence
6. **Context Builder**: Includes project files for awareness

## 🎪 Cool Examples

### Web Development
```bash
❯ /create server.js simple Express web server
❯ /create index.html landing page for the server
❯ /run server.js
```

### Data Science
```bash
❯ /create analyze.py script to analyze CSV data with pandas
❯ copy data.csv to backup_data.csv
❯ /run analyze.py
```

### DevOps
```bash
❯ /create monitor.py system monitoring script
❯ make monitor.py executable
❯ /exec crontab -e
```

## 🔬 Advanced Usage

### Custom System Prompts
Create different personalities for different tasks:

```bash
# Aggressive optimizer
echo "You optimize everything for performance" > performance_cody.txt

# Security focused
echo "You prioritize security in all decisions" > security_cody.txt
```

### Chaining Actions
```bash
❯ create backup.py daily backup script, then make it executable, then add to cron
```

### Self-Improvement Loops
```bash
❯ /selfmod analyze your own code and suggest 3 improvements
❯ /selfmod implement the most important improvement
```

## 🤝 Contributing

Contributions welcome! Cody can even help you contribute:

```bash
❯ /create feature.py implementation of new feature X
❯ /create test_feature.py unit tests for feature X
❯ git add feature.py test_feature.py
```

## 📜 License

MIT License - see LICENSE file for details.

## ⚠️ **Important Disclaimer**

**Cody executes real commands on your system and can modify its own code.** 

- ✅ Use in safe, isolated environments
- ✅ Review generated code before production use
- ✅ Keep backups of important files
- ❌ Don't run with elevated privileges unnecessarily

See [DISCLAIMER.md](DISCLAIMER.md) for full safety information.

---

## 🎉 What Users Say

*"It's like having a junior developer who never gets tired and actually does what you ask instead of just talking about it."* - Anonymous Beta Tester

*"I asked it to improve itself and now I'm slightly concerned about what I've created."* - Creator

*"Finally, an AI that actually executes commands instead of giving me copy-paste suggestions."* - Happy User

---

**Ready to build the future with an AI that builds itself?** 🚀

```bash
git clone https://github.com/yourusername/cody && cd cody && ./cody
```
