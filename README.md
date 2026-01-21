Here is a professional `README.md` for your project. You can copy this code and save it as a file named `README.md` in your project folder.

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
├── tennis_courts/              # Main dataset folder
│   ├── clay/                   # Training images for Clay
│   ├── grass/                  # Training images for Grass
│   ├── hard/                   # Training images for Hard
│   └── unknown/                # Auto-generated "junk" images
├── test_images_set/            # Separate images for final testing
├── TennisClassifier.mlpackage/ # The compiled CoreML model (Output)
├── Tennis_courts_image_classification.ipynb # Main Jupyter Notebook
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

1. **Prepare Data:**
Ensure your `tennis_courts` folder has the three subfolders: `clay`, `grass`, `hard` containing your training images.
2. **Open the Notebook:**
Launch `Tennis_courts_image_classification.ipynb` in VS Code.
3. **Step 1: Download "Unknown" Data:**
Run **Block A**. This automatically downloads the *Imagenette* dataset and populates the `unknown` folder with random images. This prevents the "Closed World" problem where the AI forces every image to be a tennis court.
4. **Step 2: Train the Model:**
Run **Block B**. This loads the 4 classes and fine-tunes the ResNet18 model.
* *Note:* The script forces execution on the CPU (`defaults.device = 'cpu'`) to ensure stability on macOS.


5. **Step 3: Test:**
Run the testing blocks to verify accuracy on the `test_images_set` folder.
6. **Step 4: Export:**
Run the final block to generate `TennisClassifier.mlpackage`.

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

```
