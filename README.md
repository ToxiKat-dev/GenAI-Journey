# GenAI Journey

My learning repo for becoming a GenAI / AI Engineer. Plan: [ROADMAP.md](ROADMAP.md) · Progress: [PROGRESS.md](PROGRESS.md)

## Step 0 — Environment setup

Do these in order. Tick each box when done. If anything fails, open Claude Code and paste the error.

### 1. Claude Code in VS Code

- [ ] VS Code 1.94 or later (Help → About)
- [ ] Extensions (`Ctrl+Shift+X`) → search **Claude Code** (publisher: Anthropic) → Install
- [ ] Click the ✻ Claude Code item in the status bar (bottom-right) → **Sign in** with your Claude account (needs a paid plan: Pro, Max, Team or Enterprise)
- [ ] Open this folder in VS Code (`File → Open Folder → genai-journey`), open Claude Code, and ask: *"What does my CLAUDE.md tell you to do?"* — it should describe the mentor setup
- [ ] Optional: install the standalone CLI too if you want to run `claude` in the terminal (see [docs](https://code.claude.com/docs/en/setup))

### 2. Core tools

- [ ] **Git** — `git --version`; set `git config --global user.name` and `user.email`
- [ ] **Python 3.12+** managed by **uv** — install from https://docs.astral.sh/uv/ then `uv --version`
- [ ] **Node.js LTS** — `node -v` (use nvm or fnm so you can switch versions)
- [ ] **Docker Desktop** — `docker run hello-world` (needed from Phase 2 onward)
- [ ] **Flutter** — you already have it; run `flutter doctor` and fix any red items
- [ ] VS Code extensions: Python, Pylance, Jupyter, Ruff, ESLint, Docker, Flutter

### 3. Accounts and API keys

API usage is billed separately from your Claude subscription. Set a monthly spending limit on every provider dashboard before you create keys.

- [ ] **MongoDB Atlas** — free M0 cluster (supports Vector Search); save the connection string
- [ ] **One LLM API key to start** — Google Gemini (has a free tier, good for learning), plus OpenAI or Anthropic when you reach Phase 1
- [ ] **GitHub** — create a repo `genai-journey` and push this folder
- [ ] Later (Phase 4): Langfuse or LangSmith account, a cloud account (Render/Railway or AWS/GCP)

### 4. Project setup

```bash
cd genai-journey
git init
uv init --python 3.12          # creates pyproject.toml
uv add jupyter numpy pandas python-dotenv
cp .env.example .env           # then fill in your real keys — .env is git-ignored
git add . && git commit -m "Initial setup"
```

### 5. Verify

Ask Claude Code: **"Run the environment check for Step 0"** — it will check each tool's version, confirm `.env` is ignored by git, and list anything missing.

When everything passes, say **"Step 1"**.

## Layout

```
genai-journey/
├── CLAUDE.md        # instructions Claude Code reads every session
├── ROADMAP.md       # the 30-step plan
├── PROGRESS.md      # status, notes, production gaps
├── notes/           # my notes per step
├── exercises/       # small practice code per step
└── projects/        # portfolio projects
```
