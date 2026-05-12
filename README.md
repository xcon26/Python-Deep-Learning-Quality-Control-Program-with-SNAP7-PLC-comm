# Deep Learning-Based CNN and PLC Integration for Real-Time Industrial Defect Detection

**Turkish Title:** GERÇEK ZAMANLI ENDÜSTRİYEL HATA TESPİTİ İÇİN DERİN ÖĞRENME TABANLI CNN VE PLC ENTEGRASYONU

## Overview

This is a comprehensive master's degree thesis project implementing an intelligent quality control system for industrial manufacturing. The system integrates deep learning (Convolutional Neural Networks) with PLC (Programmable Logic Controller) communication for real-time defect detection in casting production.

**Key Innovation:** Dual-channel production line monitoring with visual explanations (Grad-CAM) showing exactly where defects are detected.
### Imprtant Note
- **Tested on simulation** Tested on Windows 11 Tia Portal V16 with PLCSIM V16 via NetToPLCim. 
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

## Dependencies & Libraries

### Core Libraries

#### 1. **TensorFlow/Keras 2.20.0** ⭐ Core Deep Learning
```
pip install tensorflow==2.20.0
```
- **Purpose:** Deep learning framework for CNN model building, training, and inference
- **Used For:**
  - Building convolutional neural network architecture
  - Training and validation of defect detection model
  - Grad-CAM visualization for explainable AI
  - Model saving/loading (.keras format)
- **Key Components:**
  - `tf.keras.models` - Model creation
  - `tf.keras.layers` - Conv2D, Dense, MaxPooling2D layers
  - `tf.keras.callbacks` - Training callbacks
  - `tf.GradientTape` - Grad-CAM gradient computation

#### 2. **NumPy >=1.24.0** 🔢 Numerical Computing
```
pip install numpy>=1.24.0
```
- **Purpose:** Fundamental numerical computing library
- **Used For:**
  - Array operations and mathematical computations
  - Image data manipulation and normalization
  - Grad-CAM heatmap calculations
  - Data preprocessing and augmentation

#### 3. **OpenCV (cv2) >=4.8.0** 📸 Computer Vision
```
pip install opencv-python>=4.8.0
```
- **Purpose:** Advanced image processing and computer vision
- **Used For:**
  - Reading and processing industrial images
  - Image resizing and normalization (300x300 format)
  - Grad-CAM heatmap overlay (cv2.applyColorMap)
  - Image weighted addition for visualization
  - Image I/O operations
- **Key Functions:**
  - `cv2.imread()` - Read images
  - `cv2.resize()` - Resize to model input size
  - `cv2.applyColorMap()` - Apply JET colormap to heatmaps
  - `cv2.addWeighted()` - Blend original and heatmap
  - `cv2.cvtColor()` - Color space conversion

#### 4. **Pillow (PIL) >=10.0.0** 🖼️ Image Processing
```
pip install pillow>=10.0.0
```
- **Purpose:** Python Imaging Library for advanced image handling
- **Used For:**
  - Image format conversion (numpy arrays to PhotoImage)
  - Image thumbnail generation for GUI display
  - ImageTk conversion for Tkinter display
- **Key Components:**
  - `PIL.Image` - Image creation and manipulation
  - `ImageTk.PhotoImage` - Convert PIL images to Tkinter format

#### 5. **python-snap7 >=1.2.0** 🏭 PLC Communication
```
pip install python-snap7>=1.2.0
```
- **Purpose:** SNAP7 library for communicating with Siemens PLCs
- **Used For:**
  - Connecting to Siemens S7-1200/1500 and S7-300/400 PLCs
  - Reading/writing data blocks (DB) from PLC memory
  - Sending defect detection results to PLC
  - Real-time status signaling (OK=1, NOK=2, RESET=0)
- **Key Components:**
  - `snap7.client.Client()` - PLC client connection
  - `db_write()` - Write results to PLC data block
  - `db_read()` - Read acknowledgment from PLC
  - `snap7.util` - Utility functions for data conversion

