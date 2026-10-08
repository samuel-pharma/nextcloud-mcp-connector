# Contributing

Thanks for considering a contribution. This is a solo-maintained project with
hard quality gates; small, focused pull requests get reviewed fastest.

## Development setup

- Python 3.13 and [uv](https://docs.astral.sh/uv/)
- `uv sync --all-extras`
- Integration work needs a disposable Nextcloud; the `compose.yml` files in
  the repository root and the `tests/integration` fixtures show the expected
  topology

`.planning/` is the project's own working log (plans, audits, decisions) and
is checked in on purpose: every release decision is traceable there. Nothing
in it ships, and pull requests never need to touch it.

## The gates

Green locally before you push; CI runs the same set plus integration against
Nextcloud 34 and 35:

```sh
uv run pytest -q
uv run ruff check .
uv run ruff format --check .
PYRIGHT_PYTHON_FORCE_VERSION=latest uv run pyright
uv run vulture src scripts vulture_whitelist.py
uv run python scripts/check_tool_budget.py
```

The last gate holds the `tools/list` answer under its byte budget: every tool
description an MCP client downloads costs context window on the user's side,
so schema bytes are a budgeted resource here.

## Pull requests

- One concern per pull request, with tests; a behaviour change without a test
  will be asked for one.
- The tool surface is curated, not collected: a new MCP tool starts as an
  issue, because every tool costs budget and maintenance.
- The connector must never see more than the signed-in user; anything that
  widens rights is rejected regardless of how useful it is.
- Dependencies are locked in `uv.lock`; change it only through `uv` and say
  why in the commit message.

## Security problems

See [SECURITY.md](SECURITY.md); please do not open a public issue.
