# Facial Landmark Detection for Driver Drowsiness Detection  
**Optimized MobileNetV2 Deployment on Multiple Platforms for Edge AI Applications**  

## 📌 Overview  
This project implements a real-time **Facial Landmark Detection** system designed for driver drowsiness monitoring and other edge AI applications. It uses a **customized MobileNetV2** backbone optimized through **Post-Training Quantization (PTQ)** and **Quantization-Aware Training (QAT)** to achieve high performance with minimal power consumption on resource-constrained devices.  

The system is deployed across **multiple hardware platforms** — including **Xilinx Kria KV260 FPGA**, **NVIDIA Jetson Nano**, **Raspberry Pi 4B**, **Intel Core i9 CPU**, and **NVIDIA RTX 4060 GPU** — and demonstrates significant energy efficiency gains, particularly on FPGA.

---

## 🚗 Motivation  
Drowsy driving is a major cause of traffic accidents worldwide, contributing to **3–30%** of global incidents. Traditional monitoring solutions often rely on cloud processing, high-power GPUs, or costly sensors, making them unsuitable for real-time, embedded automotive applications.  

This project addresses these limitations by:
- Running **locally on low-power edge devices**  
- Detecting **key facial landmarks** (eye corners, mouth corners, head pose) in real-time  
- Supporting applications beyond drowsiness detection, including **attention monitoring**, **emotion analysis**, **AR/VR calibration**, and **facial biometrics**  

---

## 🛠 Features  
- **Lightweight Model**: Customized MobileNetV2 backbone for efficiency  
- **Quantization**:
  - **PTQ**: Fast deployment with 4× compression  
  - **QAT**: Higher robustness with minimal accuracy loss  
- **Real-Time Performance**:
  - FPGA KV260: 30 FPS @ 3W (10 FPS/W, 2.5× more efficient than GPU)  
  - Comparable accuracy: 91.74% (vs. 92.42% baseline)  
- **Cross-Platform Benchmarking**: GPU, CPU, FPGA, and SBCs  
- **Scalable for Edge AI**: Deployable without cloud connectivity  

---

## 📂 Dataset  
The system uses the **WFLW (Wider Facial Landmarks in the Wild)** dataset:
- **10,000 images** (7,500 train / 2,500 test)  
- **98 annotated landmarks** per face  
- Rich variation in pose, occlusion, lighting, and expression  
- Suitable for robust driver monitoring and other real-world applications  

---

## 📊 Results Summary  

| Platform         | FPS  | Power (W) | FPS/W | Accuracy (%) |
|------------------|------|-----------|-------|--------------|
| **FPGA KV260**   | 30   | 3.0       | 10.00 | 91.74        |
| RTX 4060 GPU     | 78   | 20        | 3.91  | 92.42        |
| Intel i9 CPU     | 54   | 40        | 1.35  | 92.42        |
| Jetson Nano 2GB  | 9    | 10        | 0.90  | 91.20        |
| Raspberry Pi 4B  | 4    | 5.1       | 0.79  | 89.70        |

---

## 🖥 System Workflow  
1. **Face Detection** → Crop & preprocess image (grayscale, resize to 112×112, normalize)  
2. **MobileNetV2 Backbone** → Extract hierarchical features  
3. **Neck Module** → Fuse multi-scale features  
4. **Head Module** → Predict 98 facial landmarks  
5. **(Optional)** Auxiliary Pose Branch for head pose regularization during training  

---

## ⚙️ Installation & Deployment  

### Requirements  
- Python 3.8+  
- PyTorch (with Brevitas for quantization)  
- OpenCV  
- Vitis AI (for FPGA deployment)  

### Steps  
```bash
# Clone the repo
git clone https://github.com/DMDung2k3/Drowsiness_Detection_Graduation_Thesis.git
cd Drowsiness_Detection_Graduation_Thesis

# Install dependencies
pip install -r requirements.txt

# (Optional) Train model
python train.py

# Quantize model (PTQ/QAT)
python quantize.py --method qat

# Deploy to KV260
bash deploy_fpga.sh
