


# Process Log - T2.1 Compressed Crop Disease Classifier

## **1. Hour-by-Hour Timeline**

| Time Block | Tasks & Milestones |
| :--- | :--- |
| **Hour 1** | Initial environment setup. Regenerated `mini_plant_set` using the provided recipe. Conducted Exploratory Data Analysis (EDA) on class distribution. Selected **MobileNetV3-Small** as the base architecture for its efficiency. |
| **Hour 2** | Implemented the training pipeline in PyTorch. Applied **Weighted Cross-Entropy Loss** to address class imbalance. Fine-tuned the model for 15 epochs, monitoring **Macro-F1** rather than raw accuracy. |
| **Hour 3** | Performed **Post-Training INT8 Quantization**. Exported the model to **ONNX** format. Verified that the final file size was under the 10MB budget (Actual: [Insert your file size, e.g., 3.8MB]). |
| **Hour 4** | Developed the **FastAPI** inference service. Built a Dockerfile for containerization. Conducted robustness testing using the `test_field.zip` dataset to evaluate performance on blurred/noisy images. |

---

## **2. LLM & Assistant Tool Declaration**

**Tools Used:** Gemini (Google), GitHub Copilot.

### **Sample Prompts Sent**
1. **Prompt:** "How to implement post-training static quantization for a PyTorch MobileNetV3-Small model and export it to a .onnx file to reduce size under 10MB?"
2. **Prompt:** "Write a FastAPI POST endpoint that accepts an uploaded image file, pre-processes it for a CNN, and returns a JSON response with the top-3 predicted classes and their probabilities."
3. **Prompt:** "Generate a requirements.txt for a lightweight computer vision inference service using FastAPI, Uvicorn, and ONNX Runtime."

### **Discarded Prompt**
- **Prompt:** "Generate a 4-minute script for my project presentation video."
- **Reason:** Discarded because the candidate brief explicitly states that the video must show "real understanding rather than LLM-generated narration." I decided to speak authentically about my code and trade-offs instead of using a script.

---

## **3. Hardest Decision Made**

The single hardest decision was the trade-off between **Input Resolution and Model Performance**. I initially considered dropping the input size from 224x224 to 128x128 to guarantee I would stay under the 10MB limit. However, initial tests showed a significant drop in the **Macro-F1 score for Maize Blight**, as the diagnostic features for that disease are very fine and small. I ultimately decided to keep the **224x224 resolution** to maintain medical accuracy and instead used **aggressive INT8 quantization** and layer pruning to hit the size target. This decision prioritized the farmer's diagnostic reliability over a simpler compression path.

