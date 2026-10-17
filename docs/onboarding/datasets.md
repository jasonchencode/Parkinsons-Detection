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

This is the larger vocal dataset for the project. Our working understanding is that it covers about 1,000 unique participants (roughly 500 with Parkinson's disease and 500 controls) performing sustained vowel phonations, and it will be the main dataset for comparing classical ML, a spectrogram-based CNN, and optional pretrained audio models.

**To confirm during the audit:**
- The source and meaning of the diagnostic labels (clinically confirmed or self-reported)
- The exact class counts and the number of recordings per participant
- Recording duration, audio quality, file format, and collection procedures
- Which demographic fields are available and how much is missing

Participant counts and the relationship between the two vocal datasets are based on our research plan and have not yet been verified against the dataset documentation. We update this section once the audit is complete.


[^1]: 0-to-4 rating scale used by doctors to measure the severity and progression of Parkinson's disease
