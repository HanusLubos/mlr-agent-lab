# RUNS

A log of what was run here, by which model, and — the point of this file — **how each result was
checked**. Newest entry first.

Entries exist so a later reader can tell the difference between "this was verified" and "this was
assumed." Keep the *How checked* sections honest; an unchecked claim is worse than a blank one.

---

## Run 4 — 2026-10-14 — working rules + docs

**Model** — unconfirmed. Claude Code routes through a custom proxy configured in the user's
settings file (`llm.ai.e-infra.cz`), where the model is set to the alias `agentic` (opus alias
`thinker`, haiku alias `mini`). Those are proxy aliases, not model IDs, so the real backing model
is not knowable from config. `/status` is a UI panel and is not readable from inside a run —
see TODO at the bottom.

**Asked** — Write `AGENTS.md` with the working rules (read README/PLAN first, uv-only Python,
run checks before claiming done); make `CLAUDE.md` load it; create `README.md`, `PLAN.md`,
`RUNS.md`.

**Changed** — added `AGENTS.md`, `CLAUDE.md`, `README.md`, `PLAN.md`, `RUNS.md`. No code touched.

**How checked**
- `uv run python hello.py` → `hello`, exit 0. Ran the documented command *before* writing it into
  README, rather than assuming it works.
- `uv run python -c "import sys,platform"` → `3.12.11 AMD64`; `uv --version` → 0.13.1;
  `gh --version` → 2.102.0. Versions in README are copied from real output, not from memory.
- Confirmed none of the five files pre-existed, so nothing was overwritten.
- Confirmed no `pyproject.toml` exists → documented that gap in README and PLAN instead of
  implying a pinned environment.

**Caveats**
- The `@AGENTS.md` import in `CLAUDE.md` is Claude Code syntax; it was not executed or verified to
  expand during this session.
- The Model field is a declared proxy alias, **not** a value read from `/status`.

---

## Run 3 — 2026-10-14 — public repo created and pushed

**Model** — same unresolved identity as Run 4.

**Asked** — Use `gh` to create a public repo `mlr-agent-lab` from this folder; show what would be
uploaded before pushing.

**Changed** — `git init` in `C:\MPA_MLR`, commit `6aa9ff9` (`hello.py`), created public repo,
pushed `main`.

**How checked**
- Previewed the upload and paused for approval before pushing, as requested.
- Confirmed the repo name was free: `gh repo view HanusLubos/mlr-agent-lab` → "Could not resolve".
- After pushing, read state back *from GitHub* instead of trusting push output:
  `gh repo view --json visibility` → `"visibility":"PUBLIC"`;
  `gh api .../git/trees/main?recursive=1` → one blob, `hello.py`, 15 bytes;
  `curl https://raw.githubusercontent.com/.../main/hello.py` → `print("hello")`.
- `git status --porcelain --ignored` → clean; `git rev-list --left-right --count origin/main...HEAD`
  → `0 0`, so nothing extra went up.

**Caveats**
- Found that `C:\MPA-MLR` (session cwd) and `C:\MPA_MLR` (project) are **different directories**;
  the dash one is empty. User chose the underscore folder as source, files left in place.

---

## Run 2 — 2026-10-14 — installed `gh` and `uv` per-user

**Model** — same unresolved identity as Run 4.

**Asked** — Install GitHub CLI and `uv` without administrator rights, into the user folder, and
check both work.

**Changed** — added `gh.exe`, `uv.exe`, `uvw.exe`, `uvx.exe` to `C:\Users\sobul\.local\bin`.

**How checked**
- Avoided `winget` for `gh` on purpose: its MSI targets `C:\Program Files` and needs elevation,
  which is exactly the constraint given. Used release zips + `Expand-Archive` instead.
- Verified the published sha256 of the uv zip before extracting: expected `3b2661a4...672` ==
  actual. `gh` publishes no checksum for its release assets.
- Functional tests, not just `--version`: `uv init` + `uv run python` built a venv and executed
  code; `uvx ruff --version` → `ruff 0.17.0` (downloaded and ran a third-party tool).
- Fresh-login PATH: rebuilt `PATH` from the registry alone and resolved `gh`, `uv`, `uvx` to
  `%USERPROFILE%\.local\bin`, proving new terminals find them with no PATH edit.
- Did not modify `PATH` — `.local\bin` was already on it. Left the pre-existing `claude.exe`
  in that directory untouched.

**Caveats**
- `gh` was installed left **unauthenticated**; the user logged in separately later.
- MSYS `tar` in Git Bash cannot read `.zip`; PowerShell `Expand-Archive` was required.

---

## Run 1 — 2026-10-14 — first script

**Model** — same unresolved identity as Run 4.

**Asked** — Write a Python program that prints hello, and run it. Also set git name/email.

**Changed** — created `hello.py`; confirmed git `user.name` / `user.email`.

**How checked**
- Ran it with Python 3.12 → stdout `hello`.
- `git config --global --get user.name|user.email` → both already set to the requested values, so
  no write was needed. Claim comes from command output, not assumption.

**Caveats**
- The `python` skill named in the first attempt does not exist in this session; the script was run
  directly instead.

---

## TODO for the user

The **Model** field is the one thing this file could not verify. `/status` is a Claude Code UI
panel and is not exposed to the agent, so a model name cannot be read from inside a run. Paste
what `/status` shows and it can be recorded properly — or accept that behind the
`llm.ai.e-infra.cz` proxy, the alias `agentic` is the most accurate label available.

Related note, kept deliberately vague: the Claude Code user settings file outside this repo stores
an `ANTHROPIC_AUTH_TOKEN` in plaintext. No value from it was copied into this repo, and none
should be — this repo is public.
