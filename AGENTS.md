# Working Rules

Read these before changing anything. They apply to every session in this repo.

## 1. Read first, then act

Before writing or editing code, read:

1. [`README.md`](README.md) — what this project is and how to run it
2. [`PLAN.md`](PLAN.md) — what is already done and what comes next

Do not start from a guess about scope when both files answer it. If they contradict each other
or the request, say so and ask rather than silently picking one.

## 2. Python always goes through `uv`

- Run code: `uv run <script.py>` or `uv run <tool>`
- Add a dependency: `uv add <package>`
- Create an environment: `uv sync`

**Never** `pip install` into the global/system interpreter, and never invoke `python` directly
when `uv run python` works. Global installs break reproducibility and are not captured in
`pyproject.toml`, so the next person (or the next run) does not get them.

Dependencies belong in `pyproject.toml`. If you see a dependency used in code but absent from it,
that is a bug — fix it with `uv add`.

## 3. Run checks before saying "done"

"Done" is a claim about verified state, not about having written code. Before reporting
completion, actually run the relevant checks and read their output:

```bash
uv run python hello.py   # the thing you just changed still works
```

Then confirm the specific thing you claimed. Rules of thumb:

- A command you did not run did not pass.
- Reporting success for an untested command is a defect, not a small shortcut.
- If a check fails, report the failure and its real output. Do not bury it.
- If you could not run a check, say which one and why instead of implying it passed.
- Reading a file back to confirm an edit landed is redundant; running behaviour is not.

## 4. Repository hygiene

This repo is **public**. Never commit secrets, tokens, API keys, or `.env` files. Before any
push, confirm nothing sensitive is staged (`git diff --cached --stat`). Do not copy values out of
machine-local config such as `~/.claude/settings.json` into tracked files.

## 5. Keep the docs honest

`PLAN.md` tracks real progress, and `RUNS.md` records how work was checked. When you finish a
step, update them in the same change. A plan that describes work already superseded is worse than
no plan.
