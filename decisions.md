# Decisions

This file is the history of the project. Append an entry when a choice changes the work: the quantity, the data, the split, the model, the loss, or the action. Leave old entries in place. A later entry can reverse an earlier one. If a result depends on a random draw, record the seed under Why. The split entry records the cutoff date, or the seed and the fraction. The pull request that merges the code names this entry.

## YYYY-MM-DD: short title

- Decision. What you chose.
- Why. The evidence.
- Alternative. What you rejected.
- Revisit. What would change the choice.

## 2026-11-25: Train/test split for Part 2

- Decision. Held out 5 of the 20 clips as a test set: C03, C07, C16, C17, C20. The other 15 clips are training. The split is fixed by hand, not drawn with a seed.
- Why. The two time-gap sessions in `data/README.md` (S01 = C01-C02, S02 = C03-C20) are too unbalanced (2 vs 18) to hold out a session. That entry allows a finer split in Part 2, as long as each of the five simultaneous two-phone pairs (C10/C11, C12/C13, C14/C15, C16/C17, C18/C19) stays on one side. C16/C17 is the one pair sent to test, kept whole; the other four pairs stay in train, including C14/C15, so the "very unclear" category is not reduced to zero training rows. The three singles (C03, C07, C20) were chosen so the test set keeps all three clarity labels (2 clear, 2 moderately unclear, 1 very unclear) instead of leaving that to chance with only 20 clips to draw from.
- Alternative. A random draw with a fixed seed, constrained to keep pairs intact. Rejected because, with only 2 "very unclear" clips total, several candidate seeds either emptied that category from train or from test; hand-picking one split and stating the criteria seemed more honest than reporting the first seed that happened to work.
- Revisit. If the team collects more clips, especially more "very unclear" ones, redo this as a seeded random split over the enlarged set.

## 2026-11-25: Baseline, model, and loss for Part 2

- Decision. Baseline: predict the training-set mean review time (70.40 s) for every clip. Model: simple linear regression of `review_time_sec_measured` on an ordinal `clarity_score` (clear=1, moderately unclear=2, very unclear=3), fit on the 15 training clips. Loss/metric: mean absolute error (MAE) in seconds, scored on the 5 held-out clips, which is the unit the staffing decision uses.
- Why. MAE baseline = 12.92 s; MAE model = 4.93 s. A 20,000-draw bootstrap over the 5 test clips gives a 90% interval for (model MAE - baseline MAE) of about [-13.97, -2.48] seconds, entirely below 0 on this test set. A simulation check (simulate from the fitted b0, b1, residual sd; refit 2000 times) recovers the fitted slope and intercept, so the fitting procedure itself is not the source of the error.
- Alternative. A model using the two dummy variables for the 3-level category instead of an ordinal score (rejected: one more parameter than the 15 training rows comfortably support, and the "very unclear" category has only 1 training row either way). Using `review_time_sec_simulated` to test the hypothesis (rejected: `data/README.md` says that column assumes the hypothesis and must not be used to test it).
- Revisit. The clarity label itself may not be independent evidence: per the Part 1 "Clarity rated after timing" entry, ratings were assigned after timing and matched an AI's preliminary rating on all 20 clips, not rated blind beforehand as the protocol specifies. If a blind re-rating (already proposed in that entry) changes the clarity labels, this split, baseline, and model should be rerun against the new labels.
