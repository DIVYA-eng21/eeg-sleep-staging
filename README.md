# EEG Sleep Stage Classification

Classifying sleep stages from raw EEG signals using the Sleep-EDF dataset from PhysioNet.
This was done as part of a research internship task.

## Dataset
Sleep-EDF Expanded Database (PhysioNet)
- 2 subjects, 1 night recording each
- 2 EEG channels: Fpz-Cz and Pz-Oz
- Sampled at 100 Hz
- 5 sleep stages: Wake, N1, N2, N3, REM

## What I did
- Loaded raw EEG signals using MNE
- Applied bandpass filter (0.5 - 30 Hz) to remove noise
- Cut continuous recording into 30 second epochs (2650 total)
- Extracted band power features using Welch's method
  (delta, theta, alpha, sigma, beta for each channel = 10 features)
- Handled class imbalance using SMOTE for ML models,
  class weights for CNN
- Trained ML and DL models

## Results

| Model | Overall Accuracy | Macro Avg |
|-------|-----------------|-----------|
| Random Forest | 95.6% | 80% |
| SVM | 96.2% | 84% |
| MLP | 94.5% | 79% |
| CNN (raw signals) | 93.0% | 79% |

SVM gave best overall accuracy. But CNN showed better recall on N1
(92% vs ~33-50% for ML models) because it learns directly from
raw signals instead of manually extracted features.

## Key Findings
- Delta band power was highest in N3 and lowest in REM,
  confirming feature extraction was biologically correct
- N1 was hardest class across all models — consistent with
  published sleep staging literature
- CNN is better at detecting minority sleep stages despite
  lower overall accuracy

## Limitation
- Only 1 subject's data was used for the full pipeline in ML pipelines
  (second subject was downloaded but not included)
  while in DL , 1 subject is downloaded and used.
- Single channel consumer EEG would perform worse;
  this used clinical grade 2 channel EEG

## Note
If GitHub shows a rendering error opening the notebook,
download it and open in Google Colab — everything works fine there.

## References
- Kemp et al. (2000). Sleep-EDF dataset.
  IEEE Transactions on Biomedical Engineering, 47(9), 1185-1194.
- Goldberger et al. (2000). PhysioNet. Circulation.

## Tech Stack
Python, MNE, Scikit-learn, TensorFlow, Keras, SciPy, imbalanced-learn
