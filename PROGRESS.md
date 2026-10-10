# Progress

Current step: **1 — AI vs ML vs DL vs GenAI; Python for AI setup**

## Log

| Step | Status | Finished | Notes |
| --- | --- | --- | --- |
| 0 Setup | Done | 2026-10-09 | Git, Flutter 3.47, Node 24 LTS via fnm, uv with Python 3.12 pinned per project, `.env` git-ignored. Pushed to GitHub over SSH. |

## Production gaps found

Gaps Claude spotted in how I build things, and whether I've fixed them.

| Gap | Where seen | Fixed? |
| --- | --- | --- |
| `uv init` defaults accepted without review (made the repo a package: `src/`, build-system, hello-world script) | Step 0, `pyproject.toml` | Yes |
| Manually downloaded binaries never update themselves | Step 0, fnm | Yes (moved to winget) |
| Default branch `master` instead of `main` | Step 0, git | Yes |

## Weak spots to revisit

- How the shell resolves commands through PATH (first match wins); activate *prepends* to PATH, it doesn't replace it.
- Prefer `uv run` over activate/full path: it syncs `.venv` to `uv.lock` before running.
- `.gitignore`: last matching pattern wins; it does nothing for already-tracked files (`git rm --cached` + rotate leaked keys).
