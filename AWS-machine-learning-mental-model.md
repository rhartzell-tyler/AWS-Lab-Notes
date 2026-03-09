## 🧠 AWS Machine Learning Services — Mental Model

AWS ML services fall into **three layers**, and exam questions map directly to these layers. If you memorize the layers, you can answer almost every ML question instantly.

---

## 1) AI Services (Pre‑trained APIs) — *“No ML skills required”*

These are plug‑and‑play APIs for common ML tasks. You don’t train anything; you just call the service.

Use these when the scenario says things like:
- “No ML expertise”
- “Need results quickly”
- “Simple API call”
- “Don’t want to manage infrastructure or models”

**Key services:**
- **Rekognition** — image/video analysis (faces, labels, unsafe content, text in images)
- **Comprehend** — NLP (sentiment, key phrases, PII detection)
- **Transcribe** — speech‑to‑text
- **Polly** — text‑to‑speech
- **Translate** — language translation
- **Textract** — OCR + form/table extraction
- **Forecast** — time‑series forecasting
- **Personalize** — recommendations
- **Kendra** — enterprise search

**Exam trigger:**  
> “We need ML but don’t want to build or train a model.”

---

## 2) ML Platform (Build/Train/Deploy) — *“We have ML engineers or data scientists”*

This is **SageMaker**.  
If the scenario mentions training, tuning, notebooks, or custom models, the answer is almost always SageMaker.

**SageMaker capabilities to remember:**
- **Studio** — full ML IDE
- **Notebooks** — Jupyter‑based development
- **Training jobs** — scalable training
- **Hyperparameter tuning** — automated optimization
- **Inference endpoints** — real‑time or batch predictions
- **Ground Truth** — data labeling
- **Pipelines** — ML workflow automation

**Exam trigger:**  
> “Train a custom model,” “host a model,” “manage ML infrastructure,” “hyperparameter tuning.”

---

## 3) ML Frameworks & Infrastructure — *“Bring your own model or framework”*

This layer is rarely tested on SAA‑C03, but you should know the pattern.

Use this when the scenario says:
- “We want full control.”
- “We use TensorFlow/PyTorch/MXNet.”
- “We need GPU clusters.”

**Key components:**
- **Deep Learning AMIs** — preconfigured EC2 images
- **Deep Learning Containers** — Docker images for ML frameworks
- **EC2 GPU instances** — p3, p4, g4, g5

**Exam trigger:**  
> “Custom training environment,” “full control,” “specialized hardware.”

---

## 🧩 How to choose the right ML service on the exam

1. **Do you need ML but don’t want to train a model?**  
   → Use an **AI Service** (Rekognition, Comprehend, Textract, etc.)

2. **Do you need to train, tune, or deploy a model?**  
   → Use **SageMaker**.

3. **Do you need full control over the ML environment?**  
   → Use **Deep Learning AMIs/Containers** or **GPU EC2**.

---

## 📝 What to memorize for the exam

- **Rekognition** — images/video  
- **Comprehend** — text/sentiment  
- **Textract** — OCR/forms/tables  
- **Transcribe** — speech → text  
- **Polly** — text → speech  
- **Translate** — language translation  
- **Forecast** — time‑series forecasting  
- **Personalize** — recommendations  
- **Kendra** — enterprise search  
- **SageMaker** — build/train/deploy ML models  
- **Deep Learning AMIs/Containers** — custom frameworks

---
