# Proposal

## Who
Project Members:
* Abhimanyu Kushwaha
* Tariq Shinwari
* David

## Hypothesis

Image clarity can predict the time needed to review footage of ordinary civilian vehicles more accurately than an average review time baseline. Motivated by my experience supporting Automatic Target Recognition software, this project will estimate reviewer minutes per unseen one minute clip to help plan imagery review staffing.

## Data

I plan to record 20 one-minute clips of parked civilian passenger cars over two weeks. The clips will include differences in lighting, background clutter, and partial obstruction.
For each clip, I will examine 12 frames at five-second intervals, from 0 through 55 seconds, and count visible passenger cars in each frame. Each frame will be counted separately, using a consistent rule for partially visible cars.
Each dataset row will record the clip identifier, image-clarity rating, and total time needed to review the frames and enter the counts. Clarity will be rated before timing as clear, moderately unclear, or very unclear. The same reviewer and procedure will be used throughout.
A simple regression model will be compared with a baseline that predicts the average training set review time. Approximately 15 clips will be used for model development and five for testing, keeping clips from the same recording session together. Evaluation will measure prediction error in seconds and examine uncertainty.

The small sample and single reviewer will limit generalization. Footage will exclude identifiable people, readable license plates, and workplace material. Sources and reuse terms will be documented in data/README.md.

## Decision affected by the model

A dataset-preparation manager will use predicted review times to allocate reviewer hours for a batch of similar civilian vehicle footage. Underestimating workload may cause delays or overtime, while overestimating it leaves unused capacity. I will compare these costs under different assumptions to assess whether the model improves staffing decisions over the average time baseline.
