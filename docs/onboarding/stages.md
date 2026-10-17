# Project Stages
Detailed information regarding the predetermined stages of our research project (subject to change)

The project has two tracks, finger-tapping video analysis (Track One) and vocal analysis (Track Two). They are modeled and evaluated independently, since their datasets differ in size, format, and prediction target. Stages 1 to 4 apply to each track separately, and Stages 5 to 8 apply to both.


## Stage 1: Dataset
Find, audit, and prepare suitable datasets for both tracks.

We'll investigate what information is available, including:

* Recordings (videos and audio)
* Labels (motor severity scores or diagnostic labels) and where they come from
* Patient information
* Demographics and how much of it is missing
* Number of unique subjects

It's important that our datasets actually support the questions we're trying to answer. Here are the current [datasets](./datasets.md) we'll be working with.

**Finger-tapping:**
* Confirm the number of unique participants (the ~234 videos likely include left- and right-hand recordings from the same person)
* Confirm which labels are available: hand-specific or task-specific motor severity scores, or only diagnostic labels. This decides whether we estimate severity or classify.

**Vocal:**
* Confirm the source and meaning of the diagnostic labels (clinically confirmed or self-reported)
* Confirm the number of recordings per participant and the exact class counts (about 1,000 participants, roughly 500 PD and 500 controls)
* Check recording duration, audio quality, format, and collection procedures
* Check whether the 100-person demographic subset overlaps with the 1,000-participant dataset, and which demographic fields are available

**Splitting:** All recordings from the same participant stay in the same training, validation, or test split. We will not treat a subset as an independent test set if it overlaps with the training data.


## Stage 2: Pose Estimation and Audio Preprocessing

**Finger-tapping:** Use pose estimation (OpenCV and MediaPipe Hand Landmarker) to extract 21 hand landmarks from each video. Instead of working directly with pixels, we'll get something like:

Video → Hand landmarks → Finger separation (thumb tip to index fingertip) over time

We'll also record tracking quality and the proportion of missing landmarks, since these will matter for reliability later.

**Vocal:** Run audio quality checks and preprocessing on the sustained-vowel recordings, then prepare them for both pipelines:

Audio → Quality checks and preprocessing → Acoustic features and log-Mel spectrograms


## Stage 3: Feature Extraction

**Finger-tapping:** Use the landmark time series to measure movement characteristics such as:

* Tapping frequency and total tap count
* Amplitude (mean and maximum)
* Amplitude variability and decrement over time
* Inter-tap intervals and timing variability
* Velocity and acceleration
* Left/right differences, where paired recordings and suitable labels exist
* Tracking quality

**Vocal:** Extract interpretable acoustic features using tools such as openSMILE and librosa:

* MFCCs
* Fundamental frequency and pitch variability
* Jitter and shimmer
* Harmonic-to-noise ratio
* Voice intensity and amplitude variability
* eGeMAPS and other task-appropriate measures

Because the recordings are sustained vowels rather than continuous speech, feature extraction and interpretation will be adapted to the actual recording task.


## Stage 4: Model Training

We select approaches based on the data available for each track, rather than applying the same architecture to both.

**Finger-tapping (classical ML):**
Given the limited sample size, we prioritize interpretable features and classical machine learning rather than starting with a complex temporal deep learning model. Candidate models:

* Logistic Regression (if the outcome is binary)
* Random Forest
* XGBoost or LightGBM
* Ordinal regression (if ordered clinical severity scores are available)

The target depends on the labels. If hand-specific or task-specific severity scores are available, we estimate motor impairment. If only diagnostic labels are available, we classify Parkinson's instead. We will not assume patient-level labels can support hand-specific severity estimates. A temporal model such as an LSTM may be revisited later only if the data and results justify it.

**Vocal (classical ML vs. deep learning):**
The initial task is binary Parkinson's classification. We compare:

1. Classical ML on engineered acoustic features (Logistic Regression, SVM, Random Forest, XGBoost or LightGBM)
2. A small CNN trained on log-Mel spectrograms, with regularization, early stopping, and augmentation where justified
3. Pretrained audio representations (e.g. wav2vec 2.0) with a classification head, as an optional extension. We start with a frozen encoder and fine-tune only if justified.

