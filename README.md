# Deep Learning-Based CNN and PLC Integration for Real-Time Industrial Defect Detection

**Turkish Title:** GERÇEK ZAMANLI ENDÜSTRİYEL HATA TESPİTİ İÇİN DERİN ÖĞRENME TABANLI CNN VE PLC ENTEGRASYONU

## Overview

This is a comprehensive master's degree thesis project implementing an intelligent quality control system for industrial manufacturing. The system integrates deep learning (Convolutional Neural Networks) with Siemens PLC (Programmable Logic Controller) for real-time defect detection and classification.

**Key Innovation:** Dual-channel production line monitoring with visual explanations (Grad-CAM) showing exactly where defects are detected.

---

## Core Features

### 🤖 Deep Learning
- **CNN Architecture:** Multi-layer convolutional neural network optimized for casting defect detection
- **Real-Time Inference:** ~200ms end-to-end (E2E) latency per part
- **Data Augmentation:** Rotation, shift, zoom, and horizontal flip for robustness
- **Grad-CAM Visualization:** XAI (Explainable AI) heatmaps showing defect locations
- **Multi-Metric Evaluation:** Accuracy, Precision, Recall, F1-Score, AUC

### 🏭 Industrial Integration
- **PLC Communication:** Siemens S7-1200/1500 & S7-300/400 via SNAP7 protocol
- **Dual-Channel Processing:** Simultaneous inspection of two production lines (CH1 & CH2)
- **File-Based Image Pipeline:** Watchdog-based file system monitoring
- **Status Signaling:** Real-time PLC register writes (OK=1, NOK=2, RESET=0)

### 📊 User Interface
- **Live Dashboard:** Dual-channel real-time visualization
- **Original + AI Heatmap Display:** Side-by-side comparison
- **Training Interface:** Hyperparameter tuning & epoch-by-epoch monitoring
- **Log Viewer:** Complete operation history with timestamps
- **PLC Settings Panel:** Easy configuration for different S7 models

### 📈 Quality Metrics
- **Per-Channel Statistics:** OK/NOK count tracking
- **Performance Dashboard:** Precision, Recall, F1-Score
- **E2E Latency Tracking:** Average and per-part processing time
- **Epoch History Viewer:** Training progress visualization

---

## Technology Stack

| Component | Technology |
|-----------|------------|
| **ML Framework** | TensorFlow/Keras 2.20+ |
| **Computer Vision** | OpenCV |
| **PLC Communication** | SNAP7 (S7 Protocol) |
| **GUI Framework** | Tkinter |
| **Image Processing** | Pillow (PIL) |
| **File Monitoring** | Watchdog |
| **Data Processing** | NumPy, Pandas |
| **Language** | Python 3.10+ |
| **OS** | Windows 10/11 (tested) |

---


