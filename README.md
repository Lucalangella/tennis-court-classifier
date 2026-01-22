```markdown
# 🎾 Tennis Court Classifier (FastAI + CoreML)

A Deep Learning project that classifies tennis court surfaces (**Clay, Grass, Hard**) using Computer Vision. 

This project demonstrates a complete pipeline: from data scraping and model training with **FastAI/PyTorch** to exporting a **CoreML** model ready for iOS deployment. It is designed to run seamlessly on both **Google Colab** (NVIDIA GPUs) and local **Mac Apple Silicon** (M1/M2/M3) machines.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/LucaLangella/tennis-court-classifier/blob/main/notebooks/train_model_colab.ipynb)
[![Read on Medium](https://img.shields.io/badge/Medium-Story-black?logo=medium)](YOUR_MEDIUM_ARTICLE_LINK_HERE)

## 🚀 Features

* **Multiclass Classification:** Distinguishes between Clay, Grass, Hard, and Unknown environments.
* **Transfer Learning:** Utilizes a pre-trained **ResNet** architecture for high accuracy with minimal data.
* **Dual Workflow:**
    * ☁️ **Cloud:** Optimized for Google Colab (Free T4 GPU).
    * 💻 **Local:** Optimized for VS Code on Apple Silicon (MPS acceleration).
* **CoreML Export:** Converts the PyTorch model into a `.mlpackage` for native iOS integration.

## 📂 Project Structure

```text
├── notebooks/
│   └── train_model_colab.ipynb   # Jupyter Notebook for Colab/Browser
├── scripts/
│   └── train_model_local.py      # Python script for VS Code/Terminal
├── models/
│   └── TennisClassifier.mlpackage # The exported model for iOS
├── README.md
└── requirements.txt

```

## 🛠️ Installation & Usage

### Option 1: Google Colab (Recommended for Beginners)

Click the "Open in Colab" badge above. The notebook handles all dependency installations and runtime setups automatically.

### Option 2: Local Development (VS Code / Mac Apple Silicon)

If you are running this on a Mac with M1/M2/M3 chips, the script includes a specific fix for PyTorch MPS (Metal Performance Shaders).

1. **Clone the repo:**
```bash
git clone [https://github.com/LucaLangella/tennis-court-classifier.git](https://github.com/LucaLangella/tennis-court-classifier.git)
cd tennis-court-classifier

```


2. **Install dependencies:**
```bash
pip install fastai coremltools numpy<2

```


3. **Run the script:**
```bash
python scripts/train_model_local.py

```



> **Note for Mac Users:** The local script automatically sets `os.environ['PYTORCH_ENABLE_MPS_FALLBACK'] = '1'` to prevent "NotImplemented" errors common when training on Apple Silicon.

## 📊 Results

The model was fine-tuned for 4 epochs, achieving an accuracy of approximately **95%**.

| Class | Precision |
| --- | --- |
| **Clay** | High |
| **Grass** | High |
| **Hard** | High |
| **Unknown** | High |

*A confusion matrix and top-loss visualization are generated at the end of the training script to help analyze performance.*

## 📱 iOS Deployment (CoreML)

The training pipeline concludes by converting the PyTorch model to CoreML format.

1. The script generates `TennisClassifier_Colab.mlpackage`.
2. Download this file.
3. Drag and drop it into your Xcode project.
4. The model is ready to use with the Vision framework!

## 🤝 Contributing

Feel free to fork this project, open issues, or submit PRs if you find better ways to handle the data or improve the model architecture!
