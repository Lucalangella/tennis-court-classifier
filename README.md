
# 🎾 AI Tennis Court Surface Classifier

**A "Practical Deep Learning for Coders" (FastAI) Project**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Lucalangella/tennis-court-classifier/blob/main/notebooks/train_model_colab.ipynb)

This project is a real-world experiment comparing **Local Training (VS Code on Mac)** vs. **Cloud Training (Google Colab)**. It classifies tennis court surfaces (Clay, Grass, Hard) and handles invalid inputs using a "Smart Unknown" class.

*Read the full story on Medium: [Link to your future article]*

---

## 🚀 The Experiment: Local vs. Cloud
I built this project twice to test different environments. The results were surprising:

| Feature | Local (VS Code/Mac) | Cloud (Google Colab) |
| :--- | :--- | :--- |
| **Setup** | Complex (Virtual Envs, PyTorch) | Zero (One-click) |
| **Error Rate** | **~0%** (Suspiciously Perfect) | **~20%** (Realistic) |
| **The Lesson** | Small batch sizes (16) + static local files led to **overfitting**. | Larger batch sizes (32) + random web data created a **robust** model. |

---

## 📂 Project Structure

```text
.
├── notebooks/                  # Training Code
│   ├── train_model_colab.ipynb # Cloud Version (Optimized for Linux/T4 GPU)
│   └── train_model_local.ipynb # Local Version (Optimized for Mac M1/M2)
├── tennis_courts/              # Dataset
│   ├── clay/
│   ├── grass/
│   ├── hard/
│   └── unknown/                # "Junk" class (random images)
├── test_images_set/            # Unseen images for final exam
├── requirements.txt            # Dependencies for local run
└── README.md
🛠️ Features
Smart "Unknown" Class: Automatically downloads random images (Imagenette) to teach the AI that "A Forest is not a Grass Court."

CoreML Export: Generates a .mlpackage file ready for iOS apps.

Architecture: Fine-tuned ResNet18 (Transfer Learning).

🏃‍♂️ How to Run
Option 1: Google Colab (Recommended)
Best for: Quick testing, free GPU, no installation.

Click the "Open in Colab" badge at the top.

Run Block 1 to set up the environment (this handles the NumPy/FastAI version fixes automatically).

Run all blocks to train and export the model.

Option 2: Local VS Code (Mac/Linux)
Best for: Building a permanent app, working offline.

Clone the Repo:

Bash

git clone [https://github.com/Lucalangella/tennis-court-classifier.git](https://github.com/Lucalangella/tennis-court-classifier.git)
cd tennis-court-classifier
Install Dependencies:

Bash

pip install -r requirements.txt
Run: Open notebooks/train_model_local.ipynb and execute the cells.

⚠️ Troubleshooting
"Found two devices, mps:0 and cpu!" (Mac): The local notebook is configured to force CPU usage to avoid Apple Silicon MPS bugs.

Dependency Conflicts (Colab): Use the train_model_colab.ipynb file; it includes a specific "Time Machine" block to downgrade NumPy to a compatible version.
