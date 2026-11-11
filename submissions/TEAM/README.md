# Cornell Text Authorship

Group22. Classify human and machine-written passages using Python notebooks.
Target metric:AUROC. Target public score:at least.98. No measured results yet.

## Start
```bash
git clone https://github.com/Jalil-g/Cornell-Text-Authorship.git
cd Cornell-Text-Authorship
uv sync --locked
cp .env.example .env
# Paste your token privately. Preserve an existing .env.
uv run jupyter lab
```

18 notebook plans,18 issues,six per member. Start issue1.
Notebooks are scaffolds. Implement each task and run it before reporting results.
Read [work plan](docs/work-plan.md),[notebook format](docs/notebook-contract.md),and [context](PROJECT_CONTEXT.md).
Keep explanations short. Keep experiment settings exact. No em dashes.
Do not commit data,credentials,models,or row predictions. No automatic uploads.
Check notebook files with `uv run python tools/check_notebooks.py`.
