# Related Works
It's important to understand what has already been done in Parkinson's disease assessment before starting our experiments. These papers cover computer vision, vocal analysis, motor symptom assessment, and the use of AI in Parkinson's research. They are grouped by the track of our project they inform.


## Track One: Finger-Tapping Video

### 1. VisionMD
Paper: [VisionMD: an open-source tool for video-based analysis of motor function in movement disorders](https://www.nature.com/articles/s41531-025-00876-6)

Shows how MediaPipe pose estimation can turn video into movement signals, including thumb-index distance during finger tapping. This is especially relevant to our planned pose-estimation pipeline.

### 2. Automated Assessment of Finger Tapping Videos
Paper: [Clinically Informed Automated Assessment of Finger Tapping Videos in Parkinson's Disease](https://pmc.ncbi.nlm.nih.gov/articles/PMC10674854/)

Uses MediaPipe hand pose estimation + time-series features + machine learning to assess finger tapping. Good reference for how we can go from video → keypoints → movement features → classical ML model, which is the approach we prioritize given our limited sample size.

### 3. Deep Learning of Parkinson's Movement
Paper: [Deep learning of Parkinson's movement from video, without human-defined measures](https://pubmed.ncbi.nlm.nih.gov/38991323/)

Takes a different approach by feeding finger-tapping video directly into a 3D CNN (Convolutional Neural Network), rather than manually defining movement features. Useful for thinking about the difference between feature-based and end-to-end approaches, and for understanding what we are trading off by staying with interpretable features.

### 4. Video-Based Quantification of Motor Characteristics
Paper: [Interpretable and granular video-based quantification of motor characteristics from the finger-tapping test](https://www.nature.com/articles/s41531-026-01307-w)

Probably the most directly relevant recent work for our finger-tapping track. It breaks finger tapping into interpretable motor characteristics such as hypokinesia, bradykinesia, sequence effect, and hesitation/halts, and uses video to predict MDS-UPDRS severity.


## Track Two: Vocal Analysis

### 5. Voice-Based Detection of Parkinson's Disease Using ML and DL
Paper: [Voice-Based Detection of Parkinson's Disease Using Machine and Deep Learning Approaches: A Systematic Review](https://pmc.ncbi.nlm.nih.gov/articles/PMC12649940/)

A systematic review of studies from 2020 to September 2025 on voice-based Parkinson's detection using machine learning and deep learning, drawing on PubMed, Scopus, IEEE Xplore, and Web of Science. It frames vocal impairment as one of the earliest and most common symptoms of PD, and gives us an overview of how classical ML and deep learning approaches have been compared in the literature. This is particularly relevant to our vocal track, where we compare engineered acoustic features against spectrogram-based CNNs and pretrained audio representations, and to how we audit our dataset, design our splits, and avoid over-claiming from a single performance metric.


## Ethics and Responsible AI

### 6. AI/ML Ethical Considerations in Health Care
Paper: [Ethical Considerations in the Use of Artificial Intelligence and Machine Learning in Health Care: A Comprehensive Review](https://pmc.ncbi.nlm.nih.gov/articles/PMC11249277/)

Provides a broad overview of the ethical issues involved in using AI in healthcare, including privacy and data security, algorithmic bias and fairness, transparency, clinical validation, and professional responsibility. This is particularly relevant to the second part of our project, where we will consider how reliable an AI-based Parkinson's assessment should be, how bias in training data could affect different patient populations, when predictions should be deferred to a clinician, and how AI should be used alongside clinical judgement.ect different patient populations, and how AI should be used alongside clinical judgement.
