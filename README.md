![Version](https://img.shields.io/badge/Version-1.0-blue)
![Hardware](https://img.shields.io/badge/Hardware-Cardputer-orange)
![Platform](https://img.shields.io/badge/Platform-M5Stack-red)
![License](https://img.shields.io/badge/License-Proprietary-gray)
[![Boosty](https://img.shields.io/badge/Support-Boosty-orange)](https://boosty.to/zeloksa)

# 📐 IMU Acoustic Analyzer (V1.0)

**IMU Acoustic Analyzer** transforms the **M5Stack Cardputer** into a professional-grade metrological tool (an acoustic scleroscope). By polling the internal BMI270 accelerometer at a high frequency of 1600Hz, the firmware captures and analyzes the micro-physics of an impact. It calculates structural hardness, elasticity, and kinetic energy absorption to instantly identify surface materials. 

Wrapped in a highly optimized, non-blocking "Blueprint" CAD-style UI, this firmware brings industrial laboratory testing directly to your pocket.

> [!IMPORTANT]
> **Source Code Status:** This project is proprietary. The source code is private. 
> **Distribution:** Binary (`.bin`) only via the **Releases** tab.

---

## ⚠️ Expectations (Must Read Before Use)

**This is a precision physical instrument, not a toy.** * **The Drop Technique is Critical:** For accurate readings, the device must fall perfectly flat. Stand it on its edge (SD card & ON/OFF switch facing UP), tilt the top center gently, and **let it fall naturally without applying any downward force**. 
* **Angles Matter:** Even a 1-degree tilt upon impact or hidden supports under a table will alter the acoustic stiffness and change the results.
* **No Artificial Debounce:** The firmware captures raw, immediate micro-bounces (less than 1ms). Dropping it on uneven surfaces will result in a `[ CROOKED DROP! ]` error.
* **Durability Reassurance:** Do not be afraid to use it! During the creation of this firmware, the device was dropped over 1000 times in this exact manner (including onto hard tiles). Because it simply tips over from a standing edge position—and is not thrown or dropped from a height—the Cardputer easily survives the impacts without any damage.

---

## ⚡ Technical Highlights

* **4-Dimensional DSP Engine:** The analyzer doesn't just look at peak impact. It calculates 4 critical physical variables:
  * `MaxG`: Peak impact hardness.
  * `Ratio`: Elastic rebound (energy return).
  * `Dt`: Time of flight (impact duration).
  * **`AUC` (Area Under Curve):** The firmware integrates the `accMagnitude` curve during the primary impact to calculate the true physical impulse. This allows the algorithm to differentiate between materials with identical peak hardness but different viscosities (e.g., dense rubber vs. soft plastic).
* **Cluster Centroid Calibration:** When adding a new material to the database (5 drops), the algorithm intelligently discards the worst (anomalous) drop and averages the remaining 4 perfect drops to create a highly stable mathematical "Centroid" profile.
* **"Zero-Shot" Physical Insight:** Even if a material is not in your database, the analyzer evaluates the raw physics and provides an instant diagnostic of its properties (e.g., `Ultra-Hard | Elastic` or `Firm | Dampening`).
* **CAD Blueprint Interface:** The UI abandons heavy polygon fills for a strict, transparent wireframe grid. This ensures zero screen-tearing and prevents rendering tasks from blocking the 1600Hz IMU polling cycle.
* **Acoustic Feedback:** Features simple and helpful audio signals to let you know when the device is ready to drop and when the measurement is successfully completed.

---

## 🛠 Installation
### Method 1: M5Burner (Recommended)
1. Open **M5Burner**.
2. Search for `IMU Acoustic Analyzer` or `Zeloksa`.
3. Select version **V1.0**.
4. Burn to your M5Stack Cardputer.

### Method 2: Manual Flashing
1. Go to the **[Releases]** tab of this repository.
2. Download the **`Sclero_V1.0.bin`** file.
3. Flash to your Cardputer using **M5Burner** (Local File) or **esptool**.

---

## 🕹 Controls
* **[ 1 ]**: Start 3-Drop Measurement.
* **[ 2 ]**: Add New Material (5-Drop Calibration).
* **[ 3 ]**: Open Database List.
* **[ < / , ] & [ > / / ]**: Navigate Database Pages (Left / Right).
* **[ 1 - 4 ]**: Delete a specific material from the current Database page.
* **[ ESC / \` ]**: Global Cancel / Return to Main Menu.
* **[ - / _ ]**: Decrease system volume by 10 (emits a test click).
* **[ = / + ]**: Increase system volume by 10 (emits a test click).

---

## 📖 Operational Guide

### 🔍 Reading the Data
When you complete a drop, you will see a breakdown of the material's properties:
* **t (Time):** The flight time in milliseconds between the primary impact and the secondary bounce.
* **R (Ratio):** The percentage of kinetic energy returned by the surface (1.0 = perfect spring, 0.1 = dead drop).
* **G (Gravity):** The raw shock value of the impact. Higher values mean absolute rigidity (e.g., concrete, solid wood).

### 💾 Persistent Database
The Cardputer utilizes its internal NVRAM (`Preferences`) to store up to dozens of material profiles. The database dynamically pages your materials and allows for instant deletion with built-in safety confirmations.

---

## ☕ Support the Project
Support the development of advanced metrological offline tools for the Cardputer ecosystem:
* **[https://boosty.to/zeloksa]**

---
*Developed by Engineer Zeloksa. Strictly optimized for Cardputer ADV.*
