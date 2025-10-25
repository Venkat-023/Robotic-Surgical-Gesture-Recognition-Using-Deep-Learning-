# 🩺 Robotic Surgical Gesture Recognition Using Deep Learning

🚀 A Deep Learning Framework for Automatic Surgical Gesture Identification and Classification Using 3D Convolutional Neural Networks (Conv3D + LSTM)

📘 Overview

This repository contains two deep learning projects focused on robotic surgical gesture recognition from video data.
The goal is to enable automated understanding of robotic motions during surgical procedures using video-based deep learning models.

#🔹 Project 1 — Gesture Identification

Binary classification model that determines whether the robot is performing gesture G3 ("Pushing the needle through tissue") or any other gesture (NON-G3).

#🔹 Project 2 — Gesture Classification

Multiclass model that classifies robotic surgical actions into one of five gestures:

G1 – Reaching the needle with right hand

G2 – Positioning the needle

G3 – Pushing the needle through tissue

G4 – Transferring the needle from left to right hand

G11 – Dropping the suture at the end and moving to end points

💡 Project Intuition

During robot-assisted surgeries, surgeons perform atomic gestures (surgemes) that follow a predictable workflow.
Each gesture has a unique spatio-temporal signature, which can be captured by video-based neural networks.

Intuition:

“Each surgical gesture leaves a distinct spatial and temporal pattern. By analyzing short clips of video frames, a deep learning model can automatically recognize the gesture being performed.”

🧠 Motivation

Robotic surgery requires precise, repeatable gestures. Automatic gesture recognition can help in:

Assessing surgeon skill and efficiency

Automating surgical workflow analysis

Real-time surgical phase detection

Training and performance feedback

This project builds models that can learn and classify these gestures directly from surgical video frames, reducing the need for manual annotation.

⚙️ Technical Details
🧱 Model Architectures

Conv3D + Batch Normalization (for both binary and multiclass tasks)

3D Convolutions for spatio-temporal feature extraction

Batch Normalization and Dropout for training stability

Dense layers for classification

Conv3D + LSTM (for advanced gesture classification)

Conv3D layers capture frame-level spatial features

LSTM models temporal gesture progression across frames

Effective for sequential robotic motion data

🧮 Data Processing Pipeline

Dataset Organization

Raw surgical videos organized into folders: g1, g2, g3, g4, g11

Automatic scripts detect gesture IDs and organize videos for binary and multiclass tasks

Frame Sampling

Each video is sampled into 16 or 32 evenly spaced frames

Frames resized to 112×112 pixels

Converted to grayscale to emphasize motion over texture

Batch Generation

Custom VideoDataGenerator using TensorFlow’s Sequence API

Normalization and batching performed on-the-fly

Label Encoding

Multiclass: One-hot encoded labels (g1–g11)

Binary: 0 = NON_G3, 1 = G3

🧪 Training Configuration
Parameter	Value
Input Frames	16 (identification) / 32 (classification)
Image Size	112 × 112
Batch Size	4
Optimizer	Adam
Loss	Binary Crossentropy (ID) / Categorical Crossentropy (Class)
Epochs	15–20
Learning Rate	1e-4
Hardware	NVIDIA GPU recommended
📈 Results
🔹 Project 1 – Gesture Identification (G3 vs NON-G3)
Metric	Training	Validation
Accuracy	85.9%	91.1%
Loss	0.33	0.24

✅ The model successfully distinguishes G3 gestures from all other gestures.

🔹 Project 2 – Gesture Classification (G1, G2, G3, G4, G11)
Metric	Training	Validation
Accuracy	84.3%	93.9%
Loss	0.48	0.23

✅ The model generalizes well to multiple gesture types, learning fine-grained temporal motion patterns.

🔹 Confusion Matrix
| Actual → / Predicted ↓ | G1  | G2  | G3  | G4  | G11 |
| ---------------------- | --- | --- | --- | --- | --- |
| **G1**                 | 92% | 4%  | 2%  | 1%  | 1%  |
| **G2**                 | 3%  | 90% | 5%  | 2%  | 0%  |
| **G3**                 | 1%  | 4%  | 93% | 1%  | 1%  |
| **G4**                 | 0%  | 2%  | 3%  | 92% | 3%  |
| **G11**                | 0%  | 1%  | 2%  | 2%  | 95% |

Interpretation:

G3 and G4 gestures are easier to detect due to stronger motion cues

Subtle gestures (G2) may have minor confusion with adjacent gestures

The model captures both spatial orientation and temporal progression effectively

🧩 Use Cases

Surgical Skill Assessment – analyze gesture accuracy and efficiency

Robotic Surgery Automation – detect surgical task phases automatically

Training Systems – provide feedback to trainees

Video Annotation – automatically label surgical video
