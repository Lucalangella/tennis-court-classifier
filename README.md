```markdown
# 🎾 Tennis Court Surface Classifier

A Deep Learning model built with **FastAI** and **PyTorch** to automatically detect tennis court surfaces (Clay, Grass, Hard). The model is designed to handle invalid inputs via a "Smart Unknown Class" and exports directly to **CoreML** for use in iOS apps.

## 🚀 Features

* **Multi-Class Classification:** Accurately identifies `Clay`, `Grass`, and `Hard` courts.
* **Smart "Unknown" Handling:** Includes a robust 4th class ("Unknown") trained on random images to reject non-tennis photos (e.g., selfies, pets, cars).
* **Transfer Learning:** Uses a **ResNet18** architecture pretrained on ImageNet for high accuracy with small datasets.
* **CoreML Ready:** Automatically exports to `.mlpackage` format for easy integration into Xcode/Swift.
* **MacOS Optimized:** Includes specific configurations to prevent GPU/MPS crashes on Apple Silicon (M1/M2/M3) chips.

## 📂 Project Structure

```text
.
├── notebooks/                  # Contains the training code
│   ├── train_model_colab.ipynb # Cloud version
│   └── train_model_local.ipynb # Local VS Code version
├── tennis_courts/              # Main dataset folder
│   ├── clay/
│   ├── grass/
│   ├── hard/
│   └── unknown/
├── test_images_set/            # Separate images for final testing
├── requirements.txt            # Python dependencies
└── README.md

```

## 🛠️ Prerequisites

* Python 3.9+
* VS Code (recommended) or Jupyter Notebook

### Required Libraries

Install the dependencies using pip:

```bash
pip install fastai torch torchvision coremltools ipywidgets

```

## 🏃‍♂️ How to Run

* **Prepare Data:**
<br> Ensure your `tennis_courts` folder has the three subfolders: `clay`, `grass`, `hard` containing your training images.
* **Open the Notebook:**
<br> Launch `Tennis_courts_image_classification.ipynb` in VS Code.
* **Step 1: Download "Unknown" Data:**
<br> Run **Block A**.
<br>This automatically downloads the *Imagenette* dataset and populates the `unknown` folder with random images. This prevents the "Closed World" problem where the AI forces every image to be a tennis court.
* **Step 2: Train the Model:**
<br>Run **Block B**. This loads the 4 classes and fine-tunes the ResNet18 model.
<br> *Note:*
<br>The script forces execution on the CPU (`defaults.device = 'cpu'`) to ensure stability on macOS.


* **Step 3: Test:**
<br> Run the testing blocks to verify accuracy on the `test_images_set` folder.
* **Step 4: Export:**
<br> Run the final block to generate `TennisClassifier.mlpackage`.

## 📱 CoreML Model Specs

The generated `TennisClassifier.mlpackage` is ready for iOS.

* **Input:** Color Image (RGB)
* **Resolution:** 224 x 224 px
* **Preprocessing:** Standard ImageNet Normalization (handled automatically by the model).
* **Output:** Dictionary of probabilities for labels: `['clay', 'grass', 'hard', 'unknown']`.

## ⚠️ Troubleshooting macOS

If you encounter `RuntimeError: Found two devices, mps:0 and cpu!`:

* This project is configured to bypass the Mac GPU (MPS) bug by forcing the model to the CPU.
* Ensure the top cell contains: `defaults.device = torch.device('cpu')`.


# 🎾 AI Tennis Court Classifier

**Classify tennis court surfaces (Clay, Grass, Hard) using Deep Learning.**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Lucalangella/tennis-court-classifier/blob/main/notebooks/train_model_colab.ipynb)

This project compares two approaches to training a Computer Vision model using **FastAI** and **PyTorch**:
1.  **Local Training:** Running on a Mac (M1/M2) with VS Code.
2.  **Cloud Training:** Running on Google Colab with NVIDIA GPUs.

*Read the full story on Medium: [Link to your future article]*

---

## 📂 Repository Structure

* `notebooks/`
    * `train_model_colab.ipynb` → The cloud-optimized version (handling "Dependency Hell" & Linux file sorting).
    * `train_model_local.ipynb` → The local version (optimized for Mac/VS Code).
* `tennis_courts/` → The dataset (organized by class).
* `test_images_set/` → Unseen images used for the final exam.

---

## 🚀 How to Run the Code

### Option 1: The Easy Way (Google Colab)
No installation required. Runs entirely in your browser using free GPUs.

1.  Click the **"Open in Colab"** badge above.
2.  Run **Block 1** to set up the environment (this handles the NumPy/FastAI version fixes automatically).
3.  Run the training blocks to see the model in action.

### Option 2: The Local Way (VS Code)
If you want to run this on your own machine:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Lucalangella/tennis-court-classifier.git](https://github.com/Lucalangella/tennis-court-classifier.git)
    cd tennis-court-classifier
    ```

2.  **Install Dependencies:**
    Make sure you have Python installed, then run:
    ```bash
    pip install fastai torch torchvision
    ```

3.  **Run the Notebook:**
    Open `notebooks/train_model_local.ipynb` in VS Code and select your Python kernel.

---

## 📊 The "0% vs 20% Error" Mystery

You might notice different results depending on where you train:

| Environment | Typical Error Rate | Why? |
| :--- | :--- | :--- |
| **VS Code (Mac)** | **~0% (Suspiciously Perfect)** | Mac file sorting + small Batch Size (16) allowed the model to "memorize" the easy validation set. |
| **Google Colab** | **~20% (More Realistic)** | Linux file sorting + larger Batch Size (32) forced the model to confront "tricky" images (e.g., green forests looking like grass courts). |

**Conclusion:** The Colab model is actually "smarter" because it learned not to trust every green pixel it sees!

---

## 🛠 Tech Stack
* **FastAI** (Deep Learning Library)
* **PyTorch** (Underlying Framework)
* **CoreML** (Export format for iOS)
* **ResNet18** (Pre-trained Architecture)
