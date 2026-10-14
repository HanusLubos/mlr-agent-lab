# mlr-agent-lab

Working rules for agents (and humans) in this repo live in [`AGENTS.md`](AGENTS.md).
Progress lives in [`PLAN.md`](PLAN.md). The audit log lives in [`RUNS.md`](RUNS.md).

## Goal

A small, reproducible lab for experimenting with **agentic MLR workflows** — building and
evaluating coding agents that can run a task end to end, check their own output, and report
honestly about what they verified.

The current repository is a **scaffold**: one runnable script plus the conventions that keep
later work reproducible. The substantive experiments are not written yet; `PLAN.md` is the
source of truth for where that stands, so read it before assuming scope.

## Requirements

| Tool | Version used here | Notes |
| --- | --- | --- |
| [uv](https://docs.astral.sh/uv/) | 0.13.1 | Python + dependency management |
| Python | 3.12.11 | resolved by `uv`, not installed by hand |
| git | any recent | repo lives on `main` |
| [gh](https://cli.github.com/) | 2.102.0 | only needed for GitHub operations |

`uv` and `gh` are installed **per-user** in `%USERPROFILE%\.local\bin` on this machine (no
administrator rights). They are already on the user `PATH`, so a new terminal finds them.

## How to run things

From the repository root:

```bash
uv run python hello.py     # the demo script
uv add <package>           # add a dependency (records it in pyproject.toml)
uv sync                    # create/sync the virtualenv from pyproject.toml
```

Do **not** use `pip install` against the global interpreter — see `AGENTS.md` §2.

One caveat worth knowing: there is **no `pyproject.toml` yet**, so `uv run` currently falls back
to an already-installed CPython rather than a project-local `.venv`. The commands above still
work, but nothing is pinned. First real step of `PLAN.md` is to fix that with `uv init` +
`uv add`.

## Layout

```
AGENTS.md   working rules — read these first
CLAUDE.md   loads AGENTS.md into Claude Code
README.md   this file: goal + how to run
PLAN.md     progress and next step
RUNS.md     run log: model, request, how it was checked
hello.py    demo entry point
```

## Repo location note

On this machine the project lives at `C:\MPA_MLR` (underscore). The Claude Code session default
directory is `C:\MPA-MLR` (dash) — a **different, empty** folder. `cd` into the underscore path
before running git or file commands.

## Remote

<https://github.com/HanusLubos/mlr-agent-lab> — public, default branch `main`.
