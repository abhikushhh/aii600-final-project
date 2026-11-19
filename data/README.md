# Data

The data files are not committed to git. They are assets on the public GitHub release tagged `data` on this fork, `abhikushhh/aii600-final-project`. The notebook reads a local copy from `data/`.

## Summary

- **Source.** Original video recorded by the project team for this course: 21 clips filmed on 2026-11-16 between 17:38 and 18:11 (UTC−05:00) on two phones, in outdoor retail parking lots. Not taken from a public dataset, Kaggle, or a scraped site. The raw videos are **not** published (they contain readable license plates). What is published is a clip-level table and the 12 sampled still frames per clip, with license plates blurred.
- **Terms.** The team owns the recordings and allows the derived table and the plate-blurred frames to be republished on this release for the course. The raw videos are not republished. Reuse outside the course needs the team's permission.
- **Unit of observation.** One ~60-second clip of parked civilian passenger cars (`C01`–`C20`), reviewed at 12 stills: 0, 5, 10, …, 55 s.
- **Sample size.** 20 clips (240 frames). One reviewer.
- **Time span.** One evening: 2026-11-16, 17:38–18:11 (dusk and night lighting only). Review dates: 2026-11-17 (C01–C09) and 2026-11-18 (C10–C20).

## Files

| File on the `data` release | What it is | SHA-256 |
| --- | --- | --- |
| `clip-log.csv` | 20 rows, one per clip: IDs, session, clarity, review times | `04f9a869dd29f868da53fc15173f7762b03343dfbd1cb16932f6e9a1464b4827` |
| `frames.zip` | 240 plate-blurred JPGs, `frames/C01/C01_t00.jpg` … `frames/C20/C20_t55.jpg` (720×1280, 17.6 MB) | `0f47aff1824cdd28ed2a6ba083fc4501a3d6b08950b6d939a771af4591411c45` |

Download them into this folder from the project root:

```bash
gh repo set-default abhikushhh/aii600-final-project
gh release download data --dir data --repo abhikushhh/aii600-final-project
cd data && unzip -o frames.zip && cd ..
shasum -a 256 data/clip-log.csv data/frames.zip
```

Without the GitHub CLI, open the repository's **Releases** page, open the release **Data**, and download both files into `data/`.

When a file changes, upload it again and update its hash in this file in the same commit:

```bash
gh release upload data data/clip-log.csv --repo abhikushhh/aii600-final-project --clobber
shasum -a 256 data/clip-log.csv
```

## `clip-log.csv` columns

| Column | Meaning |
| --- | --- |
| `Clip ID` | `C01`–`C20`, in order of recording start |
| `Session ID` | `S01` (C01–C02) or `S02` (C03–C20). A new session starts after a gap of more than 5 minutes |
| `Source file` | Original phone file name (not published) |
| `Recorded at` | Recording start, ISO 8601 with offset |
| `Clarity` | `clear`, `moderately unclear`, or `very unclear`, assigned by Abhimanyu Kushwaha on 2026-11-18, after timing (see "Provenance") |
| `review_time_sec_measured` | Seconds the reviewer spent reviewing the clip's 12 stills, measured with the review timer, excluding interruptions |
| `review_time_sec_simulated` | **Not a measurement.** A literature-based planning estimate (see below). Do not use it to test the hypothesis |
| `Interruption sec` | Seconds paused for interruptions (0 for every clip) |
| `Notes` | Free-text notes; blank for every clip in this release |
| `Review date` | Date of the timed review |
| `Reviewer` | Who did the timed review (one person for all clips) |

Empty cells mean "not measured", not zero. Car counts were not collected, so the table has no count columns.

## How the data were collected

1. **Recording.** Two people walked the same lots with two phones at the same time. Files were sorted by recording start; the first 20 became `C01`–`C20`; the 21st (`IMG_1382.MOV`) is a spare and is not in the dataset.
2. **Frames.** The still at each of 0, 5, …, 55 s was saved as a JPG. Every frame went through an automatic license-plate detector (YOLOv9 plate model from `open-image-models`, via `fast-alpr`, confidence ≥ 0.2); each detected plate was pixelated and blurred (137 plates across 21 clips). Plate text was not stored.
3. **Timing.** One reviewer, Abhimanyu Kushwaha, reviewed the 12 stills of each clip in `protocol/review-timer.html` on 2026-11-17 (C01–C09) and 2026-11-18 (C10–C20). Pauses for interruptions are logged separately and excluded.
4. **Clarity.** Abhimanyu Kushwaha assigned one of the three labels defined in `protocol/review-protocol.md` to each clip on 2026-11-18.
5. **Counts.** Car counts were not collected for this dataset. `protocol/counting-rule.md` is kept as the written rule for the review task.

### Provenance

- **Review times** were measured by Abhimanyu Kushwaha.
- **Clarity ratings** were assigned by Abhimanyu Kushwaha on 18 November 2026, *after* the review times had been measured and *after* he had seen preliminary AI-generated clarity ratings in the working spreadsheet. His ratings match those preliminary ratings on all 20 clips. This deviates from the protocol, which says to rate clarity *before* timing. The ratings were therefore not blind to the AI labels or to the timing experience, and they may be anchored on the AI labels.
- **AI use.** An AI assistant (Cursor) was used to extract the frames, blur license plates, and draft the documentation (this file, the counting rule, the review protocol, and the review timer page). It also made the preliminary clarity ratings.

