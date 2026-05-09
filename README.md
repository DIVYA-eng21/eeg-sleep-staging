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
- Extracted band power features myself using Welch's method
  (delta, theta, alpha, sigma, beta for each channel = 10 features)
- Handled class imbalance using SMOTE
- Trained ML and DL models

## Results

| Model | Overall Accuracy | Macro Avg |
|-------|-----------------|-----------|
| Random Forest | 95.6% | 80% |
| SVM | 96.2% | 84% |
| MLP | 94.5% | 79% |

SVM performed best. N1 was hardest to classify across all models
which is consistent with published sleep staging literature.

## Key Finding
Delta band power was highest in N3 (deep sleep) and lowest in REM,
which matches known neuroscience. This confirmed that feature
extraction was working correctly.

## Note
If GitHub shows a rendering error opening the notebook,
download it and open in Google Colab — everything works fine there.

## Tech Stack
Python, MNE, Scikit-learn, TensorFlow, Keras, SciPy, SMOTE
