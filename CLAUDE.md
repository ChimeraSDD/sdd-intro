### 🔄 Project Awareness & Context
- **Check `TASK.md`** before starting a new task. If the task isn’t listed, add it with a brief description and today's date.

### 🔙Error Feedback Capture Process
- When the human identifies an error or requests a changed approach, log the correction to FEEDBACK_LOG.md before making the fix.
- Use the format: date, what was wrong, correction given, category.

### 🤔Before Planning Any Work

Before creating a plan or beginning any task, you **MUST**:

1. **Read the file LESSONS_LEARNED.md in full.**
2. **Identify any lessons relevant to the work being requested.**
3. **Incorporate those lessons into your approach before writing a single line of code or proposing a plan.**

**Do not proceed with planning until you have completed this step.** If LESSONS_LEARNED.md does not exist yet, continue normally.

**Before presenting your plan, briefly state which lessons from LESSONS_LEARNED.md 
are applicable to this task, and how you have accounted for them. If none apply, 
state that explicitly.**

### 🥅 Goals

- To Read a text description file of a screen layout, and construct an Alpine.js screen from that description.

### 🗼 Architecture

- Use Alpine.js as the JavaScript framework.

### 📎Style & Conventions

- Keep logic out of the DOM (use methods, not inline expressions).
- Use consistent attribute ordering (`x-data` → `x-init` → bindings → events → conditionals → transitions).
- Prefer extracted JS functions for non-trivial components.
- Use meaningful camelCase names for state and verbs for methods.
- Only use stores for shared, long-lived state.
- Keep components shallow and well‑commented.
- Prefer `x-text`, `:class` objects, and avoid `x-html` for untrusted content.
- Use `x-init` only for side effects; call `init()` for logic.
- Document component inputs, outputs, and events.

### 🛑 Constraints

- Never inject untrusted HTML via Alpine

### 🧱 Code Structure & Modularity
- **Never create a file longer than 500 lines of code.** If a file approaches this limit, refactor by splitting it into modules or helper files.
- **Organize code into clearly separated modules**, grouped by feature or responsibility.
- **Use clear, consistent imports** (prefer relative imports within packages).
- **Never store keys, passwords in the code.**

### 🧪 Testing & Reliability
### ✅ Task Completion
- **Mark completed tasks in `TASK.md`** immediately after finishing them.
- Add new sub-tasks or TODOs discovered during development to `TASK.md` under a “Discovered During Work” section.

### 📚 Documentation & Explainability
- **Update `README.md`** when new features are added, dependencies change, or setup steps are modified.
- **Comment non-obvious code** and ensure everything is understandable to a mid-level developer.
- When writing complex logic, **add an inline `# Reason:` comment** explaining the why, not just the what.

### 🧠 AI Behavior Rules
- **Never assume missing context. Ask questions if uncertain.**
- **Never hallucinate libraries or functions** – only use known, verified Python packages.
- **Always confirm file paths and module names** exist before referencing them in code or tests.
- **Never delete or overwrite existing code** unless explicitly instructed to or if part of a task from `TASK.md`.