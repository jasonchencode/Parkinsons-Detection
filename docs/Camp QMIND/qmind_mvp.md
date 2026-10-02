# Camp QMIND MVP Hackathon
Welcome guys! Today we're gonna build a little demo of our Parkinson's project to showcase that our idea is viable, computable, and actually pretty cool to see in action.
> MVP stands for Minimum Viable Product btw. It's basically a simplified version of our project that shows essential features.

## The Plan
As y'all know, our project will use computer vision to analyze finger-tapping and eventually explore how these movements can be used to assess Parkinson's. For Camp QMIND, we don't have the time/resources to build a full, fleshed-out system. Instead, we're gonna make an MVP of the first part of our research:

**Video → Hand Tracking → Movement Measurements → Visualization**

The result could show the finger-tapping video and what the computer measure/sees at the same time (something like how the distance between fingers changes). This is just an idea also, so we can always pivot or implement something else if any of you have really cool ideas.


## 1. Data
First, we need a small set of finger-tapping videos to work with. We already have a dataset, but we could look into other datasets for a bit as long as they:

- clearly show someone's hand
- contain finger-tapping movements
- are short enough to process quickly
- have enough movement to measure

And then we need to get a video loaded and processed frame-by-frame


## 2. Hand Tracking
Now we need to get the computer to understand where the hand and fingers are. We can use **MediaPipe Hand Landmarker** to detect points such as:

- thumb tip
- index fingertip
- finger joints
- wrist

The landmarks can be drawn on top of the video so the demo can see what the computer sees.