#### 6. **Watchdog >=3.0.0** 👁️ File System Monitoring
```
pip install watchdog>=3.0.0
```
- **Purpose:** File system event monitoring
- **Used For:**
  - Monitoring input folders for new images (KAMERA_1_GELEN, KAMERA_2_GELEN)
  - Automatic triggering of defect detection when images arrive
  - Asynchronous file processing without blocking GUI
- **Key Components:**
  - `FileSystemEventHandler` - Base handler for file events
  - `Observer` - Watch directory for changes
  - `on_created()` - Triggered when new image files appear

#### 7. **Pandas >=2.0.0** 📊 Data Processing
```
pip install pandas>=2.0.0
```
- **Purpose:** Data manipulation and analysis (optional, for future statistical analysis)
- **Used For:**
  - Processing quality control metrics
  - Creating reports and statistics tables
  - Data export functionality

### Built-in Python Libraries (No Installation Required)

#### System & OS
- **`sys`** - System-specific parameters and functions
- **`os`** - Operating system interfaces (file paths, directory operations)
- **`time`** - Time-related functions (performance timing, delays)
- **`logging`** - Event logging system for application tracking
- **`threading`** - Multi-threaded processing for concurrent operations
- **`shutil`** - High-level file operations (copying, moving)

#### GUI & User Interface
- **`tkinter`** - Python's standard GUI library for the entire UI
  - `tk` - Core widgets (Frame, Label, Button, Canvas)
  - `ttk` - Modern themed widgets (Notebook, Progressbar, Scrollbar)
  - `filedialog` - File selection dialogs
  - `messagebox` - Alert and confirmation dialogs

#### Data & Time
- **`datetime`** - Date and time handling for log timestamps
- **`queue`** - Thread-safe queue for async file processing
- **`random`** - Random number generation (utility functions)

---

## Installation & Setup

### Prerequisites
- **Python:** 3.10 or higher
- **pip:** Python package manager
- **System:** Windows 10/11 (tested on Windows)

### Quick Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/SafakBayraktar/Python-Deep-Learning-Quality-Control-Program-with-SNAP7-PLC-comm.git
   cd Python-Deep-Learning-Quality-Control-Program-with-SNAP7-PLC-comm
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Verify Installation**
   ```bash
   python -c "import tensorflow as tf; print(f'TensorFlow {tf.__version__}')"
   python -c "import cv2; print(f'OpenCV {cv2.__version__}')"
   python -c "import snap7; print('SNAP7 installed')"
   ```

### Manual Installation (if needed)
```bash
pip install tensorflow==2.20.0
pip install numpy>=1.24.0
pip install opencv-python>=4.8.0
pip install pillow>=10.0.0
pip install python-snap7>=1.2.0
pip install watchdog>=3.0.0
pip install pandas>=2.0.0
```

---

## Dependency Summary Table

| Library | Version | Purpose | Category |
|---------|---------|---------|----------|
| tensorflow | 2.20.0 | Deep learning framework | ML Core |
| numpy | ≥1.24.0 | Numerical computing | Data Processing |
| opencv-python | ≥4.8.0 | Computer vision | Image Processing |
| pillow | ≥10.0.0 | Image I/O & GUI | Image Processing |
| python-snap7 | ≥1.2.0 | PLC communication | Industrial |
| watchdog | ≥3.0.0 | File monitoring | System |
| pandas | ≥2.0.0 | Data analysis | Data Processing |
| tkinter | Built-in | GUI framework | UI |
| sys, os, time | Built-in | System utilities | Core |
| logging, threading | Built-in | Async & logging | Core |
| datetime, queue | Built-in | Data structures | Core |

---

## Project Structure

