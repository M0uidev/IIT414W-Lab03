# Expectation for one additional candidate

The five base results are supplied. This expectation concerns YOUR additional run.

- Base model: `forest_sqrt` (the best base system on dev: 140 / 370 events caught with 945 alerts).
- Parameter and old → new value (one allowed tuple): `min_samples_leaf` 30 → 100.
- Conditions held fixed: same CSV (hash checked by `load_learning`), train 2018–2021, dev = first 11 rounds of 2022, seed 414, the nine `FEATURES`, same preprocessing fitted on train only, `n_estimators=150`, `max_depth=6`, `max_features='sqrt'`, `class_weight='balanced_subsample'`. Same threshold rule on dev (max 10% of windows alerted, maximise events caught, then precision, then threshold). The threshold is picked again for the candidate, so it can be a different number from the parent's 0.608.
- Have you already run this additional candidate? No. We wrote this before the first run. The base comparison was reproduced first (it matches the supplied table), but the candidate has not been fitted yet.
- Expected effect and mechanism, written before the first additional run:
  With `max_depth=6` each tree has at most 64 leaves and about 63k training rows, so most leaves already hold far more than 100 rows. The new limit should only bite on small, specific leaves, for example a split on one circuit's one-hot column or a short tyre-life range. Those small leaves are where a tree can memorise 2018–2021 details that may not repeat in 2022. So we expect:
  1. Train event recall goes down a little from 0.520 (less in-sample fitting).
  2. Dev event recall stays close to the parent's 140 / 370 (0.378). Our guess is within about ±10 events, with a small chance of a gain if the small leaves were overfitting.
  3. Dev precision stays near 0.36. The alert count stays close to the 945 budget cap.
  We think the change is too small to move the result a lot. If dev drops clearly, that would mean the small leaves were capturing real patterns (for example circuit-specific pit timing) and not just noise.
- Other trials already made, if any, and how the final candidate was chosen: None. We did not run the other two tuples. We chose this one because `forest_sqrt` is the strongest base system and a bigger leaf size is the most direct test of whether its small leaves help or hurt on 2022. Changing `max_depth` to 3 felt like a much bigger change, harder to explain with one mechanism.

Keep this record after running, even if wrong. Explain actual results in “4. Explain your additional result”.
Do not rewrite an expectation as if it predicted a result already seen.
