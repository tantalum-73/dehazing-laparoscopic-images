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

## 📊 Dataset: DeSmoke-LAP

This project utilizes the [DeSmoke-LAP dataset](https://www.ucl.ac.uk/interventional-surgical-sciences/weiss-open-research/weiss-open-data-server/desmoke-lap), a publicly available benchmark designed for developing and evaluating smoke removal algorithms in laparoscopic surgery.&#8203;:contentReference[oaicite:0]{index=0}

### 📁 Dataset Composition

- **Source**: 10 robot-assisted laparoscopic hysterectomy procedure videos.
- **Frame Extraction**: Videos were decomposed into frames at 1 frame per second (fps).
- **Image Selection**: From each video:
  - 300 hazy images
  - 300 clear images  
  These were selected based on manual observation of electrocauterisation events.
- **Test Clips**: Short video clips of 50 frames from each procedure were extracted and used for testing.
- **Evaluation**:
  - 5-fold cross-validation was performed for all methods.
  - Quantitative evaluation was done using referenceless metrics.
  - Qualitative evaluation was conducted through surveys completed by surgeons.

### 📥 Download & License

- **Download**: The dataset is available from the [UCL WEISS Open Data Server](https://www.ucl.ac.uk/interventional-surgical-sciences/weiss-open-research/weiss-open-data-server/desmoke-lap).
- **License**: Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0).


### 📚 Citation

> Pan, Y., Bano, S., Vasconcelos, F., Park, H., Jeong, T. T., & Stoyanov, D. (2022).  
> *DeSmoke-LAP: Improved unpaired image-to-image translation for desmoking in laparoscopic surgery*.  
> International Journal of Computer Assisted Radiology and Surgery.  
> [https://doi.org/10.1007/s11548-022-02595-2](https://doi.org/10.1007/s11548-022-02595-2)

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
