# 🦴 Smart Spine - Your AI Posture Health Guardian

> "Let Smart Spine be the one who knows your back best."
> **Smart Spine** is a real-time posture monitoring system based on computer vision, designed to address spinal health issues caused by prolonged sitting. This project originated from the **NTHU Leader AI Winter Workshop**, implementing a full-stack development workflow from data collection and feature engineering to model deployment.

---

## Project Contributors

Frey (Wei-Cheng) Fu - frey.50302.fu.123@gmail.com<br>
Yuan-Ting (Jimmy) Tiao - tjimmy0113@gmail.com<br>
Alvin - ooii8929@gmail.com

---

## 💡 Project Demo

[https://youtu.be/kE5gtMvK_TI](https://youtu.be/kE5gtMvK_TI) <br>
[https://drive.google.com/file/d/11X3Vzp-c48s-IwMnMFBf-W5gu10aM6xj/view?usp=sharing](https://drive.google.com/file/d/11X3Vzp-c48s-IwMnMFBf-W5gu10aM6xj/view?usp=sharing)

---

## 💡 Project Highlights

* **Keypoint Detection Technology**: Utilizes **PoseNet** to detect 17 human keypoints, with specific optimizations for seated scenarios.
* **High-Dimensional Feature Engineering**: Integrates keypoint coordinates with image area features, expanding into a **14,739-dimensional** feature vector to capture subtle postural differences.
* **Lightweight Deployment**: Implemented via Web technology. No environment installation is required; inference can be performed directly in a browser for an optimized user experience.

---

## 🛠 Technical Architecture

### System Analysis Workflow

The system analyzes core nodes of the upper body to accurately determine whether a subject is in a "Correct Posture" or "Incorrect Posture."

| Phase | Description |
| --- | --- |
| **Video Input** | Real-time streaming input via WebCam or static images. |
| **Keypoint Detection** | Extracts 17 body keypoints (facial features, shoulders, elbows, hips, etc.) using **PoseNet**. |
| **Feature Flattening** | Combines keypoint coordinates and local image features into a **14,739-dimensional feature vector**. |
| **Classification Inference** | Passed into a custom neural network classifier for Binary Classification. |
| **Result Output** | Real-time feedback on correct/incorrect probability with reminders to adjust posture. |

---

## 🧠 Model Architecture

To maintain high performance and accuracy on the web, we designed a streamlined yet powerful MLP (Multi-Layer Perceptron):

* **Input Layer**: 14,739 Features
* **Dense Layer 1**: 100 Neurons (ReLU activation)
* **Regularization**: Dropout (50%) - *Effectively prevents overfitting and improves generalization.*
* **Output Layer**: 2 Neurons (Softmax activation) - *Outputs the probability distribution for correct and incorrect postures.*

---

## 📊 Keypoint Definition (17 Keypoints)

The 17 core endpoints monitored by the system are as follows:

| ID | Body Part | ID | Body Part |
| --- | --- | --- | --- |
| 0 | Nose | 9-10 | Left/Right Wrists |
| 1-2 | Left/Right Eyes | 11-12 | Left/Right Hips |
| 3-4 | Left/Right Ears | 13-14 | Left/Right Knees |
| 5-6 | Left/Right Shoulders | 15-16 | Left/Right Ankles |
| 7-8 | Left/Right Elbows |  |  |

---

## 🚀 Quick Start

Developed with Web technology, this project supports instant execution:

1. **Clone the Repository**

```bash
git clone https://github.com/your-username/smart-spine.git
cd smart-spine

```

2. **Start a Local Server** (Python recommended)

```bash
python -m http.server 8000

```

3. **Run the Application**
Open `http://localhost:8000/posture_detection.html` in your browser.

---

## 📁 File Descriptions

* `posture_detection.html`: Core application, integrating PoseNet and the Teachable Machine inference engine.
* `posture_detection_architecture.docx`: Detailed technical specifications and product planning document.
* `README.md`: Project overview and development documentation.

---

## 🤝 References

* **Dataset Source**: [Human Pose Dataset](https://dayta.nwu.ac.za/articles/dataset/Human_pose_dataset_sit_stand_pose_classes_/23290937)
* **Training Platform**: [Teachable Machine](https://teachablemachine.withgoogle.com/train)
* **Technical Reference**: [Building Pose Analysis System (OpenCV)](https://learnopencv.com/building-a-body-posture-analysis-system-using-mediapipe/)