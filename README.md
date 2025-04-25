# Dehazing Laparoscopic Images using Diffusion + GANs

This project implements advanced image dehazing techniques using a hybrid of Generative Adversarial Networks (GANs) and Denoising Diffusion Probabilistic Models (DDPMs). Specifically, it targets smoke removal (desmoking) from laparoscopic surgery images to improve visual clarity for safer and more effective procedures.

## ✨ Motivation

Laparoscopic surgery often suffers from visual obstruction due to smoke produced by surgical instruments. Removing this haze is vital for:

- Improving surgeon visibility.
- Reducing operation risks.
- Enabling better computer vision analysis (e.g., segmentation, object detection).

## 📌 Problem Statement

Conventional dehazing methods (e.g., Dark Channel Prior) rely on fixed assumptions that break down under surgical conditions. This project addresses those limitations by:

- Using unpaired image-to-image translation.
- Introducing a novel hybrid of CycleGAN and a diffusion model (UNet2D).

## 🚀 Key Contributions

- 🔁 **CycleGAN Baseline:** Learns mapping between hazy and clear images using unpaired training data.
- 🌫️ **CycleGAN + Diffusion (Post-Processing):** Refines CycleGAN output with a standalone diffusion model.
- 💡 **Integrated CycleGAN-Diffusion Model:** Combines adversarial and denoising training into a unified architecture using a custom loss function.

## 🧠 Architecture Overview

- **Generators**: U-Net based, convert hazy ↔ clear images.
- **Discriminators**: CNNs to distinguish real vs. generated images.
- **Diffusion Model**: UNet2D with attention blocks, integrated via DDPMScheduler for iterative denoising.

### 📉 Loss Functions

- **Adversarial Loss**: GAN-based realism.
- **Cycle Consistency Loss**: Maintain round-trip image integrity.
- **Identity Loss**: Prevent over-editing.
- **Diffusion Loss**: Learn denoising trajectory.

## 🧪 Experiments

### Dataset

- Unpaired laparoscopic hazy and clear images.
- Images resized to `256x256` and augmented.

### Evaluation Metrics

| Metric | Description | Goal |
|--------|-------------|------|
| FADE   | Fog density | ↓ Lower is better |
| JNBM   | Visual sharpness | ↑ Higher is better |
| REA    | Edge preservation | ↓ Lower is better |

### Results Summary

| Model                 | FADE ↓ | JNBM ↑ | REA ↓ |
|----------------------|--------|--------|--------|
| **CycleGAN + Diffusion** | **2.17** | **24.98** | **9.80** |
| CycleGAN             | 2.57   | 36.15   | 7.56   |
| Cycle + Post Diffusion | 5.41 | 54.98   | 4.65   |

💥 The integrated model outperforms all baselines!

## 🧰 Installation
1. Clone the Repository:
```bash
git clone https://github.com/tantalum-73/dehazing-laparoscopic-images.git
cd dehazing-laparoscopic-images
```
2. Set Up the Environment:
   Ensure you have Python 3.7 or higher installed. It's recommended to use a virtual environment.
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```
3. Install Dependencies
```bash
pip install -r requirements.txt
```

## 📚Future Work
- Optimize diffusion loss and scheduling
- Scale to real-time applications
- Explore multi-domain haze scenarios (e.g., satellite, automotive)
- Tune hyperparameters and explore transformer-based GANs

## 🧑‍💻 Authors
- Rohan Reddy Pathi – pathi.r@northeastern.edu
- Vikramadithya Pabba - pabba.v@northeastern.edu
- Chaitanya Prudvi Balusu - balusu.c@northeastern.edu
- Param Madan - madan.pa@northeastern.edu
