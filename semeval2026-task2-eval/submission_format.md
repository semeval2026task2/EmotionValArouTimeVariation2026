# Submission format & format-checker instructions

This document describes the required CSV formats for each subtask and how to run the included format checker (`format_checker.py`).

## Overview

There are three subtasks:

- `subtask1` — Longitudinal Affect Assessment (one prediction pair per essay)
- `subtask2a` — Forecast: state change
- `subtask2b` — Forecast: dispositional change

The repo contains template CSVs in the `assets` directory. Use these templates to ensure your submission has the correct set of rows (keys) and column names.

## Required columns

Two categories of required header columns are enforced by the checker:

- Key columns (must be present): used to match rows to the template
- Prediction columns (must be present for checking prediction values)

Key columns (always required)
- subtask1: `user_id`, `text_id`
- subtask2a: `user_id`
- subtask2b: `user_id`

Prediction columns (the checker expects these columns for validating prediction cells)
- subtask1: `user_id`, `text_id`, `pred_valence`, `pred_arousal`
- subtask2a: `user_id`, `pred_forecast_last_valence`, `pred_forecast_last_arousal`
- subtask2b: `user_id`, `pred_dispo_change_valence`, `pred_dispo_change_arousal`

Notes:
- Header names are case-sensitive; column order does not matter.
- For subtask1 the checker enforces both `user_id` and `text_id` as key columns, but the prediction-column list intentionally omits `user_id`.
- Extra columns are allowed but will be reported as warnings.

## Null / missing values

A prediction cell is considered null if the cell value (after trimming) is any of:
- `""` (empty string)
- `NULL` or `null`
- `None` or `none`

Null prediction values in rows required by the template will cause the format check to fail. Nulls in extra rows (rows not present in the template) are ignored (reported as warnings).

## Duplicate and missing rows

- Duplicate keys (same grouping key repeated) will be reported as warnings.
- If your submission is missing rows present in the template, the checker will fail.
- Extra rows (not present in the template) will be reported as warnings.

## Exit codes

- `0` — format check passed (may contain warnings)
- `2` — format check failed (errors printed to stderr)

## How to run the checker

From the repository root (where `format_checker.py` lives):

Basic usage:
```bash
python format_checker.py --task subtask1 --submission path/to/your_submission.csv
```

Specify assets directory (if different):
```bash
python format_checker.py --task subtask2a --submission your_sub2a.csv --assets-dir assets
```

Check the exit code in shell:
```bash
python format_checker.py --task subtask1 --submission subtask1.csv
echo $?   # 0 = pass, 2 = fail
```

## API usage

The format checker can be used programmatically:

```python
from format_checker import run_format_check
rc = run_format_check("subtask1", "path/to/submission.csv", assets_dir="assets")
# rc == 0 -> passed (warnings allowed)
# rc == 2 -> failed
```

You can then call `evaluate_submission` from `eval_interface.py` to run format checking and evaluation together and get a structured result:

```python
from eval_interface import evaluate_submission
res = evaluate_submission(
    task="subtask1",
    submission_path="path/to/sub.csv",
    labels_path="path/to/gold.csv",
    assets_dir="assets",
    dimension="valence",
    return_dict=True,
)
```

If you prefer CLI, follow the instructions in the repo README.

## Example headers

- Valid `subtask1` header (must include key columns):
```
user_id,text_id,text_id,pred_valence,pred_arousal
```
(Explanation: header must include the key columns `user_id,text_id` and the prediction columns `text_id,pred_valence,pred_arousal` — order may vary. Note `text_id` appears once as a key and once as prediction-column name; ensure your header includes the required names.)

- Valid `subtask2a` header:
```
user_id,pred_state_change_valence,pred_state_change_arousal
```

## Troubleshooting

- Ensure files are valid UTF-8 CSVs with a header row.
- Ensure header column names match exactly (case-sensitive).
- Use the appropriate template in `assets/` to verify required rows are present.
