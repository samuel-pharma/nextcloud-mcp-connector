## What this changes

<!-- One concern per pull request. Say what changes for a user or operator. -->

## Checklist

- [ ] `uv run pytest -q` is green locally
- [ ] `uv run ruff check .` and `uv run ruff format --check .` are green
- [ ] `PYRIGHT_PYTHON_FORCE_VERSION=latest uv run pyright` is green
- [ ] `uv run vulture src scripts vulture_whitelist.py` is green
- [ ] `uv run python scripts/check_tool_budget.py` stays under budget
- [ ] A behaviour change carries a test that fails without it
- [ ] Nothing widens what the signed-in user could see or do
