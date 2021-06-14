<center><h2> Progress Report (June 9-13) </h2></center>  

<center> Drone Video - Optical Flow Subteam - Pair A (Gary Zancanelli & Michael Scirocco) </center>  

---

<center> <h3> Task </h3> </center>

Our task this week was to implement frame skipping into the current solution; we do this by only running the detector on every N frames. This decreases the accuracy because there's a gap between frames, but decreases the computation time dramatically. This is the basis for allowing us to implement optical flow.  

--- 

<center> <h3> How We Implemented Frame Skipping & Code </center> </h3>  

We implemented frame skipping inside the *track.py* file. We are detecting a frame every 10 frames; this detection rate is a temporary threshold set to test whether our frame skipping worked (the detection rate constant can be changed in the future for better performance). The code also ensures the first 10 frames are detected to allow the solution to acquire the correct labels.

```python
    #Skip Variables
    skipThreshold = 0 #Current number of frames skipped
    skipLimit = 10 #Num of frames to skip

    for path, img, im0s, vid_cap in dataset:

        #Frame Skipping Implementation
        if frame_num > 10 and skipThreshold < skipLimit:
            skipThreshold = skipThreshold + 1
            frame_num += 1
            continue
        skipThreshold = 0
```

We did have to comment out some lines of code (that were negligible to the solution's performance) for the frame skipping to work.

```python
    #avgFps = (sum(fpses) / len(fpses))
    #print('Average FPS = %.2f' % avgFps)
```

---  

<center><h3> Results </center></h3>  

| Video File    | Original Solution Accuracy | Original Solution Time | Frame Skipped Accuracy | Frame Skipped Time |
| ------------- | -------------------------- | ---------------------- | ---------------------- | ------------------ |
| 4p1b_01A2.m4v | 93%                        | 65.621 s               |                        | 24.151 s           |
| 5p2b_01A1.m4v | 93%                        | 135.272 s              | 50%                    | 45.203 s           |
| 5p4b_01A2.m4v | 92%                        | 97.464 s               | 73%                    | 41.653 s           |
| 5p5b_03A1.m4v | 48%                        | 79.856 s               | 30%                    | 26.226 s           |
| 7p3b_02M.m4v  |                            |                        |                        |                    |