### Clip-to-file mapping

| Clip | File | Recorded at (−05:00) | Duration s | Session |
| --- | --- | --- | --- | --- |
| C01 | IMG_3093.MOV | 17:38:53 | 65.1 | S01 |
| C02 | IMG_3094.MOV | 17:40:04 | 59.8 | S01 |
| C03 | IMG_3095.MOV | 17:49:37 | 60.5 | S02 |
| C04 | IMG_3096.MOV | 17:51:04 | 60.8 | S02 |
| C05 | IMG_1373.MOV | 17:51:13 | 61.3 | S02 |
| C06 | IMG_3097.MOV | 17:52:34 | 71.3 | S02 |
| C07 | IMG_3098.MOV | 17:57:51 | 65.7 | S02 |
| C08 | IMG_3105.MOV | 17:59:15 | 65.0 | S02 |
| C09 | IMG_3106.MOV | 18:00:29 | 63.2 | S02 |
| C10 | IMG_1377.MOV | 18:00:58 | 82.9 | S02 |
| C11 | IMG_3099.MOV | 18:00:58 | 83.6 | S02 |
| C12 | IMG_1378.MOV | 18:02:47 | 64.1 | S02 |
| C13 | IMG_3100.MOV | 18:02:47 | 61.4 | S02 |
| C14 | IMG_1379.MOV | 18:04:11 | 68.9 | S02 |
| C15 | IMG_3101.MOV | 18:04:11 | 74.5 | S02 |
| C16 | IMG_1380.MOV | 18:06:46 | 67.2 | S02 |
| C17 | IMG_3102.MOV | 18:06:46 | 63.3 | S02 |
| C18 | IMG_3103.MOV | 18:08:23 | 74.7 | S02 |
| C19 | IMG_1381.MOV | 18:08:24 | 73.1 | S02 |
| C20 | IMG_3104.MOV | 18:10:26 | 62.7 | S02 |

`IMG_3105` and `IMG_3106` have no Apple metadata (1080×1920 exports), so their container `creation_time` was used. Five pairs started in the same second on the two phones (C10/C11, C12/C13, C14/C15, C16/C17, C18/C19). They show different views of the same lots at the same moment, so each pair must stay on the same side of the train/test split.

## How the measurement differs from what the decision needs

The decision needs reviewer time per unseen one-minute clip for a batch of similar footage. The dataset measures something narrower:

- **Bias (too low).** The timed task is reviewing 12 pre-extracted stills in a web page. It leaves out finding files, seeking in video, and the clarity preview. A real review job would take longer.
- **Bias (one person).** One reviewer, who reviewed clips in ID order, so practice effects and personal speed are built in. Another reviewer could be faster or slower.
- **Bias (clarity labels).** Clarity was rated after timing and after seeing the AI's preliminary ratings, and it matches them on every clip. A rater who knows how long a clip took may call slow clips "unclear", which would make the clarity–time link look stronger than it is.
- **Bias (scope).** One evening, dusk and night only, retail lots only. Daylight, rain, or other scene types are not covered.
- **Noise.** n = 20 clips, 2 of them `very unclear`; clip-to-clip variation in time is large relative to the sample.

## Sessions and the split

Sessions use a time-gap rule: S01 = C01–C02 and S02 = C03–C20. That split is unbalanced (2 vs 18). For the planned ~15 train / 5 test split, keep each simultaneous pair together. The split itself, with its seed or cutoff, is recorded in `decisions.md`.

## Simulated review time (`review_time_sec_simulated`), not a measurement

A planning estimate for a dry run of the cost analysis, made before measured times existed. It assumes the hypothesis (a clarity multiplier), so it must not be used to test it. Its *n* values were the preliminary AI-assisted frame counts, which are not part of this dataset. Per frame with *n* cars and clarity multiplier *k* (`clear` 1.00, `moderately unclear` 1.25, `very unclear` 1.50, an assumption): search time *k*·(2.4 + 0.9·(*n* − 1)) s if *n* ≥ 1, else *k*·1.0 s; plus entry time 1.35 + 0.28·(digits(*n*) + 1) s. Per clip: the sum over 12 frames plus 1.35 + 0.28·(characters in the median + 1) s, rounded. Sources: Bearman et al., *What's the Point*, ECCV 2016 ([arXiv:1506.02106](https://arxiv.org/abs/1506.02106)); Card, Moran & Newell, Keystroke-Level Model (1980, 1983); Trick & Pylyshyn, *Psychological Review* 101(1), 1994.

## Privacy

A clip is used only if it has no identifiable people, no readable license plates, and no workplace material. The raw videos fail the plate test, so they stay off GitHub; the published frames are plate-blurred. No recognizable faces were found in the sampled frames; distant, unidentifiable figures appear in C07, C09, C12, and C20, and a vehicle occupant is visible in C10 at 20 s. The scenes are public retail lots.
