# ⚠️ DISCLAIMER

## Important Notice

**Cody is an experimental self-modifying AI assistant that executes shell commands and modifies code automatically.**

### 🚨 **USE AT YOUR OWN RISK**

- **Cody executes commands directly on your system** — it can create, modify, or delete files.
- **Cody can modify its own source code** — behaviour may change unexpectedly.
- **No warranty or guarantee** of safety, security, or correctness.
- **Always review generated code** before execution in production environments.
- **Run in isolated environments** when testing new features.
- **Keep backups** of important files (Cody creates its own backups but do not rely solely on them).

### 🛡️ **Safety Features**

- Basic safety checks block dangerous commands (`rm -rf`, `sudo`, etc.).
- Automatic backup creation before self-modifications.
- Confirmation prompts for command execution.
- Limited context to prevent token overflow.

### 🔐 **Security and Privacy**

- **Local endpoints are still network services** — treat them as trusted dependencies.
- **Logs may contain sensitive context** — review memory and history files regularly.
- **Do not store secrets** in `.env` or prompts unless you understand the risks.

### ⚖️ **Legal**

- **No liability** for any damage, data loss, or system issues.
- **Educational/experimental use only** — not intended for production systems.
- **You are responsible** for understanding what Cody does before using it.
- **Compliance with local laws** regarding AI and automated systems is your responsibility.

### 🔧 **Recommendations**

- ✅ Test in virtual machines or containers first.
- ✅ Review the system prompt (`cody_system.txt`) before use.
- ✅ Monitor Cody's actions closely, especially self-modifications.
- ✅ Keep regular backups of your work.
- ❌ Do not use on production systems without extensive testing.
- ❌ Do not run with elevated privileges unless absolutely necessary.

---

**By using Cody, you acknowledge that you understand these risks and accept full responsibility for any consequences.**

*"With great AI power comes great responsibility" - Uncle Ben, probably*
