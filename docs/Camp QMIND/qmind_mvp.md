# Camp QMIND MVP Hackathon
Welcome guys! Today we're gonna build a little demo of our Parkinson's project to showcase that our idea is viable, computable, and actually pretty cool to see in action.
> MVP stands for Minimum Viable Product btw. It's basically a simplified version of our project that shows essential features.

## Intro to Parkinson's Disease
By now, hopefully you know what Parkinson's is, but if you don't, here is a quick crash course:

- progressive neurodegenerative disease in the dopamine-producing area of the brain
- primarily affects motor movement (ie. tremors, bradykinesia/slowed movement, stiff muscles, poor posture)
- causes: unknown (maybe genes? maybe toxin exposure?)
- risk factor: old age (>50), genetics, male sex

How is it diagnosed? 
- bradykinesia
- resting tremor
- rigidity
- postural instability

## What is finger tapping?
Tap the index finger and thumb together quickly and as widely as possible for at least 10 repetitions. 
- A positive test is when the movement becomes slower or smaller over time. 
- Fingers and toes are commonly affected.

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


## 3. Movement Measurements
Once we have the landmarks, we can start measuring movement.

Our main measurement will be the distance between the thumb and index fingertip over time.

As someone taps, this distance changes and creates a signal we can plot:

```text
Distance
   ^
   |
   |       /\       /\       /\
   |      /  \     /  \     /  \
   |_____/    \___/    \___/    \____
   |
   +---------------------------------> Time
```

From this, we can try to calculate:

- Number of taps
- Tapping frequency
- Average amplitude
- Amplitude variability
- Pauses between taps

If we have time, we can use peak detection to automatically identify individual taps.


## 4. Interactive Demo
Now let's turn this into something that actually feels like a product rather than just a notebook.

Ideally, our demo will show:


```text
┌──────────────────────┬──────────────────────┐
│   FINGER-TAPPING     │   FINGER DISTANCE    │
│       VIDEO          │        GRAPH         │
│                      │                      │
│   ● hand landmarks   │    /\    /\    /\    │
│                      │___/  \__/  \__/  \__ │
├──────────────────────┴──────────────────────┤
│ Taps: 42   Frequency: 4.8 Hz   Amplitude: X │
└─────────────────────────────────────────────┘
```

**Bonus**: make the video and graph interact with each other. Clicking a point on the graph could jump the video to that moment.


## 5. Design / UX
This isn't just a technical project!

Design members can work on:

- The layout of the demo
- Video + graph synchronization
- How movement measurements are displayed
- Explaining what each measurement means
- Making the interface understandable to someone who knows nothing about AI

The goal is to make the technical work **easy to understand**.


## 6. Pitch Competition!
We're gonna make a 🔥**FIRE**🔥 presentation

Our pitch will include:

- Team introduction
- The problem we're exploring
- What the computer sees
- How we turn movement into data
- Ethical considerations (is reliable, fair, clinically meaningful, stored safely?)
- **LIVE DEMO**
- What we learned
- Where the project goes next

The main demo should tell a simple story:

**Here is the video → here is what the computer sees → here is the movement signal → here is what we can measure → here is what each measurement means**

---

### MVP Success Criteria
By the end of Camp, we should aim to have:

- [ ] Finger-tapping video processed
- [ ] Hand landmarks displayed
- [ ] Thumb-index distance calculated
- [ ] Distance plotted over time
- [ ] At least one movement metric calculated
- [ ] Basic tap detection working
- [ ] A simple demo we can present

#### Stretch Goals
- [ ] Video and graph synchronized
- [ ] Multiple videos compared
- [ ] More movement characteristics
- [ ] "Can You Fool the AI?" interactive demo
- [ ] Cleaner UI
- [ ] AI Confidence Check
- [ ] Live demonstration of demo; record feature
- [ ] Adding additional tests: Hand supination, fist open close, toe tapping, rigidity testing, tremor testing




