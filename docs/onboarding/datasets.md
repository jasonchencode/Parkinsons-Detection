# Datasets

We'll primarily work with two finger-tapping datasets.

## [HUBU-FIS Finger Tapping Dataset](https://zenodo.org/records/17738775)
This dataset contains 234 finger-tapping videos from both healthy controls and people diagnosed with Parkinson's disease. It also includes an UPDRS rating for each video.[^1]

This will be our main dataset for the computer vision side of the project, since we can work directly with the videos.


## [Parkinson's Finger-Tapping Dataset](https://figshare.com/articles/dataset/Parkinson_data_csv/28883489?file=54255155)

This dataset contains 100 subjects: 53 with Parkinson's disease and 47 healthy subjects. Instead of the original videos, it provides finger-tapping features extracted using computer vision, including tapping count, amplitude, variation, and amplitude decrement.

We'll use this dataset to help us understand which movement characteristics are associated with Parkinson's and to provide another dataset for comparison.

[^1]: 0-to-4 rating scale used by doctors to measure the severity and progression of Parkinson's disease
