# Project Stages
Detailed information regarding the predetermined stages of our research project (subject to change)

## Stage 1: Dataset
Find and prepare a suitable finger-tapping video dataset.

We'll investigate what information is available, including:
- Videos
- Motor symptom labels
- Patient information
- Demographics
- Number of subjects

It's important that our dataset actually supports the questions we're trying to answer. Here are the current [datasets](./datasets.md) we'll be working with.


## Stage 2: Pose Estimation
Use pose estimation to extract hand and finger landmarks from each video. Instead of working directly with pixels, we'll get something like: 

Video → Hand landmarks → Movement over time


## Stage 3: Feature Extraction
Use the landmarks to measure movement characteristics such as:
- Speed
- Frequency
- Amplitude
- Variability
- Left/right differences


## Stage 4: Model Training
Train models to estimate motor symptom severity from the movement data.

We'll first establish a baseline using traditional machine learning on extracted movement features. We'll then explore **temporal deep learning models**, which are models designed to learn patterns and changes across sequential data over time. Our planned primary architecture is an **LSTM (Long Short-Term Memory) network**, trained on sequences of hand keypoints and movement measurements to learn temporal patterns in the tapping behaviour.

While the LSTM will be our primary approach, we may explore other temporal deep learning architectures depending on our results and the structure of the data.

The LSTM will predict a **continuous measure of motor symptom severity**, rather than simply classifying someone as having Parkinson's or not.

## Stage 5: Uncertainty
A model shouldn't just give us a prediction, but should also state how confident it is. We'll investigate different methods for estimating and evaluating this uncertainty.


## Stage 6: Explainability & Fairness
We'll look into:
- What movement patterns the model uses
- Whether performance changes across patient groups
- Whether uncertainty changes across patient groups
- How limitations in the dataset could affect the model


## Stage 7: Ethics
Towards the end, we'll connect our technical results to the clinical setting. Questions we'll explore include:
- When should an AI system provide an assessment?
- When should it say "I'm not sure"?
- When should a clinician override the model?
- What should responsible use of a system like this look like?
- How do participants and future patients also override the model (not just clinicians). What will happen if the patient doesn't think the model is accurately capturing their experience?

