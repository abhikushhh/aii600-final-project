# Data

The data files are not committed to git. They are assets on the public GitHub release tagged `data` on this fork, `abhikushhh/aii600-final-project`. The notebook reads a local copy from `data/`.

## Summary

- **Source.** Original video recorded by the project team for this course: 21 clips filmed on 2026-11-16 between 17:38 and 18:11 (UTC−05:00) on two phones, in outdoor retail parking lots.
- **Terms.** The team owns the recordings and allows the derived table and plate-blurred sampled frames to be republished for the course. Raw videos are not republished because they contain readable license plates.
- **Unit of observation.** One ~60-second clip of parked civilian passenger cars (`C01`–`C20`), reviewed at 12 stills: 0, 5, 10, …, 55 s.
- **Sample size.** 20 clips (240 sampled frames). One reviewer.
- **Time span.** One evening: 2026-11-16, 17:38–18:11. Timed reviews were completed on 2026-11-17 and 2026-11-18.

## Release files

| File | What it is | SHA-256 |
| --- | --- | --- |
| `clip-log.csv` | 20 clip rows: identifiers, session, clarity, measured review time, planning fields, and preliminary AI-assisted count fields | `04f9a869dd29f868da53fc15173f7762b03343dfbd1cb16932f6e9a1464b4827` |
| `frames.zip` | 240 plate-blurred JPGs under `frames/C01/…` through `frames/C20/…` | `0f47aff1824cdd28ed2a6ba083fc4501a3d6b08950b6d939a771af4591411c45` |

Download from the project root:

```bash
gh release download data --dir data --repo abhikushhh/aii600-final-project
```

Without GitHub CLI, open the repository's **Releases** page, open the release tagged **data**, and download the files into `data/`.

Verify hashes:

```bash
shasum -a 256 data/clip-log.csv data/frames.zip
```

## Important columns

| Column | Meaning |
| --- | --- |
| `Clip ID` | `C01`–`C20` |
| `Session ID` | `S01` or `S02` |
| `Recorded at` | Recording start timestamp |
| `Clarity` | `clear`, `moderately unclear`, or `very unclear` |
| `review_time_sec_measured` | Human timed review seconds; this is the outcome used for the hypothesis test |
| `review_time_sec_simulated` | Planning estimate only; it assumes the hypothesis and is **not** used to test it |
| `t00` … `t55`, `Car count median` | Preliminary AI-assisted count fields from the working table; they are **not human measurements and are not used in the Part 2 model or held-out test** |
| `Interruption sec` | Paused interruption time, excluded from measured review time |
| `Notes` | Provenance / close-call notes |

Empty cells mean "not measured", not zero.

## How the data were collected

1. **Recording.** Two people recorded the parking-lot footage on two phones. The first 20 clips in recording order became `C01`–`C20`; the 21st is a spare.
2. **Frames.** Stills were sampled at 0, 5, …, 55 seconds. License plates in the published sampled frames were blurred automatically; plate text was not stored.
3. **Timing.** One reviewer reviewed the 12 sampled frames per clip and timed the review task. Interruptions were logged separately and excluded from review time.
4. **Clarity.** Clarity used three labels: clear, moderately unclear, very unclear.
5. **Preliminary AI-assisted counts.** The released working table contains AI-assisted per-frame count fields. These are retained for provenance only and are not used to test the clarity/review-time hypothesis.

## Provenance and limitations

- Review times are human measurements.
- Clarity was assigned **after** timing and after preliminary AI-generated ratings had been seen. That deviates from the intended blind protocol and can bias the clarity–time relationship upward.
- One reviewer performed all timed reviews.
- The footage covers one evening, retail parking lots, and dusk/night lighting.
- Only two clips are `very unclear`.
- Reviewing pre-extracted stills omits file handling and video seeking, so real production work may take longer.

## Split constraints

The time-gap sessions are S01 = C01–C02 and S02 = C03–C20. For model evaluation, simultaneous two-phone pairs are kept together. The final held-out split is documented in `decisions.md`.

## Privacy

Raw videos remain off GitHub because license plates are readable. Published sampled frames are plate-blurred. The data are limited to public retail parking-lot scenes and are used only for this course project.