```
project_root/
├── requirements.txt                          # All dependencies
├── README.md                                 # This file
├── DL_QC_Final+TestResults.ipynb            # Main application (Jupyter Notebook)
├── besleme.ipynb                            # Data feeding/preprocessing notebook
│
├── dokum_hata_tespit_modeli.keras           # Trained CNN model
├── splash.png                               # Application splash image
├── kalite_kontrol.log                       # Application log file
│
├── KAMERA_1_GELEN/                          # Channel 1 input folder (watchdog monitored)
├── KAMERA_1_ARSIV_OK/                       # Channel 1 OK parts archive
├── KAMERA_1_ARSIV_NOK/                      # Channel 1 NOK parts archive
│
├── KAMERA_2_GELEN/                          # Channel 2 input folder (watchdog monitored)
├── KAMERA_2_ARSIV_OK/                       # Channel 2 OK parts archive
└── KAMERA_2_ARSIV_NOK/                      # Channel 2 NOK parts archive
```

---

## Usage & Running the Application

### 1. **Launch the Application**
```bash
jupyter notebook DL_QC_Final+TestResults.ipynb
```

Or run directly in Python:
```bash
python -c "exec(open('DL_QC_Final+TestResults.ipynb').read())"
```

### 2. **Main Tabs Overview**

**ÇIFT KANAL ÜRETIM (Dual Channel Production)**
- Real-time monitoring of both production lines
- Original image and AI heatmap display
- OK/NOK status and confidence scores

**MODEL AYARLARI (Model Settings)**
- Hyperparameter tuning (epoch, batch size, learning rate)
- Model training on custom datasets
- Progress monitoring and epoch history

**PLC AYARLARI (PLC Settings)**
- Configure PLC IP address
- Set Rack/Slot for different Siemens models
- Configure data block offsets

**LOG (Logging)**
- Real-time operation logs
- Save logs to file
- Debug information

### 3. **Image Processing Pipeline**

```
New Image → KAMERA_X_GELEN/ 
         → Watchdog detects 
         → CNN inference (300x300 input) 
         → Grad-CAM visualization 
         → PLC write result 
         → Archive to OK/NOK folder 
         → Log entry with timestamp
```

---

## Configuration

### PLC Connection (192.168.8.167)
```
Default Settings:
- IP: 192.168.8.167
- Rack: 0
- Slot: 1 (S7-1200) or 2 (S7-300/400)
- Data Block: 1
```

### Model Input
```
Image Size: 300 × 300 pixels
Format: RGB (3 channels)
Defect Classes: 2 (OK/NOK)
```

### Quality Thresholds
```
Confidence Threshold: 0.50 (adjustable)
Archive Limit: 50 parts per folder
E2E Latency Target: ~200ms
```

---

## Troubleshooting

### Common Issues

**1. TensorFlow GPU/CPU Issues**
```bash
# If TensorFlow installation fails:
pip install --upgrade pip setuptools wheel
pip install tensorflow==2.20.0
```

**2. SNAP7 Connection Fails**
```
Error: "PLC baglanti hatasi"
Solution: 
- Verify PLC IP address is correct
- Check network connectivity
- Ensure S7-1200: Rack=0, Slot=1 (default)
```

**3. Watchdog Not Detecting Images**
```
Solution:
- Ensure image folders exist in working directory
- Use .jpg, .jpeg, .png, .bmp formats
- Check file write permissions
```

**4. GUI Not Displaying**
```bash
# Verify Tkinter installation:
python -m tkinter  # Should open a test window
```

---

## References

- TensorFlow Documentation: https://www.tensorflow.org/
- OpenCV Documentation: https://docs.opencv.org/
- SNAP7 Library: https://sourceforge.net/projects/snap7/
- Watchdog: https://watchdog.readthedocs.io/
- Keras: https://keras.io/

---

## License & Citation

**For Thesis Inclusion (APA 7 Format):**
```
SafakBayraktar. (2026). Python-Deep-Learning-Quality-Control-Program-with-SNAP7-PLC-comm [Computer software]. https://github.com/SafakBayraktar/Python-Deep-Learning-Quality-Control-Program-with-SNAP7-PLC-comm
```

---

## Support & Contact

For questions or issues, please open a GitHub issue in the repository.

**Author:** SafakBayraktar  
**Version:** 26.5  
**Last Updated:** May 12, 2026
