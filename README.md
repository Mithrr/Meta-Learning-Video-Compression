# Meta-Learning-Video-Compression
A meta-learning–based video compression project that improves motion compensation across multiple video domains using the Reptile algorithm. The system combines classical optical flow with a lightweight neural residual refinement network to learn adaptive motion representations for both cartoon (ATD-12) and live-action human activity videos
A Reptile Meta-Learning Based Motion Compensation Network for Video Compression

**Overview**

This project presents a meta-learning–based motion compensation framework designed to improve adaptive video compression across multiple video domains. The system integrates classical optical flow, deep neural residual refinement, and the Reptile meta-learning algorithm to create a single generalized model capable of handling both cartoon/animation and live-action human activity videos.

Traditional video compression techniques rely on fixed motion estimation methods such as block matching and optical flow, which struggle with varying motion distributions across domains. This project addresses that limitation by training a Reptile-based model that learns generalizable motion priors capable of adapting quickly to different motion characteristics.

The framework was trained and evaluated on:

* ATD-12 Dataset — Cartoon / animation domain
* Human Activity Recognition (HAR) Dataset — Live-action domain

The proposed system focuses on:

* Motion compensation
* Residual minimization
* Frame reconstruction
* Compression-aware learning

rather than full codec implementation.

⸻

**Key Features**

* Multi-domain adaptive motion compensation
* Reptile-based meta-learning
* Cross-domain generalization
* Residual Flow Network (RFN)
* Optical-flow-guided refinement
* Frame reconstruction and residual analysis
* Compression-aware optimization
* PSNR and SSIM evaluation
* Residual energy minimization

⸻

**Problem Statement**

Traditional video compression algorithms use static motion estimation techniques that fail to adapt across different motion domains such as cartoons and real-world videos. Existing CNN-based systems often require retraining for each domain, limiting scalability and adaptability.

This project proposes a Reptile meta-learning–based motion compensation network capable of learning generalized motion representations across multiple domains, improving compression efficiency and reconstruction quality without retraining for each video type.

⸻

**Objectives**

* Design a Reptile-based adaptive motion compensation framework
* Integrate classical optical flow with neural refinement
* Train on both animation and live-action datasets
* Minimize residual energy for compression efficiency
* Improve reconstruction quality (PSNR / SSIM)
* Demonstrate cross-domain generalization
* Compare performance with traditional motion estimation approaches

⸻

**Project Architecture**

**Pipeline**

Video Dataset (ATD-12 + HAR)
        ↓
Frame Extraction & Preprocessing
        ↓
Initial Motion Estimation (Farnebäck Optical Flow)
        ↓
Residual Flow Network (RFN)
        ↓
Reptile Meta-Learning
        ↓
Frame Reconstruction
        ↓
Residual Computation
        ↓
Compression Evaluation

⸻

**Datasets Used**

**_1. ATD-12 Dataset_**

Type:

Animation / Cartoon

Purpose:

Used to train the model on:

* Stylized motion
* Smooth exaggerated transitions
* Low-texture cartoon movement

Characteristics:

* Animation triplets
* Non-rigid cartoon motion
* Smooth temporal changes

⸻

_**2. Human Activity Recognition (HAR) Dataset**_
Type:

Live-action / Human activity

Purpose:

Used to train the model on:

* Real-world articulated motion
* Human movement patterns
* Fine local motion changes

Characteristics:

* Walking
* Running
* Gestures
* Dynamic body motion

⸻

**Preprocessing Pipeline**

The preprocessing stage includes:

* Frame extraction
* Frame resizing (256×256)
* RGB normalization
* Optical flow computation
* Meta-task formation
* Data augmentation

Motion Prior

Farnebäck Optical Flow is used to generate:

* coarse motion vectors
* initial flow fields

These act as priors for neural refinement.

⸻

**Residual Flow Network (RFN)**

The Residual Flow Network is a lightweight U-Net–style CNN responsible for refining coarse motion estimation.

Inputs

* Previous frame
* Next frame
* Initial optical flow

Output

* Residual flow correction (ΔF)

Refined Flow Equation

F_refined = F_init + ΔF

⸻

**Reptile Meta-Learning**

Why Reptile?

Reptile was chosen because:

* First-order meta-learning
* Computationally lightweight
* Faster than MAML
* Learns generalized initialization
* Efficient adaptation across domains

⸻

Reptile Training Procedure

Inner Loop

Task-specific adaptation:

* Cartoon motion
* Human motion
* Rotation
* Fast motion
* Slow motion

Outer Loop

Meta-update:

θ ← θ + ε(θ′ − θ)

where:

* θ = global weights
* θ′ = task-adapted weights
* ε = meta learning rate

The model gradually learns a generalized initialization capable of adapting to different video motion distributions.

⸻

Frame Reconstruction

The model reconstructs the next frame using motion-compensated warping.

Reconstruction Process

1. Predict refined motion flow
2. Warp previous frame
3. Reconstruct next frame
4. Compute residual

Residual Equation

Residual = I(t+1) − Î(t+1)

Lower residual magnitude indicates:

* better motion prediction
* better compression efficiency

⸻

Loss Function

The training objective combines:

* photometric accuracy
* residual minimization
* smoothness regularization

L = L_photo + λ_r L_residual + λ_s L_smooth

Where:

* L_photo → reconstruction fidelity
* L_residual → compression proxy
* L_smooth → flow regularization

⸻

Training Configuration

Parameter	Value
Framework	PyTorch
Optical Flow	OpenCV Farnebäck
Resolution	256×256
Optimizer	Adam
Batch Size	6
Meta Iterations	200
Inner Steps	8–10
Inner Learning Rate	3e-3
Meta Learning Rate	0.2
Hardware	Google Colab GPU / Mac M2 Pro

⸻

**Results**

**Quantitative Results**

Domain	PSNR	SSIM	Residual Reduction
ATD-12 (Cartoon)	34.07 dB	0.914	~30%
HAR (Live Action)	32.83 dB	0.901	~22%

⸻

**Qualitative Results**

The framework successfully:

* reconstructed future frames
* reduced temporal prediction error
* generated smoother optical flow
* minimized residual maps

Visual outputs include:

* reconstructed frames
* residual maps
* optical flow visualizations
* predicted vs actual comparisons

⸻

**Key Contribution**

Unlike traditional compression systems that use:

* fixed motion estimation
* domain-specific CNNs

this project introduces:

A SINGLE META-LEARNED MODEL

capable of adapting across:

* cartoons
* animation
* human activity
* live-action videos

using:

Reptile-based adaptive motion compensation.

⸻

**Technologies Used**

* Python
* PyTorch
* OpenCV
* NumPy
* Matplotlib
* Google Colab
* GitHub

⸻

**Repository Structure**

project/
│
├── notebooks/
│   └── reptile_motion_comp.ipynb
│
├── datasets/
│   ├── ATD12/
│   └── HAR/
│
├── outputs/
│   ├── reconstructed_frames/
│   ├── residual_maps/
│   └── optical_flow/
│
├── checkpoints/
│   └── reptile_model.pth
│
├── figures/
│
├── README.md
├── requirements.txt
└── .gitignore

⸻

**Future Work**

* Integrate with HEVC / VVC codecs
* Add entropy coding
* Real bitrate optimization
* Train on larger datasets (UCF101, HEVC)
* Explore MAML / Meta-SGD
* Real-time encoder deployment
* Hardware acceleration (FPGA / CUDA)

⸻

**Authors**

* Mitrajith K
* Priyadharshini D
* Reshma B
* Viswanathan G

Department of Artificial Intelligence and Data Science
VIT University

