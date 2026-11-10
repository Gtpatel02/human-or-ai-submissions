# Word baseline

Issue #3 implements the fixed baseline in `notebooks/03_word_baseline.ipynb`.
It uses the merged notebook 02 helpers. Model and feature code live in notebook 03.

## Current evidence

The first fresh-kernel execution stopped at input preflight. This checkout has no
competition CSVs or private duplicate-audit artifact. The safe failure record is
`results/03_word_baseline/20261110T182052474849Z-preflight-failed.json`.
It records zero fitting rows, zero evaluation rows, and null validation AUROC.
No competition model has run. Do not mark #3 done or use it as a finished dependency.

## Restore inputs and run

Download the competition's five CSVs into ignored `data/raw/`. Keep their original
bytes. Notebook 02 checks them against `configs/data_manifest.json` and the pinned
audit before any fitting. Do not change the manifest or fixed split to pass checks.

Run notebook 01 to regenerate its private duplicate components if they are absent.
Use its matching `duplicate_components.json` at the path named in the pinned audit,
as described in `docs/split-metrics.md`. Check the expected SHA-256 before copying.
Do not invent an empty component file from the public audit summary.

```bash
uv sync --locked
uv run --locked python tools/check_notebooks.py
uv run --locked python tools/check_word_baseline.py
uv run --locked jupyter nbconvert --execute --to notebook --inplace notebooks/03_word_baseline.ipynb
```

The method check uses synthetic text only. It checks training-only vocabulary and
IDF, class-1 probabilities, ID order, serialization, and CSV round trips. It does
not read competition text or save a competition score.

## Successful handoff

The notebook fits lowercase word 1-2 TF-IDF and C1 logistic regression on 8,000
rows. It measures train and validation AUROC, fit/evaluation time, vocabulary size,
iteration count, and the maximum probability difference after reloading.

Each successful run keeps its own model and ID-aligned predictions under ignored
`artifacts/03_word_baseline/<run-id>/`. The stable private pointer
`artifacts/03_word_baseline/latest.json` names those files, their hashes, the split
checksum, and the safe result record. Check these hashes before downstream use.
Load the pipeline with joblib and call notebook 02's `class1_probabilities(model, texts)`.

Only safe aggregate metrics and the inline plot belong in the committed notebook.
The saved JSON records source revision, notebook source hash, configuration,
versions, lock hash, data/split identity, seed, runtime, and artifact hashes.
No upload occurs. A teammate review and successful fresh-kernel run are still
required before completion.
