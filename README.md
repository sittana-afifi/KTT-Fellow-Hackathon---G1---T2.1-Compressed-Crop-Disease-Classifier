# 🌿 T2.1 Compressed Crop Disease Classifier

## **Project Overview**
This repository provides a high-performance, edge-optimized Computer Vision model designed to diagnose crop diseases in rural, low-bandwidth environments. The system identifies five critical classes: **Healthy, Maize Rust, Maize Blight, Cassava Mosaic, and Bean Spot.**

The core differentiator of this solution is the balance between **model compression (<10MB)** and **field robustness**, ensuring accuracy even with noisy, motion-blurred images common in field diagnostics.

---

## **🚀 Performance Metrics**
| Metric | Result | Target |
| :--- | :--- | :--- |
| **Model Size (INT8 Quantized)** | **5.94 MB** | < 10 MB |
| **Macro-F1 (Validation)** | **99.11%** | ≥ 80% |
| **Macro-F1 (Field Test)** | **99.11%** | Robustness Check |
| **Inference Latency** | **[Insert Latency, 282.93 ms]** | N/A |

---

## **📁 Project Structure**
```text
.
├── data/
│   ├── data_generator.ipynb                 # Dataset recipe and labels (gitignored images)
├── models/
│   ├── model_quantized.onnx # Final <10MB production model
│   └── train.py            # Training & Quantization script
├── service/
│   ├── app.py              # FastAPI inference service
│   └── Dockerfile          # Containerization for deployment
├── samples/                # Sample field images for testing
├── requirements.txt        # Production dependencies
├── process_log.md          # Development timeline & tool declaration
├── ussd_fallback.md        # Product design for non-smartphone users
├── SIGNED.md               # Candidate Honor Code
└── README.md               # Project documentation
```
---


## **🛠️ Technical Architecture**

### **1. Model Training & Compression**
- **Base Architecture:** [e.g., MobileNetV3-Small] chosen for its efficiency on mobile CPUs and high accuracy-to-parameter ratio.
- **Optimization:** Fine-tuned on `mini_plant_set` using Weighted Cross-Entropy to address class imbalance.
- **Quantization:** Applied **Post-Training INT8 Quantization** to reduce the footprint significantly while meeting the 10MB budget.
- **Format:** Exported to **ONNX** for high-speed, cross-platform inference on edge devices.

### **2. Inference API**
A **FastAPI** service serves the model via a single endpoint:
- **`POST /predict`**: Accepts a JPEG/PNG image and returns:
    - **Primary Diagnosis**: The predicted disease class.
    - **Confidence Score**: Probability of the prediction.
    - **Top-3 Alternates**: Other likely candidates.
    - **Inference Latency**: Time taken for a single pass in milliseconds.

---

## **📦 Deployment & Reproduction**

### **Setup**
```bash
pip install -r requirements.txt
```
Run locally
```bash
python service/app.py
```
Run via Docker
```bash
docker build -t crop-classifier .
docker run -p 8000:8000 crop-classifier
```
---

# 🌍 Product & Business Adaptation: USSD Fallback Strategy

## **1. The Digital Divide Challenge**
While our 10MB quantized model is designed for edge efficiency, many farmers in rural Rwanda still utilize feature phones (non-smartphones) or live in areas with zero data coverage. To ensure the intelligence of the **Crop Disease Classifier** reaches everyone, we implement a "Human-in-the-Loop" USSD extension.

## **2. The Workflow**

### **Step A: The Village Agent (Smartphone User)**
A local agricultural extension officer or "Village Lead" carries a low-cost smartphone containing the compressed model. 
* They perform the physical scans of the crops.
* The model runs locally on their device (Offline).
* Results are cached until they reach a 2G/3G signal area.

### **Step B: Data Synchronization**
Once the agent reaches connectivity, the diagnostic results (e.g., *Maize Rust detected at coordinates -1.94, 30.06*) are synced to the Ministry of Agriculture’s central database.

### **Step C: USSD Retrieval (`*123#`)**
The individual farmer, using a basic feature phone, can access their farm's specific health data:
1. **Dial `*123#`**: The farmer enters their National ID or Farm ID.
2. **Menu Selection**: 
    - 1: View Latest Diagnosis
    - 2: Treatment Recommendations
    - 3: Request Agronomist Visit
3. **SMS Delivery**: The farmer receives a text message: *"AMAKURU! Your maize scan from Tuesday shows Rust. Please apply [Treatment Name] immediately. Avoid watering leaves directly."*

## **3. Strategic Impact**
- **Accessibility**: 100% community coverage, regardless of device ownership.
- **Data-Driven Policy**: Real-time heatmaps of disease outbreaks (Maize Blight or Cassava Mosaic) allow for rapid government intervention.
- **Low Cost**: USSD is zero-rated or extremely low-cost, removing the financial barrier of mobile data for the farmer.

