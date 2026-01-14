# Enhancements and Additional Features

This document outlines proposed enhancements and additional features for Cody. The goal is to improve usability, safety, extensibility, and developer experience while keeping the tool lightweight and hackable.

## 1) User Experience Improvements

- **Interactive onboarding wizard**
  - Guides first-time setup (creating `.env`, selecting endpoint/model).
  - Validates endpoint connectivity with clear, actionable feedback.
- **Command discovery UI**
  - Contextual command suggestions as you type (based on history and repo files).
  - `/help` upgrade: searchable, grouped by task (create/edit/run/etc.).
- **Session profiles**
  - Named profiles for different projects (per-project models, memory files, and endpoints).

## 2) Safety and Governance

- **Command risk scoring**
  - Introduce a risk tier system (low/medium/high) with optional auto-approval for low-risk commands.
- **Audit log**
  - Append all executed commands and file modifications to a log with timestamps.
- **Sandbox mode**
  - Optional dry-run or restricted mode to prevent any file system writes or external calls.

## 3) Project Awareness and Context

- **Language-aware context packing**
  - Prefer relevant files (e.g., for Python, include `pyproject.toml`, `requirements.txt`).
- **Incremental context caching**
  - Cache summaries of large files to avoid re-sending full content each request.
- **Context filters**
  - User-defined include/exclude patterns (e.g., ignore `dist/`, `node_modules/`).

## 4) LLM and Tooling Enhancements

- **Multi-model workflows**
  - Route “analysis” vs “code generation” to separate models/endpoints.
- **Streaming responses**
  - Stream output as tokens arrive for better responsiveness.
- **Local tool runner**
  - Allow tool execution with explicit opt-in (e.g., linting, tests, formatting).

## 5) Developer Productivity

- **Project templates**
  - `cody init` to scaffold common project types (Python, Node, Go).
- **Code quality automation**
  - Optional auto-format after file creation or edit.
- **Task orchestration**
  - A simple task runner config (e.g., `.cody_tasks`) for common workflows.

## 6) Extensibility

- **Plugin system**
  - Load custom commands or handlers via a `plugins/` directory.
- **Hook system**
  - Pre/post hooks for commands (`/run`, `/create`, `/edit`).
- **Event-based architecture**
  - Emit events for command lifecycle phases to enable analytics or plugins.

## 7) Observability and Debugging

- **Verbose debug mode**
  - Emits detailed trace logs for API calls and prompt construction.
- **Diagnostics report**
  - Generates a single snapshot (environment, config, model list, etc.).
- **Health checks**
  - Add `/doctor` to verify dependencies and config validity.

## 8) Documentation and Support

- **Interactive tutorials**
  - Step-by-step guided commands for new users.
- **Example prompts**
  - Curated examples for typical development tasks.
- **Troubleshooting playbooks**
  - Common failures and how to resolve them.

---

## Suggested Priorities

1. **Short-term**: `/doctor`, audit log, context filters.
2. **Mid-term**: plugin system, multi-model workflows, streaming responses.
3. **Long-term**: onboarding wizard, sandbox mode, event-based architecture.

---

If you want any of these implemented, specify priorities, platform constraints, and the target experience (minimal vs. fully-featured).
