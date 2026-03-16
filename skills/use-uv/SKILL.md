---
name: use-uv
description: Enforces that all Python execution uses `uv run` instead of bare `python` or `python3`. Apply this skill whenever running Python scripts, modules, or one-liners — including `pip install`, `pytest`, `jupyter`, or any Python-based CLI tool. Activate proactively any time a shell command would invoke Python or a Python package manager, even if the user doesn't mention uv.
---

# Use `uv` for all Python execution

This project uses [uv](https://docs.astral.sh/uv/) to manage Python versions and dependencies. Running bare `python`, `python3`, `pip`, or `pip install` bypasses the project's virtual environment and dependency lockfile, which leads to missing packages, wrong Python versions, and unreproducible results.

## Rules

1. **Scripts and modules**: use `uv run python script.py` or `uv run python -m module` instead of `python script.py` or `python -m module`.
2. **Package installation**: use `uv add <package>` (to add a dependency) or `uv pip install <package>` (for one-off installs in the venv) instead of `pip install`.
3. **Python-based CLI tools** (pytest, jupyter, ruff, mypy, etc.): prefix with `uv run`, e.g. `uv run pytest`, `uv run jupyter lab`.
4. **One-liners**: `uv run python -c "..."` instead of `python -c "..."`.

## Why this matters

`uv run` ensures the correct Python version (declared in `pyproject.toml`) and the project's locked dependencies are always active. Without it, commands silently use the system Python, which may be a different version or missing project dependencies entirely.
