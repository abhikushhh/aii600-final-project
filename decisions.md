# Decisions

This file is the history of the project. Append an entry when a choice changes the work: the quantity, the data, the split, the model, the loss, or the action. Leave old entries in place. A later entry can reverse an earlier one. If a result depends on a random draw, record the seed under Why. The split entry records the cutoff date, or the seed and the fraction. The pull request that merges the code names this entry.

## YYYY-MM-DD: short title

- Decision. What you chose.
- Why. The evidence.
- Alternative. What you rejected.
- Revisit. What would change the choice.

## 2026-11-18: Part 1 dataset

- Decision. I recorded 20 one-minute clips (C01–C20) of parked cars in retail parking lots on 2026-11-16. For each clip I reviewed 12 stills (one every 5 seconds, 0–55 s) in `protocol/review-timer.html` and timed myself, leaving out interruptions. I did not collect car counts. `clip-log.csv` and the blurred frames are on the `data` release. The raw videos stay off GitHub.
- Why. The raw videos show readable license plates. The blurred stills are exactly what I reviewed and timed.
- Alternative. Publishing the raw videos (rejected for privacy). Recording per-frame car counts (dropped; I didn't collect them).
- Revisit. If a plate or face is still readable in a frame, re-blur it or use the spare clip, and update the hashes. If a teammate has time to review the clips too, time them again to see how much reviewers differ.

## 2026-11-18: Clarity rated after timing

- Decision. I rated each clip's clarity on 2026-11-18: clear = C04, C09, C13, C15, C17, C20; very unclear = C07, C14; the other 12 moderately unclear.
- Why. I rated them myself, after looking up online how long it would take a human being to look at a blur vs clear image. My ratings were similar those on all 20 clips.
- Alternative. Rating clarity before timing.
- Revisit. If there's time, a teammate rates the 20 clips blind and we compare.

## 2026-11-18: Sessions by a 5-minute gap

- Decision. A new session starts when a clip begins more than 5 minutes after the previous one ended: S01 = C01–C02, S02 = C03–C20.
- Why. Clips from one session share lighting and parking lots, so they shouldn't be split between training and testing.
- Alternative. One session per pair of clips I filmed at the same time on two phones (finer and more balanced); I didn't use it for Part 1.
- Revisit. Part 2 can use a finer split, but each pair filmed together (C10/C11, C12/C13, C14/C15, C16/C17, C18/C19) has to stay on the same side.

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

## 2026-11-26: Business loss assumptions for Part 3

- Decision. For the business analysis, use a scenario labor rate of $30 per reviewer-hour. Measure decision loss as absolute timing error converted to labor cost, with underestimation weighted 1.5 times and overestimation weighted 1.0 times. Test sensitivity at $20, $30, and $45 per hour and underestimation multipliers of 1.0, 1.5, and 2.0.
- Why. The project needs a loss in the units of the decision, not only MAE. Underestimating review work can create rush/overtime pressure, so the base scenario makes that mistake more costly. These are explicit planning assumptions rather than claims about a specific customer's wage or overtime policy. On the five held-out clips, the clarity model has lower business loss than the baseline in every tested scenario.
- Alternative. Treat every second of under- and overestimation as equally costly and report only MAE. Rejected because it does not represent the stated business concern that underestimating workload can be more disruptive.
- Revisit. Replace the scenario rates and multipliers with a real customer's wage, overtime, missed-deadline, and idle-capacity costs if those data become available.

## 2026-11-26: Business action from the clarity model

- Decision. For clip-level staffing and scheduling on footage similar to this sample, use the clarity model rather than the one-mean baseline. Under the base asymmetric loss, schedule to the model prediction plus an approximately 2.1-second buffer, the 60th percentile implied by an underestimation cost of 1.5 versus an overestimation cost of 1.0. Do not claim that the model already improves total batch quoting.
- Why. Held-out MAE is 4.93 s for the clarity model versus 12.92 s for the baseline. Under the base business assumptions, total loss across the five held-out clips is about $0.271 for the model versus $0.688 for the baseline, a reduction of about 61%. The model also has less total underestimation error and less total overestimation error on this test set, so the preferred method does not change across the tested sensitivity scenarios. However, both methods estimate about 352 seconds for the five-clip batch versus 359 seconds actual, so the evidence is specifically about better per-clip allocation rather than better total-batch cost.
- Alternative. Continue using the 70.40-second training mean for every clip. Rejected for clip-level scheduling because it is substantially less accurate on the held-out clips and has higher decision loss under all tested scenarios.
- Revisit. Rerun the action decision if a blind clarity re-rating changes the labels, if a larger held-out batch no longer shows the model advantage, or if real business cost data imply a materially different loss function.
## 2026-11-27: Clarify split fraction and evaluation boundary

- Decision. Document the fixed Part 2 split as 15 training clips and 5 held-out clips, i.e. 75% train and 25% test. No random seed was used because the split was selected by a fixed hand-defined rule that kept simultaneous pairs together and represented all three clarity levels in the test set. Also record that the clarity model has lower absolute error on four of the five held-out clips, while the mean baseline is better on C16; the two methods are nearly tied on the total five-clip batch estimate.
- Why. The final checklist asks for the split fraction and for a statement of where the method wins and where it does not. This entry clarifies those facts without rewriting the older Part 2 decision.
- Alternative. Rewrite the 2026-11-25 split entry. Rejected because `decisions.md` is a history and old entries should remain unchanged.
- Revisit. Replace this clarification if a larger dataset leads to a seeded random split or a different held-out evaluation.
