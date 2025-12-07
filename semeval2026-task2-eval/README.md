# Evaluation interface and format checker

This repository contains simple scripts for the SemEval task evaluation and submission format checking.

## Quick start (CLI)

Install dependencies (for evaluation):

```bash
python -m pip install numpy scipy
```

Run the format check only:

```bash
python format_checker.py --task subtask1 --submission path/to/submission.csv [--assets-dir assets]
# assets directory defaults to "assets". "assets" directory contains templates for submission files (user_ids and text_ids will be updated in the template during the evaluation phase.
```

Run full evaluation (one dimension per run):

```bash
python eval_interface.py --task subtask1 --submission path/to/submission.csv --labels path/to/gold.csv --dimension valence [--assets-dir assets]
# assets directory defaults to "assets"
```

To write JSON output (optional flag shown in brackets):

```bash
python eval_interface.py --task subtask1 --submission sub.csv --labels gold.csv --dimension valence [--json out.json] [--assets-dir assets]
# --json is optional; --assets-dir defaults to "assets"
```

## API usage (importable)

All scripts expose importable functions so you can call them from Python code and receive structured results instead of using the CLI.

- format_checker

```python
from format_checker import run_format_check
rc = run_format_check("subtask1", "path/to/submission.csv", assets_dir="assets")
# rc == 0 -> passed (warnings allowed)
# rc == 2 -> failed
```

- eval_interface

```python
from eval_interface import evaluate_submission
result = evaluate_submission(
    task="subtask1",
    submission_path="path/to/sub.csv",
    labels_path="path/to/gold.csv",
    assets_dir="assets",
    dimension="valence",
    return_dict=True,   # returns structured dict instead of printing/exiting
)
# result is a dict: {'status': 'ok', 'task': ..., 'dimension': ..., 'metrics': {...}, 'warnings': [...]}
```

Notes:
- `evaluate_submission(..., return_dict=True)` returns a dict and does not exit the process — useful for programmatic evaluation across many submissions.
- `eval_interface` computes metrics for one dimension at a time (valence or arousal); call it twice to compute both.

## Files

- `format_checker.py` — CLI and importable function `run_format_check(task, submission_path, assets_dir)` that validates submission CSV against the template in `assets/`. See `format_checker.py` header for usage.

- `eval.py` — importable evaluation functions:
  - `task1_correlation(user_ids, text_ids, predictions, labels)` — returns flat dict with within-person, between-person and composite correlations.
  - `task2_correlation(user_ids, predictions, labels)` — between-person Pearson r or flat Pearson when `user_ids` is `None`.

- `eval_interface.py` — ties the format checker and evaluation functions. It runs the format check, loads submission and label CSVs, computes metric for one dimension (valence or arousal), and prints or writes JSON. Use `evaluate_submission(..., return_dict=True)` for programmatic use.

Each file has a small header docstring describing its use.

---

For more details, see the header of each Python file.
