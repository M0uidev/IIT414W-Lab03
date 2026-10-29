# Common AI recommendation audit

Respond in at most five short lines to the recommendation quoted in the brief.
Accept/reject, methodological reason, and a precise checkable cell/function/output in this repository:

Reject. If 2026 results pick the forest setting and the threshold, 2026 stops being an independent test, because it has already been used to make choices, so its score would be optimistic.
The training years ending in 2021 do not fix this: what matters is which data the choices were tuned on, not the training dates.
In our repo every choice is made on dev only: `evaluate_scores` (`lab03_support_v3.py`, line 112) calls `choose_threshold(dev_scores, dev, ...)`, and `load_learning` (line 49) only accepts `train`/`development` partitions.
`outputs/run_manifest_v3.json` records `"threshold_selection": "dev only; reused unchanged on train"`, and `data/manifest_lab03_v3.json` lists 2026 data as excluded.
A fair 2026 check would freeze `forest_sqrt__min_samples_leaf_100` and threshold 0.602 first, then score 2026 once without changing anything.

## Truthful use / no-use record

Tool and use, or “No AI used for this lab”:

If used, one actual suggestion (quote or faithful summary):
What we accepted/rejected:
Exact check performed and repository evidence:
One limitation relevant to this work:

Do not invent an error or interaction. No minimum number of prompts is required.

## Contributions

- Matías Mouat: set up the Python 3.11 environment and README run steps, wrote “1. Define the prediction” and “2. Explain the common comparison”, wrote and committed `experiment_spec.md` before the first candidate run, set the `extra-config` cell and wrote “4. Explain your additional result”.
- María José López: ran the section 5 queries (`context-query`, `context-query-circuit19`, `event-query-fresh-tyres`, `event-query`), wrote the three entries in “Your three entries”, wrote `memo.md` and the common audit above, and checked that memo numbers match `comparison_table.md`.
