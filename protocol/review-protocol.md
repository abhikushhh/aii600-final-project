# Review protocol (Part 1)

One reviewer (Abhi Kush) rates all 20 clips with this procedure and `counting-rule.md`. Do not split clips across reviewers. Do not start the review timer until clarity is recorded.

## IDs

| Field | Rule |
| --- | --- |
| **Clip ID** | `C01`–`C20`. One row per clip. Use the ID on the file, not a guess. |
| **Session ID** | `S01`, `S02`, … Clips filmed in the same sit-down / same outing share an ID so Part 2 can keep them in the same train/test split. **Leave blank until Abhi assigns groups.** Do not invent sessions. |

## Setup (once)

1. Print or keep open `counting-rule.md` and `clip-log-template.csv`.
2. Confirm each source file maps to `C01`–`C20` and is ~60 s.
3. Use the same player, same screen, same viewing distance for all clips.
4. Use a stopwatch you can pause. Review time is **counting + data entry only**.
5. Work in one pass per clip (clarity, then timed count). Do not pre-count.

## Per clip

### A. Open and identify

Open the clip. Write **Clip ID**. Write **Session ID** only if already assigned; otherwise leave blank. Write **Review date** (`YYYY-MM-DD`) and **Reviewer** (`Abhi Kush`).

### B. Rate clarity **before** any timed counting

Scrub or step through the 12 sample times (0, 5, …, 55 s) **without enumerating cars**. Judge how hard the **typical** sampled frame is to count. Write **Clarity** using **exactly** one of the three labels below.

Then stop previewing. Do not count yet.

| Label (write this string) | Operational definition |
| --- | --- |
| `clear` | In a typical sample frame, parked passenger cars separate from background at a glance. Edges are distinct. Light is usable (not blown out or too dark). Occlusion/clutter does not force extra scrutiny for most cars. Second looks are rare. |
| `moderately unclear` | Counting needs extra attention. Typical causes: mixed shadow/glare, moderate occlusion, small/distant cars, mild blur or compression, cars packed so boundaries take work. Most objects can still be classified as car vs not **without guessing**. |
| `very unclear` | A substantial share of candidates need guesswork or fail the counting rule. Typical causes: severe dark, rain/fog, hard glare, heavy occlusion, extreme distance, or poor focus. “Do not count if uncertain” will be used often. |

If frames differ, rate the **majority / typical** difficulty, not the single worst frame. Put “mixed: …” in Notes after timing (Notes are not timed as a separate essay; a short note is part of data entry).

Clarity is about **countability**, not plate readability. Plates must remain unreadable for privacy.

### C. Time counting + data entry

1. Reset the stopwatch. Confirm Clarity is already filled.
2. **Start** the stopwatch.
3. At each of **0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55 s**, pause the **video** (not the stopwatch), count parked civilian passenger cars under `counting-rule.md`, and enter that integer in the matching `Count *s` column.
4. Compute **Car count** = median of the 12 integers (mean of 6th and 7th when sorted). Enter it.
5. Enter a short **Notes** value if needed (close calls, skipped timestamps, mixed clarity).
6. **Stop** the stopwatch.
7. Write **Review time seconds** as whole seconds on the stopwatch (**excludes** interruptions; see below).

Do not include: file hunting, player setup, clarity preview, or writing Session ID later.

### D. Interruptions (record separately)

If attention leaves the task (phone, conversation, leaving the seat, unrelated app):

1. **Pause** the stopwatch immediately.
2. Add the paused duration to **Interruption seconds** (running total for that clip). If none, leave blank or `0`.
3. Resume the stopwatch and continue from the frame you left. Do not re-count finished frames.

If you **lost your place** (forgot which frames were done or which cars were counted in the current still):

1. Pause the stopwatch. Add that pause to **Interruption seconds**.
2. Discard the partial **Review time seconds** for this clip (do not save a half-time).
3. Keep the **Clarity** already rated (do not re-rate unless the first rating was a slip of the finger).
4. Restart timed counting from step C.1. In Notes write `restart after lost place`.

**Review time seconds** never includes interruption time. Do not “make up” lost time. Do not invent times.

## Order and completeness

- Review `C01` through `C20` in ID order unless a file is missing; then skip, note, and return.
- Same reviewer for every clip.
- Do not discuss counts with teammates until the log is filled (single-rater dataset).
- Do not fill **Review time seconds**, **Car count**, or frame counts from memory or estimates. If a clip was not timed, leave those cells empty.

## After all 20

Spot-check that Clarity used only the three allowed strings, Session IDs are blank or a consistent `S0k`, and no clip has review time without frame counts. Copy interruption handling into `data-readme-draft.md` only as the method, not as fake numbers.
