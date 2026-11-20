# Datasets

We work with datasets for two tracks: finger-tapping video (Track One) and vocal recordings (Track Two). The tracks are modeled and evaluated independently, since the datasets differ in size, format, and prediction target.

For every dataset, Stage 1 of the project involves an audit to confirm the number of unique participants, the source and meaning of the labels, and what demographic information is available (see [stages.md](stages.md)).


## Track One: Finger-Tapping Video

### [HUBU-FIS Finger Tapping Dataset](https://zenodo.org/records/17738775)
This dataset contains 234 finger-tapping videos from both healthy controls and people diagnosed with Parkinson's disease. It also includes an UPDRS rating for each video.[^1]

This will be our main dataset for the computer vision side of the project, since we can work directly with the videos.

**To confirm during the audit:**
- The number of unique participants (left- and right-hand recordings may come from the same person)
- Whether the UPDRS ratings are hand-specific or task-specific, or only available at the patient level. This decides whether we estimate motor severity or classify Parkinson's.
- Which demographic metadata is available

All videos from the same participant must stay in the same training, validation, or test split.

### [Parkinson's Finger-Tapping Dataset](https://figshare.com/articles/dataset/Parkinson_data_csv/28883489?file=54255155)

This dataset contains 100 subjects: 53 with Parkinson's disease and 47 healthy subjects. Instead of the original videos, it provides finger-tapping features extracted using computer vision, including tapping count, amplitude, variation, and amplitude decrement.

We'll use this dataset to help us understand which movement characteristics are associated with Parkinson's and to provide another dataset for comparison.


## Track Two: Vocal Recordings

Our vocal data consists of sustained vowel phonations (such as /a/), used for binary Parkinson's disease classification. Because these are sustained vowels rather than continuous speech, feature extraction and interpretation are adapted to the actual recording task.

### [Voice Samples for Patients with Parkinson's Disease and Healthy Controls (Figshare)](https://figshare.com/articles/dataset/Voice_Samples_for_Patients_with_Parkinson_s_Disease_and_Healthy_Controls/23849127)

Voice recordings of participants with Parkinson's disease and healthy controls, with demographic information such as age and sex. Published work using what appears to be this repository describes WAV recordings of the vowel /a/ made on participants' own phones, with a small number of recordings (reported as 81 voices, 40 PD and 41 controls).

This is likely the source of the demographic information we use for the vocal track. We'll use it to examine age and gender composition, and to check whether model performance varies across groups, subject to sample size.

**To confirm during the audit:** the exact file and class counts, the recording procedure and devices, and whether these participants overlap with the larger vocal dataset. If they do, they cannot be treated as an independent test set if their recordings were used for training or model selection.

### [Parkinson's Voice Dataset (Kaggle)](https://www.kaggle.com/datasets/ucimachinelearning/parkinsons-voice-dataset?select=Voice_Dataset)

This is the larger vocal dataset for the project, and it will be the main dataset for comparing classical ML, a spectrogram-based CNN, and optional pretrained audio models. Initial checks (November 2026) confirm that it contains raw audio: 1,134 WAV recordings (68.2 MB), organized as 574 files labeled Healthy and 560 files labeled Parkinsons, released under CC0 on the UCI Machine Learning Repository's Kaggle account.

**To confirm during the audit (still open):**
- The number of unique participants: the 1,134 files do not map one-to-one to participants until the file naming is verified
- The source and meaning of the diagnostic labels (clinically confirmed or self-reported): the dataset currently ships with no description, no listed authors, and no DOI or provenance
- Recording duration, audio quality, sampling rate, and collection procedures
- Which demographic fields are available (none are published with the dataset so far)

A request on the dataset's discussion board asking for the original source, participant information, and recording protocol has remained unanswered as of November 2026. Until documentation appears, these counts come from the file listing rather than dataset documentation.

### [Parkinson Speech Dataset with Multiple Types of Sound Recordings (UCI)](https://archive.ics.uci.edu/dataset/301/parkinson%2Bspeech%2Bdataset%2Bwith%2Bmultiple%2Btypes%2Bof%2BAudio%2Brecordings?)
**Folder**: Parkinson_Multiple_Sound_Recording

**Format**: TXT files containing extracted voice features

**Participants**: 40 (20 Parkinson's, 20 healthy), with 26 recordings/tasks per participant.

Useful for exploring acoustic features and training classical ML models.

### [Parkinsons Telemonitoring (UCI)](https://archive.ics.uci.edu/dataset/189/parkinsons+telemonitoring)
**Format**: Pre-extracted voice features

**Participants**: 42 people with early-stage Parkinson's, with repeated recordings.

Contains UPDRS scores, making it useful for exploring severity prediction rather than PD-versus-healthy classification.

### [Parkinson's Disease Data Set (Kaggle)](https://www.kaggle.com/datasets/vikasukani/parkinsons-disease-data-set)
**Format**: Pre-extracted voice features

**Participants**: 31 (23 Parkinson's), with 195 total voice observations.

Useful for testing an initial classical ML classification model.

### [Audios vowel A PD (Figshare)](https://figshare.com/articles/dataset/Audios_vowel_A_PD/21453867)
**Folder**: 21453867

**Format**: WAV recordings

**Participants**: 126 (55 Parkinson's), with some demographic information.

Additional raw vowel recordings for feature extraction and classification experiments.

### [Parkinson's Disease Classification (UCI)](https://archive.ics.uci.edu/dataset/470/parkinson+s+disease+classification)
**Format**: Pre-extracted acoustic features

**Participants**: 252 (188 Parkinson's, 64 healthy)

[^1]: 0-to-4 rating scale used by doctors to measure the severity and progression of Parkinson's disease
