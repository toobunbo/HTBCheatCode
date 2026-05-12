## Pull Request Process

1. Fork the repository and create a feature branch from `main`.
2. Keep PRs focused: one logical change per PR.
3. Include tests for new functionality.
4. Ensure `ruff check`, `ruff format`, `mypy`, and `pytest` all pass.
5. Write a clear PR description explaining **what** and **why**.

## Commit Messages

Use concise, imperative-mood messages:

```
feat: add XML escaping for LLM code context
fix: prevent path traversal in ContextProvider
refactor: centralize model defaults into constants.py
docs: add CONTRIBUTING.md
```
