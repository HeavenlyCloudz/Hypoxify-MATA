# Hypoxify MATA
**Microwave Acoustic Thermoacoustic Array for Pancreatic Hypoxia Stratification**

## 📌 Overview
Hypoxify MATA is a wearable, non-invasive microwave-induced thermoacoustic tomography (MITT) system designed to map pancreatic tumor hypoxia. It is a surveillance-adjunct tool intended for high-risk individuals already undergoing pancreatic cancer screening, aiming to provide a label-free alternative to PET radiotracers and invasive biopsies.

## 🔬 The Clinical Gap
Pancreatic ductal adenocarcinoma (PDAC) is one of the most hypoxic solid tumors. Hypoxia drives chemoresistance and metastasis. Current surveillance methods (MRI/EUS) detect structural abnormalities but cannot measure oxygenation status. FAZA-PET can measure hypoxia but is expensive, requires a radiotracer, and is not standard of care. Hypoxify addresses this by utilizing the endogenous dielectric contrast of hypoxic tissue.

## ⚙️ System Architecture
The system is a dual-pack wearable device designed to target the retroperitoneal pancreas:
*   **Hardware:** 6 UWB antennas (840 MHz–2 GHz), 6 PZT acoustic sensors (1–2 MHz), a Raspberry Pi 5, a NanoVNA-F V2, and an AD9226 high-speed ADC (65 MSPS) controlled by a Raspberry Pi Pico 2.
*   **Geometry:** A piecewise semi-circular arc (plywood frame) with a measured dielectric profile, ensuring local normal incidence for microwave illumination.
*   **Signal Processing:** Receiver-pair-pruned Cross-Correlation Beamforming (CCBF) to suppress non-coherent noise (e.g., bowel gas scattering), followed by Time-Gain Compensation (TGC) based on a weighted tissue attenuation model (0.55 dB/cm/MHz).

## 🧠 The Algorithm: VW-EE-PINN
The core innovation is the Virtual Wave Edge-Enhanced Physics-Informed Neural Network. 
*   **The Physics Problem:** Deep-tissue acoustic attenuation irreversibly destroys high-frequency information. 
*   **The Solution:** The network amortizes the regularized Virtual Wave inverse problem, predicting a lossless 3D virtual wave volume in a single forward pass.
*   **The Loss Function:** Constrained by the acoustic wave equation (Westervelt form), a Picard-consistency data term, and a novel dielectric–oxygen coupling constraint.
*   **The Output:** A 3D Spatial Hypoxia Probability Density Function and a scalar Hypoxia Score (0–100%), interpretable via SHAP and Integrated Gradients.

## 🧪 Validation Pipeline
1.  **Synthetic:** VW-EE-PINN reconstruction accuracy on simulated MITT signals (>85% IoU).
2.  **Phantom (The Critical Experiment):** Agar phantoms with sodium sulfite (oxygen scavenger) to establish the dielectric-to-oxygen calibration curve and demonstrate statistically significant separation between normoxic and hypoxic states.
3.  **Dielectric Probe:** Validating permittivity/conductivity shifts against oxygen concentration.
4.  **Ex Vivo:** Porcine pancreas models with injected hypoxic gels.
5.  **Usability:** IRB-approved healthy volunteer trials (<5 min scan time).

## 📂 Repository Structure
*   `/hardware`: CAD files for the plywood arc, PCB schematics for the dual-pack harness.
*   `/firmware`: Pico 2 PIO/DMA C-code for the AD9226 ADC acquisition.
*   `/software`: Python pipeline for CCBF, TGC, and VW-EE-PINN inference.
*   `/data`: Simulated k-Wave training sets and phantom characterization data.

## 🚀 Current Status (Nov 2026)
*   Hardware components received (Pico 2, AD9226, PZTs).
*   Plywood block templates finalized.
*   Next milestone: Serial ADC validation and PZT soldering.

## 👩🏽‍🔬 Author
**Anie Udofia** 
Grade 11, William Aberhart High School (Calgary, AB) 
*Project Mentorship: Dr. Elise Fear (NSERC Chair in Microwave Imaging, University of Calgary).*
