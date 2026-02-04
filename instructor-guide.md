# Instructor Guide: Machine Learning Fundamentals

## Module Overview

In this module, learners study the basics of machine learning — data preprocessing, inference, and model deployment — as applied in web systems. The session focuses on demystifying "Client-Side AI," moving students away from Python-heavy backends to running pre-trained models directly in the browser using JavaScript.

## Learning Objectives

By the end of this session, students will be able to:

* **Describe and apply fundamental ML concepts** relevant to integrating AI into web applications, specifically differentiating between *training* and *inference*.
* **Explain the role of Tensors** as the standard unit of data in machine learning and perform basic preprocessing (resizing, normalization).
* **Deploy and execute** a pre-trained machine learning model in the browser using TensorFlow.js to classify images or text.



## Session Pacing Guide (120 Minutes total)

| Duration | Segment | Instructor Action |
| --- | --- | --- |
| **20 min** | **Machine Learning in the Browser** | Discuss the shift from Cloud AI to Edge AI. Explain *why* we run ML in the browser (Privacy, Latency, Offline availability). |
| **30 min** | **The ML Pipeline: Tensors & Preprocessing** | "The Math Part." Use the "Excel Sheet" analogy for Tensors. Explain why images must become numbers (0-1 floats) before the model can read them. |
| **20 min** | **Training vs. Inference** | Use the "Studying vs. Taking the Exam" analogy. Clarify that in this course, we are mostly doing *Inference* (using existing brains). |
| **20 min** | **Live Demo: MobileNet** | Live code a simple HTML page that loads MobileNet via CDN. Show the `model.json` network request in DevTools. |
| **30 min** | **Lab: Running Models with TensorFlow.js** | Facilitate the lab. Help students access the webcam (if attempting the challenge) or debug image loading issues.

 |

---

## Delivery Notes & Teaching Tips

### 1. Training vs. Inference (The "Exam" Analogy)

* **Concept:** Beginners often think they need to "teach" the AI everything.
* **Analogy:**
* **Training:** A student studying for 4 years to become a doctor (Takes a long time, huge energy, requires a library of books/data).
* **Inference:** The doctor diagnosing a patient (Fast, happens in the moment, applies the knowledge they already have).


* **Key Point:** We are acting as the hospital hiring the doctor (Loading the Pre-trained Model), not the medical school (Training the Model).

### 2. Tensors (The Data Structure)

* **Visual Aid:** Draw a spreadsheet.
* **Scalar:** A single cell.
* **Vector:** A single column.
* **Matrix:** The whole sheet (2D).
* **Tensor:** A workbook containing multiple sheets (3D, 4D, etc.).


* **Why specific to Images?** Explain that an image is just a stack of 3 Matrices: Red, Green, and Blue.

### 3. Client-Side vs. Server-Side

* **Privacy Hook:** Ask the class: "If you built an app that detects skin cancer from a photo, would you feel comfortable sending those photos to a server?"
* **The Solution:** Client-side ML keeps the data on the user's phone. It never touches the internet. This is a massive selling point for TensorFlow.js.

---

## Lab Guide: Running Models with TensorFlow.js

**Lab Objective:** Use TensorFlow.js to run a simple in-browser model for image or text classification.

### Setup

* **Tools:** Code editor (VS Code), Browser.
* **Server:** Students need a local server (like Live Server extension in VS Code) because loading local images (`file://`) often causes security errors in JS.

### Common Student Issues & Solutions

* **Issue:** `SecurityError: The operation is insecure.` (Tainted Canvas).
* *Solution:* They are trying to load an image from a different domain without CORS headers. Use images from a source like Unsplash (with `crossorigin="anonymous"`) or local files served via a local host.


* **Issue:** "The model is taking forever to load."
* *Solution:* The first load of MobileNet is heavy (~2-4MB). Explain that the browser caches it, so the second refresh will be instant.


* **Issue:** "It thinks my coffee mug is a 'buckle'."
* *Solution:* MobileNet is small and fast, not perfect. This is a great moment to discuss **Confidence Scores** (Probability). If the confidence is low (e.g., 0.1), the app should probably say "I don't know."



### Debrief Questions

At the end of the lab, ask:

1. "Did you notice your laptop fan spinning up? Why?" (The browser accessed the GPU to do math).
2. "If you disconnect your WiFi, does the app still work?" (Yes, once the model is cached/downloaded).

---

## Resources for the Instructor

* **Reference:** [TensorFlow.js Pre-trained Models](https://github.com/tensorflow/tfjs-models)
* **Reference:** [MobileNet Class Names List](https://www.google.com/search?q=https://github.com/tensorflow/tfjs-models/blob/master/mobilenet/src/imagenet_classes.ts) (Useful to see what the model *can* actually detect).
* **AI Prompt Bank:**
* *"Explain the difference between a Tensor and a standard JavaScript Array."*
* *"My TensorFlow model is running slowly. What are three ways to optimize performance in the browser?"*