# eval.py — Usage guide

Concise guide for using the evaluation helpers in this repository.

## Requirements

- Python 3.8+
- numpy, scipy

Install (if needed):
```bash
python -m pip install numpy scipy
```

## What this provides

- `task1_correlation(user_ids, text_ids, predictions, labels)`
  - Returns a flat dict with: `r_within`, `p_within`, `r_between`, `p_between`, `r_composite`
  - `r_within`: average of per-user Pearson r (nan if not computable)
  - `p_within`: harmonic-mean combined p-value of per-user tests (None if no p-values)
  - `r_between`: Pearson r across users after averaging predictions/labels per user
  - `r_composite`: Fisher-z composite of within+between

- `task2_correlation(user_ids, predictions, labels)`
  - Returns: `{"r": r, "p": p, "n": n}`
  - If `user_ids` is provided the function averages per-user then computes Pearson across users; if `None` it computes Pearson on flat arrays.

## API usage (examples)

- Use functions directly:

```python
from eval import task1_correlation, task2_correlation

# Subtask 1
res1 = task1_correlation(user_ids, text_ids, preds, labels)

# Subtask 2
res2 = task2_correlation(user_ids, preds, labels)
```

- Use the helper that runs format checking + evaluation:

```python
from eval_interface import evaluate_submission

result = evaluate_submission(
    task="subtask1",
    submission_path="path/to/sub.csv",
    labels_path="path/to/gold.csv",
    assets_dir="assets",
    dimension="valence",
    return_dict=True,
)
# result is a dict: {"status":"ok","metrics":...,"warnings":...}
```

## Notes and interpretation

- Correlations (`r`) are in [-1, 1] or `nan` if not computable.
- `p`-values come from `scipy.stats.pearsonr` when applicable; `p_within` is a harmonic-mean combination.
- `r_composite` uses Fisher's z: atanh-average -> tanh to keep the result in Pearson bounds.
- Inputs may be Python lists or numpy arrays; functions use numpy-aware masking for NaNs.

## Troubleshooting

- Many `nan` results often indicate:
  - users with < 2 observations (no per-user Pearson)
  - constant predictions or labels (zero variance)
- To debug, inspect per-user counts or print per-user correlations (task1 returns per-user data inside the dict).

## Further resources

- See `README.md` for CLI usage of `format_checker.py` and `eval_interface.py` and examples for running in batch or producing JSON output.
