# PLAN

Status legend: `[x]` done and checked · `[ ]` not started · `[~]` in progress

## Where things stand

Scaffold exists and is verified working. No experimental code yet. Everything below the
scaffold line is unstarted.

## Done

- [x] `hello.py` — prints `hello`; verified by running it
- [x] Git identity configured globally (`HanusLubos` / `lubos.hanus6@gmail.com`)
- [x] `uv` 0.13.1 and `gh` 2.102.0 installed per-user, no admin rights
- [x] Public repo created and pushed: <https://github.com/HanusLubos/mlr-agent-lab>
- [x] Working rules written (`AGENTS.md`) and loaded from `CLAUDE.md`
- [x] Docs scaffolded: `README.md`, `PLAN.md`, `RUNS.md`

## Next step

**Pin the environment.** This is the one blocking item — nothing else is reproducible until it
exists. There is currently no `pyproject.toml`, so `uv run` silently uses an ambient CPython 3.12.11
and no dependency is recorded.

```bash
uv init --name mlr-agent-lab   # creates pyproject.toml (hello.py already exists, keep it)
uv add --dev pytest ruff
uv sync
uv run python hello.py         # must still print: hello
uv run ruff check .
```

Then commit. If `uv init` objects to the existing directory, add `pyproject.toml` by hand rather
than re-initialising over the scaffold.

## Later

- [ ] Add a real entry point (`main.py` or a `src/` package) once there is something to run
- [ ] Add first actual experiment/evaluation once the goal in `README.md` is narrowed
- [ ] CI: `uv run ruff check .` + `uv run pytest` on push to `main`
- [ ] Decide what "MLR" concretely means here — the goal statement is currently broad

## Known issues

- **Two confusingly similar directories.** Project is `C:\MPA_MLR` (underscore); session cwd is
  `C:\MPA-MLR` (dash), which is empty. Always `cd` to the underscore path first.
- **`git init` warned** `LF will be replaced by CRLF`. Harmless for now, but worth a
  `.gitattributes` (`* text=auto eol=lf`) before line endings cause real diffs.
- **Model identity unconfirmed** — see `RUNS.md`; the recorded value is from settings, not
  from `/status`.
