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
