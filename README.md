# NeuroNetFlow
A MATLAB-based software toolbox for integrated analysis of cerebrospinal fluid flow dynamics using phase-contrast MRI

## 1. Project Overview

NeuroNetFlow is an open-source, GUI-based MATLAB software toolbox designed for the integrated analysis of cerebrospinal fluid (CSF) dynamics using phase-contrast MRI (PC-MRI) in combination with cardiorespiratory physiological signals.

Cerebrospinal fluid plays a critical role in maintaining central nervous system homeostasis, including mechanical buffering, buoyancy, and metabolic waste clearance. While CSF flow has traditionally been attributed primarily to cardiac-driven pulsatility, accumulating evidence highlights respiration as a major contributor to CSF circulation through venous return mechanisms. Importantly, breathing patterns in humans are highly variable and can be voluntarily modulated, offering a potential non-invasive pathway to influence CSF dynamics.

Recent advances in velocity-encoded MRI enable the direct quantification of both cardiac and respiratory components of CSF motion. However, comprehensive analysis remains challenging due to the limited availability of open-source tools that integrate PC-MRI data with physiological recordings in an accessible graphical environment. NeuroNetFlow addresses this gap by providing a modular, user-friendly GUI that substantially reduces manual coding effort while ensuring reproducibility and transparency.


## 2. Installation

### Step 1: Download
```bash
git clone https://github.com/SeokbeenLim/NeuroNetFlow.git
```
### Step 2: Add MATLAB Path
```bash
addpath(genpath(pwd));
savepath;
```
### Step 3: Launch
```bash
Breathing_PCMRI_GUI_Ver1
```


## 3. Pipeline Overview
NeuroNetFlow follows a predefined yet flexible analysis pipeline:

### Input

NeuroNetFlow is specifically designed, validated, and tested using **phase-contrast MRI (PC-MRI) data acquired from Philips MRI scanners**. At the current stage, compatibility is limited to Philips data formats.

**Imaging Data**
- Format: NIfTI (`.nii`)
- Required files:
  - Magnitude image (`.nii`)
  - Phase image (`.nii`)
- Acquisition: Phase-contrast MRI (PC-MRI) from Philips scanners
- Notes:
  - The software assumes Philips-specific phase scaling and metadata conventions.
  - Data from other vendors (e.g., Siemens, GE) have **not been tested** and are not currently supported.

**Physiological Data**
- Format: Philips physiology log file (`.log`, SCANPHYSLOG)
- Required signals:
  - Respiratory belt signal
  - Photoplethysmography (PPG)
  - System marker channels
- Characteristics:
  - Time-stamped physiological recordings synchronized with the MRI acquisition
  - Parsed using a dedicated Philips log reader implemented within NeuroNetFlow

### Processing features
**Module 1: Image Processing**
- PC-MRI Input Handling
- Automated CSF Segmentation
- Interactive ROI Refinement
- Background Phase Calibration
- Physiological Signal Import and Synchronization

**Module 2: Signal Analysis**
- Respiratory Signal Processing
- CSF Dynamics Quantification
- Spectral Decomposition of CSF Signals
- Cardiac Signal Processing
- Integrated Multi-Signal Visualization
- Breathing-Cycle Normalization

### Output and Exported Features

NeuroNetFlow exports all processed signals and quantitative features in formats optimized for downstream statistical analysis. Outputs can be saved as MATLAB `.mat` files for full signal access and as structured `.xlsx` tables for group-level analysis across participants.

**Output Formats**
- MATLAB `.mat`: Preprocessed signals, intermediate results, and extracted features
- Excel `.xlsx`: Participant-wise feature tables for statistical analysis

**Feature Categories**

- A. Temporal CSF Velocity Features (PC-MRI; Temporal Domain)
- B. Temporal CSF Flow-Rate Features (Velocity → Flow Rate)
- C. Respiration-Phase–Resolved Integrated Flow Features
- D. Volume Displacement Stability and Detrending Diagnostics
- E. Spectral CSF Features (Respiratory and Cardiac Bands)
- F. Respiratory Timing Features
- G. Breathing-Cycle–Normalized Features (0–100% Cycle)

## 4. Key Features

- GUI-based integrated analysis of PC-MRI and physiological data
- Semi-automatic CSF ROI segmentation with interactive mask editing
- Static tissue-based phase calibration for velocity correction
- Extraction of cardiac- and respiratory-driven CSF components
- Time- and frequency-domain analysis of CSF and physiology signals
- Modular App Designer architecture supporting extensibility


## 5. Software Architecture

NeuroNetFlow is built on a modular MATLAB App Designer architecture centered around a main control interface.

![NeuroNetFlow software architecture](figures/Fig_Software_Structure.png)

### Main Control Interface
- **Breathing_PCMRI_GUI_Ver1.mlapp**  
  Central hub for data loading, parameter configuration, and execution of CSF analysis workflows.

### Associated Sub-GUI Windows
- Analysis_further_window.mlapp – Advanced parameter tuning  
- Analysis_signals_window.mlapp – Time- and frequency-domain signal analysis  
- CSF_onecycle_Window.mlapp – Single respiratory cycle analysis  
- Calibration_window.mlapp – Static tissue-based calibration  
- Calibration_window_overall.mlapp – Global calibration validation  
- MagnitudeImgPlot.mlapp – Magnitude image and ROI inspection  
- Open_image_slide.mlapp – Multi-slice image viewer  

All dependencies were validated using MATLAB Dependency Analyzer.


## 6. System Requirements

| Category | Requirement |
|--------|-------------|
| Operating System | macOS (Apple Silicon, Sequoia 15.7.2 or later)<br>Windows 10 / 11 |
| Software | MATLAB R2023a or later |
| Hardware – Memory | Minimum 8 GB RAM (16 GB recommended) |
| Hardware – CPU | Intel Core i7 or later; Apple M2/M3 series |
| Display | 1920 × 1080 (Full HD) or higher recommended |
| Imaging Data | NIfTI (.nii) magnitude and phase images from Philips scanners |
| Physiological Data | Philips SCANPHYSLOG (.log) files |
