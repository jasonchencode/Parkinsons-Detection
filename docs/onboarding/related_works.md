# Related Works
It's important to understand what has already been done in Parkinson’s disease assessment before starting our experiments. These papers cover computer vision, motor symptom assessment, and the use of AI in Parkinson’s research.

## 1. VisionMD
**Paper:** [VisionMD: an open-source tool for video-based analysis of motor function in movement disorders](https://www.nature.com/articles/s41531-025-00876-6)

Shows how MediaPipe pose estimation can turn video into movement signals, including thumb-index distance during finger tapping. This is especially relevant to our planned pose-estimation pipeline.


## 2. Automated Assessment of Finger Tapping Videos
**Paper:** [Clinically Informed Automated Assessment of Finger Tapping Videos in Parkinson’s Disease](https://pmc.ncbi.nlm.nih.gov/articles/PMC10674854/)

Uses MediaPipe hand pose estimation + time-series features + machine learning to assess finger tapping. Good reference for how we can go from video → keypoints → movement features → model.


## 3. Deep Learning of Parkinson's Movement
**Paper:** [Deep learning of Parkinson’s movement from video, without human-defined measures](https://pubmed.ncbi.nlm.nih.gov/38991323/)

Takes a different approach by feeding finger-tapping video directly into a 3D CNN, rather than manually defining movement features. Useful for thinking about the difference between feature-based and end-to-end approaches.


## 4. Video-Based Quantification of Motor Characteristics
**Paper:** [Interpretable and granular video-based quantification of motor characteristics from the finger-tapping test](https://www.nature.com/articles/s41531-026-01307-w)

Probably the most directly relevant recent work for our project. It breaks finger tapping into interpretable motor characteristics such as hypokinesia, bradykinesia, sequence effect, and hesitation/halts, and uses video to predict MDS-UPDRS severity.


## 5. AI/ML Ethical Considerations in Health Care
**Paper:** [Ethical Considerations in the Use of Artificial Intelligence and Machine Learning in Health Care: A Comprehensive Review](https://pmc.ncbi.nlm.nih.gov/articles/PMC11249277/)

Provides a broad overview of the ethical issues involved in using AI in healthcare, including privacy and data security, algorithmic bias and fairness, transparency, clinical validation, and professional responsibility. This is particularly relevant to the second part of our project, where we will consider how reliable an AI-based Parkinson’s assessment should be, how bias in training data could affect different patient populations, and how AI should be used alongside clinical judgement.
