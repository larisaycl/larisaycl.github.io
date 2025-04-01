---
title: "Virtual Tasks for Eye Gaze Characterization"
excerpt: "Virtual tasks for eye gaze characterization, and open-source ROS wrapper for Tobii Pro Glasses 3<br/><img src='/images/gazetasks.png'>"
collection: portfolio
---

## Overview
This project is the implementation of the eye gaze characterization system presented in "Characterizing Eye Gaze for Assistive Device Control". This work was presented at ICORR 2023, with journal extension subsequently published in Wearable Technologies, Volume 6, 2025. 

The main contributions of this work are three-fold:
* A suite of open-source assessment and data gathering tasks for use with an eye gaze tracking interface.
* An open-source system for interfacing an eye gaze tracker for real-time control, integrated within the Robot Operating System (ROS) software suite.
* An end-user study that employs these tools to collect data for an individualized characterization of eye gaze for control, to provide further insights into the design of interfaces for systems that use eye gaze as input.

Code can be found here: [Eyegaze Characterization Tasks](https://github.com/argallab/eyegaze_characterization_tasks/)

## Summary of Virtual Tasks
![](/images/gazetasks.png)

The four characterization tasks were designed to collect gaze data for specific types of gaze movement patterns and metrics during eye-based control. 

### A: Painting Task
**Task description:** Participants’ eye gaze position controls a virtual paintbrush. They are asked to ‘paint’ the entire screen with their eyes within 5 minutes.

**Features of interest:** Distribution of eye gaze, distribution of fixations, areas of visual neglect.

### B/C: Focus Task (with/without visual feedback)
**Task description:** Participants viewed and fixated on 60 randomly appearing circular targets of varying sizes on the screen and were asked to maintain their gaze for 2 seconds. If 2 seconds of continuous fixation was not maintained by the end of 10 seconds, the target timed out.

**Features of interest:** Saccades, fixations, dwell time

**Visual feedback:** Participants are given feedback on how much longer they need to fixate on the target via variations in opacity. A target becomes more transparent the longer participants dwell on it, up to 2 seconds when the target fades completely and the next target appears. Two variants of the task exist: (1) Participants are not given any visual feedback of where their measured gaze is. (2) Participants are provided with this feedback in the form of a moving dot on the screen.

### D: Tracking Task
**Task description:** Twenty-four moving targets (circles) appear on the screen one after another. Participants are tasked with following the targets with their gaze. Targets move at a speed of approximately 15 degrees of visual angle per second.

**Features of interest:** Smooth pursuit.

**Visual feedback:** Participants are given feedback on the proximity of their measured gaze to the moving target by a variation in the opacity of the target. (More opacity indicating being closer to the target.)