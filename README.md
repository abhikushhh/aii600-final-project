# AII 600 Final Project

## Project

**Image Clarity for Review-Time Planning**

We test whether image clarity predicts the time needed to review one-minute clips of parked civilian passenger cars more accurately than using one average review time for every clip. The business decision is how much reviewer time to schedule for similar footage.

## Team

- Abhimanyu Kushwaha - @abhikushhh
- Tariq Shinwari - @Tariqshinwar
- David - @marscandothis555-cmyk

## Main result

On five held-out clips:

- Mean-time baseline MAE: **12.92 seconds**
- Clarity-model MAE: **4.93 seconds**
- Reduction in absolute prediction error: about **62%**

Under the Part 3 base business scenario ($30/hour, with underestimation weighted 1.5x more than overestimation), the clarity model reduced decision loss from about **$0.688 to $0.271** across the five held-out clips.

The recommended use is **clip-level staffing and scheduling for similar footage**, not a claim that the model improves total quotes for every possible batch.

## Repository map

- `PROPOSAL.md` - original project proposal
- `analysis.ipynb` - data checks, split, baseline, model, uncertainty, held-out evaluation, and business decision analysis
- `decisions.md` - chronological decision history
- `presentation.qmd` / `presentation.html` - final title slide + Action / Reason / Risk / Value presentation
- `fig/` - saved figures, including the layer diagram
- `data/README.md` - data provenance, release files, hashes, and download instructions
- `protocol/` - review/counting procedure used for data collection

## AI disclosure

AI assistants were used in this project. **Cursor** was used for frame extraction, license-plate blurring, documentation drafting, and preliminary clarity-rating assistance. **ChatGPT** was used for Part 3 business-loss analysis, presentation drafting, and repository/checklist review. The team reviewed the work and is responsible for everything committed to the repository.

