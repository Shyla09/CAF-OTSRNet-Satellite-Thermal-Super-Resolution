# CAF-OTSRNet

## Cross-Attention Fusion Optical Guided Thermal Super-Resolution Network

CAF-OTSRNet is an advanced deep learning framework for generating high-resolution thermal imagery from low-resolution thermal inputs using complementary optical and texture information. The model combines cross-attention based multi-modal fusion, geometric alignment, and uncertainty-aware prediction to produce accurate, physically consistent, and artifact-resistant thermal super-resolution outputs.

---

## Live Demo

Demo URL:

https://huggingface.co/spaces/biconcavelens/civic-minds-demo

---

## Overview

Thermal satellite imagery often suffers from lower spatial resolution compared to optical imagery. CAF-OTSRNet addresses this challenge by leveraging high-resolution optical and texture information to reconstruct detailed thermal maps while preserving thermal consistency and minimizing artifacts.

Key capabilities include:

- Cross-attention based thermal-optical feature fusion
- Multi-modal learning using thermal, optical, and texture data
- Geometric alignment for sensor registration
- Artifact suppression through texture safety mechanisms
- Progressive multi-scale super-resolution
- Pixel-wise uncertainty estimation
- Physics-aware thermal reconstruction

---

## Using the Demo

### Step 1: Upload Input Data

Upload a preprocessed `.npz` patch containing the required thermal and optical inputs.

### Step 2: Run Inference

Click **Submit** to execute the super-resolution pipeline.

### Step 3: Analyze Results

The interface displays:

- Low-resolution thermal input
- Ground-truth thermal image
- CAF-OTSRNet super-resolved output
- Error visualization maps
- Quantitative performance metrics

### Evaluation Metrics

- RMSE (Root Mean Square Error)
- PSNR (Peak Signal-to-Noise Ratio)

---

## Model Architecture

CAF-OTSRNet follows a five-stage architecture designed specifically for thermal image super-resolution.

### 1. Enhanced Geometric Alignment

Prior to fusion, optical and thermal modalities are spatially aligned using:

#### Affine Transformation

Learns global transformations including:

- Translation
- Rotation
- Scaling

#### Deformable Refinement

Predicts dense displacement fields for correcting local distortions and achieving sub-pixel registration accuracy.

---

### 2. Multi-Branch Feature Encoding

Three dedicated encoders extract modality-specific representations.

#### Thermal Encoder

Processes low-resolution thermal imagery through multi-scale residual blocks to preserve thermal structures.

#### Optical Encoder

Extracts contextual information from:

- 9 Optical Bands
- NDVI
- NDWI
- NDBI

Channel attention mechanisms prioritize the most informative spectral features.

#### Texture Encoder

Generates texture-aware descriptors using Sobel edge information derived from:

- Red Band
- Near Infrared (NIR) Band

---

### 3. Safe Multi-Modal Fusion

#### Cross-Attention Fusion

Thermal features act as queries while optical representations provide contextual guidance, enabling effective transfer of spatial detail.

#### Texture Safety Network

A reliability estimation module computes per-pixel safety scores to prevent the introduction of misleading optical textures into thermal predictions.

This significantly reduces reconstruction artifacts.

---

### 4. Progressive Super-Resolution Decoder

The decoder reconstructs high-resolution thermal imagery using a Laplacian Pyramid framework.

Resolution progression:

```text
32 × 32
   ↓
64 × 64
   ↓
128 × 128
```

Each stage predicts residual details that refine the reconstruction and preserve fine-scale thermal structures.

Skip connections from encoder stages ensure information retention across scales.

---

### 5. Multi-Head Prediction System

#### Super-Resolution Head

Generates the final high-resolution thermal image.

#### Uncertainty Head

Produces confidence estimates for each pixel, enabling reliability-aware analysis.

#### Emissivity Head (Optional)

Predicts emissivity maps that can be incorporated into physics-guided training objectives.

---

## Repository Structure

```text
CAF-OTSRNet/
│
├── app.py
├── caf-otsrnet.ipynb
├── requirements.txt
├── model_weights.pth
│
├── test npz files/
│   ├── patch_000000_64_64.npz
│   ├── patch_000001_0_0.npz
│   ├── patch_000001_0_128.npz
│   └── patch_000001_128_128.npz
│
└── README.md
```

---

## Installation

### Prerequisites

- Python 3.8+
- PyTorch
- Git

### Clone Repository

```bash
git clone https://github.com/Shyla09/CAF-OTSRNet-Satellite-Thermal-Super-Resolution.git
cd CAF-OTSRNet-Satellite-Thermal-Super-Resolution
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Running the Application

Launch the Streamlit interface:

```bash
streamlit run app.py
```

The application will open in your browser where you can upload `.npz` files and evaluate model predictions.

---

## Sample Test Files

Example `.npz` test patches are provided in:

```text
test npz files/
```

These files can be directly uploaded into the demo interface for evaluation.

---

## Applications

- Satellite thermal image enhancement
- Environmental monitoring
- Urban heat island analysis
- Precision agriculture
- Infrastructure inspection
- Climate studies
- Remote sensing analytics

---

## Technical Highlights

- Multi-modal thermal-optical fusion
- Cross-attention based feature interaction
- Sensor alignment and registration
- Texture-aware artifact suppression
- Progressive Laplacian Pyramid reconstruction
- Uncertainty estimation for reliability assessment
- Physics-aware thermal modeling

---

## License

This project is intended for research, educational, and demonstration purposes.

---
CAF-OTSRNet Development Team

Cross-Attention Fusion Optical Guided Thermal Super-Resolution for Satellite Remote Sensing.
