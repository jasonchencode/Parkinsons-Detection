# Parkinson's Disease Detection

Parkinson's disease (PD) is a neurological disorder that can affect a person's movement. One of the symptoms we are interested in is **bradykinesia**, which refers to slowness of movement and can be assessed through repetitive movements such as finger tapping.

A lot of existing research uses computer vision or machine learning to detect Parkinson's from movement data. However, many approaches ultimately try to answer a pretty simple question: **Does this person have Parkinson's or not?**

That's not quite what we're interested in.

Instead, we want to explore whether a computer vision system can **measure Parkinson's-related motor symptoms from video while also communicating how uncertain it is about its assessment.** Basically, we're asking whether we can build a model that doesn't just give an answer, but also tells us how much we should trust that answer?

This gives us two sides to the project:
- **Technical**: Build and evaluate a computer vision model for assessing motor symptoms from finger-tapping video.
- **Research/ethics**: Investigate what it actually means to use a system like this in a clinical setting, including uncertainty, bias, explainability, and when the system should defer to a clinician.



## Why finger tapping?

Finger tapping is a standardized motor task that can reveal changes in movement associated with Parkinsonian symptoms.

When someone repeatedly taps their fingers, we can measure things like:
- How many taps they complete
- How far their fingers move
- How quickly they move
- How consistent each tap is
- Whether the movement gets smaller over time
- Differences between the left and right hand
These are things that can be measured from a video without requiring specialized sensors.

## Why are we doing this?
Medical AI can produce impressive predictions, but a prediction by itself does not tell us whether the system should be trusted.

A model might perform well on the data it was trained on but behave differently when:

- The lighting changes
- The camera is positioned differently
- A hand is partially obstructed
- The video quality is lower
- The person looks different from the training population
