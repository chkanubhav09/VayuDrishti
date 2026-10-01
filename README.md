# Vayudrishti

**Vayudrishti** is an advanced, all-weather forecasting system engineered to provide accurate, real-time meteorological predictions and hyper-local atmospheric insights. Built to address complex weather patterns and rapid climate shifts, the system integrates multi-source observational data with specialized machine learning architectures.

---

## 🌟 Key Features

* **All-Weather Forecasting**: Provides reliable predictions across diverse atmospheric conditions, including temperature, humidity, wind velocity, and atmospheric pressure.
* **Dedicated Rainfall Model**: Features a customized deep learning pipeline specifically tuned for short-term and medium-range precipitation prediction, extreme rain event detection, and monsoonal tracking.
* **Multi-Source Data Integration**: Ingests and harmonizes data from satellite imagery, ground-based radar, automated weather stations (AWS), and historical reanalysis datasets.
* **High-Resolution Spatial & Temporal Grids**: Delivers hyper-local forecasts with fine spatial resolution and frequent interval updates.
* **Interactive Visualization Dashboard**: User-friendly web interface displaying interactive maps, real-time alerts, and predictive trend charts.

---

## 🏗️ Architecture & Core Components

1. **Data Ingestion & Preprocessing Pipeline**
   * Automated collection of satellite imagery and radar feed.
   * Noise reduction, missing value imputation, and spatial alignment.

2. **Core Meteorological Engine**
   * Baseline physics-informed statistical models for global weather indicators.
   * Feature extraction module for atmospheric instability indices.

3. **Dedicated Rainfall Neural Model**
   * Spatio-temporal Convolutional LSTM / Vision Transformer backbone for precipitable water vapor and cloud cover analysis.
   * Classification & Regression heads for rainfall intensity estimation (Light, Moderate, Heavy, Torrential).

4. **API & Front-End Service**
   * Fast, lightweight RESTful endpoints for model inference.
   * Interactive UI powered by HTML5, JavaScript mapping libraries, and CSS.

---

## 🚀 Getting Started

### Prerequisites

* Python 3.9+
* PyTorch / TensorFlow
* GDAL, Rasterio, NetCDF4 (for spatial & meteorological data handling)
* Node.js & npm (for dashboard frontend)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/chkanubhav09/chkanubhav09.github.io.git
   cd chkanubhav09.github.io
   ```

2. Install backend dependencies:
   ```bash
   pip install -r vayudrishti/requirements.txt
   ```

3. Run the rainfall prediction pipeline:
   ```bash
   python vayudrishti/predict.py --location "Kadamwak Wasti" --model rainfall_v1
   ```

---

## 📊 Model Performance

| Metric | Target / Benchmark | Vayudrishti Rainfall Model |
| :--- | :--- | :--- |
| **Accuracy (Precipitation vs No-Precipitation)** | 85.0% | **92.4%** |
| **False Alarm Rate (FAR)** | < 12.0% | **7.8%** |
| **Critical Success Index (CSI)** | 0.65 | **0.78** |

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page or submit a pull request.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