All vocal models use consistent training, validation, and test partitions wherever possible. We establish a reproducible classical baseline first, then ask whether deep learning provides a meaningful improvement in performance, calibration, or robustness. A deep learning model is not automatically considered better based on one metric or one test split.

**Preventing leakage:** Preprocessing, feature selection, and hyperparameter tuning are fitted only within the training data or cross-validation folds.


## Stage 5: Evaluation and Validation

Each track uses metrics appropriate to its task.

* **Vocal classification:** ROC-AUC, sensitivity and specificity, precision, recall, F1, confusion matrix, probability calibration, and accuracy (never as the sole measure). We'll also discuss how predictive values change in populations with different disease prevalence.
* **Finger-tapping:** MAE, RMSE, and error across the severity range for continuous scores. Ordinal-aware metrics and agreement measures for ordinal scores. Classification metrics if only binary labels exist.

We report variability across cross-validation folds and confidence intervals where feasible, and reserve an independent test set where dataset size and structure permit.


## Stage 6: Uncertainty

A model shouldn't just give us a prediction, but should also state how confident it is. We'll investigate different methods for estimating and evaluating this uncertainty:

* Probability calibration
* Bootstrap-based uncertainty analysis
* Deep ensembles (for suitable models)
* Monte Carlo dropout (for compatible neural networks)
* Conformal prediction (where its assumptions and calibration data permit)

We distinguish between a model's confidence and whether its prediction is actually correct. High confidence alone does not establish reliability.

* **Vocal:** Can uncertainty identify recordings that are difficult to classify?
* **Finger-tapping:** Is uncertainty associated with poor landmark tracking, unusual movement patterns, or larger clinical prediction errors?

The goal is to investigate whether uncertainty can support a deferral mechanism, where predictions are flagged for clinician review when reliability is insufficient.


## Stage 7: Robustness, Explainability & Fairness

**Robustness and distribution shift:**
* Finger-tapping: camera angle and distance, lighting, compression, frame rate, hand occlusion, missing landmarks, movement speed
* Vocal: background noise, microphone quality and distance, recording device, duration and intensity, differences in vocal tasks, demographic and language variation
* Does uncertainty increase when input quality deteriorates? Where possible, we'll consider external validation.

**Explainability:**
* Classical ML: feature importance and SHAP, to see which movement or acoustic characteristics contribute
* Vocal deep learning: time-frequency occlusion experiments or spectrogram-region importance
* Do classical and deep learning approaches appear to rely on consistent patterns?
* Highly ranked features are not assumed to cause Parkinson's, and highlighted regions are not treated as validated biomarkers. Findings are hypotheses requiring clinical validation.

**Fairness:**
* Whether performance changes across patient groups (sensitivity, specificity, false-positive and false-negative rates, calibration, and prediction error for severity)
* Whether uncertainty and deferral rates change across patient groups
* For the vocal track, whether the demographic subset supports age and gender analysis, subject to its size and overlap with the main dataset. For finger-tapping, this depends on the available metadata.
* How limitations in the datasets (representation, recording conditions, composition) could affect the models
* Subgroup results are interpreted cautiously where sample sizes are small, and strong overall performance is not treated as evidence of fairness.


## Stage 8: Ethics and Human Oversight

Towards the end, we'll connect our technical results to the clinical setting. The intended system is not an autonomous diagnostic tool. It is a research framework for clinician-supervised assessment:

Input data → Quality checks → Predictive model → Prediction and uncertainty → Reliability assessment → Clinician review when needed

Questions we'll explore include:

* When should an AI system provide an assessment?
* When should it say "I'm not sure"?
* When should a clinician override the model?
* What should responsible use of a system like this look like?
* How do participants and future patients also override the model (not just clinicians)? What will happen if the patient doesn't think the model is accurately capturing their experience?
* How should the limitations of each modality be communicated before the system can support clinical decisions?

Any potential clinical use would require further validation and appropriate clinical oversight.


## Final Synthesis

The two tracks are compared at the research level, not combined into a single diagnostic score:

* How useful are interpretable features for each modality?
* Does deep learning improve performance for vocal analysis?
* How do data quantity and representation affect model complexity?
* Which types of input degradation affect each model?
* Can uncertainty and explainability improve the reliability of both approaches?

Multimodal fusion would only be considered as a future extension if a dataset with both vocal and finger-tapping recordings from the same participants, compatible labels, and a defensible validation design becomes available.
