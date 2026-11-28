# Checklist

Tick every line that the pushed `main` covers. A line you cannot tick needs one sentence saying why.

## 1. Question

- [x] The question is one sentence, then one quantity with units and a time window.
- [x] The decision is named, and the loss or profit is a formula. The costlier mistake is named.
- [x] A layer diagram: data, model, prediction, decision.

## 2. Data

- [x] Source, unit of observation, sample size, time span, and how it was collected.
- [x] How the measurement differs from the quantity the decision needs, and whether that gap is bias or noise.
- [x] One plot of the raw data and one table of summary statistics, before any model.

## 3. Model

- [x] The model as equations. Each parameter in words, and the mechanism it stands for.
- [x] The assumptions, and the one you trust least.
- [x] Simulated data from the model are checked against the fitted parameters; the refit simulation recovers the intercept and slope.

## 4. Uncertainty

- [x] Model predictions carry approximate 90% prediction intervals.
- [x] Error is measured out of sample, and the notebook explains that uncertainty grows at sparsely represented clarity levels.
- [x] Residuals are plotted and discussed as noise versus bias.

## 5. Decision

- [x] An explicit prediction-to-action rule is given, and the asymmetric loss explains the planning buffer.
- [x] The preferred action is tested across hourly rates and underestimation penalties.
- [x] The value of being less wrong is reported in dollars under clearly labeled scenario assumptions.

## 6. Evaluation

- [x] A held-out set the model never saw is used, with prediction-interval coverage reported as a limited calibration check.
- [x] The method is scored against a simple baseline in seconds and in business-loss units.
- [x] The clarity model has lower absolute error on 4 of 5 held-out clips; the baseline is better on C16. The two methods are nearly tied on the total five-clip batch estimate.

## Decisions

- [x] `decisions.md` preserves Part 1, Part 2, and Part 3 history.

## 7. Communicate

- [x] `presentation.html` is a title slide plus Action, Reason, Risk, and Value, rendered from `presentation.qmd`.
- [x] Key effects are stated in plain language and real units.
- [x] Limits are stated: small sample, one reviewer, narrow scene/time range, sparse very-unclear category, and non-blind clarity ratings.

## Repository

- [x] Names and GitHub usernames are in `README.md`.
- [x] The group used pull requests for Parts 2 and 3; the remaining Part 1 documentation is restored in the final cleanup commit.
- [x] `requirements.txt` pins the packages and `.python-version` records the Python 3.11.9 kernel that ran the notebook.
- [x] `data/README.md` documents the public release, hashes, and download commands; the notebook checks `clip-log.csv`; the notebook has been run from the top with saved outputs.
- [x] The split is documented as 15 training clips and 5 held-out clips (75% / 25%), selected by a fixed hand-defined rule; no random seed was used.

## Disclosure

- [x] `README.md` states which AI tools were used and for what.
