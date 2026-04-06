# How Much Machine Learning Is on the SAA‑C03 Exam?

Short answer: very little.

Longer answer:

- The SAA‑C03 exam is not ML‑focused.
- AWS expects you to recognize ML services, not build models.
- ML questions usually involve:
  - Picking the right service for a use case
  - Knowing when to use a pre‑trained AI service vs. SageMaker
  - Understanding high‑level integration patterns

Expected exam weight: less than 5%, often 1–2 questions out of 65.

You do not need algorithms, training workflows, or tuning knowledge — just service boundaries and architectural fit.

---

# Mental Model of AWS Machine Learning Services (SAA‑Friendly)

Think of AWS ML services in three layers, from simplest to most complex.

---

## Layer 1 — AI Services (Pre‑trained, API‑based)

You do not train anything. You call an API.

These are the ones most likely to appear on the SAA exam.

| Category | Service | What It Does |
|---------|---------|--------------|
| Vision | Rekognition | Image/video labeling, face detection, OCR |
| Language | Comprehend | Sentiment, entities, key phrases |
| | Translate | Language translation |
| | Transcribe | Speech‑to‑text |
| | Polly | Text‑to‑speech |
| Chatbots | Lex | Conversational interfaces |
| Search | Kendra | Intelligent enterprise search |
| Forecasting | Forecast | Time‑series forecasting |
| Recommendations | Personalize | Personalized recommendations |

Mental model:  
If the business problem is solved by calling a pre‑trained API, use an AI Service.

---

## Layer 2 — ML Platform (Build/Train/Deploy Models)

This is where SageMaker fits.

### Amazon SageMaker = The ML Factory

It provides:

- Data labeling (Ground Truth)
- Notebook environments
- Training jobs
- Hyperparameter tuning
- Model hosting/endpoints
- Pipelines for MLOps

Mental model:  
If you need to build, train, or deploy your own ML model, use SageMaker.

For SAA, remember:

- SageMaker = custom ML
- AI Services = pre‑built ML
- SageMaker endpoints scale automatically
- Integrates with S3, ECR, Lambda, API Gateway

---

## Layer 3 — ML Infrastructure (DIY ML)

Rarely tested on SAA, but good for architectural awareness.

| Service | Purpose |
|---------|---------|
| EC2 GPU instances (P‑series, G‑series) | Custom training/inference |
| ECS/EKS | Containerized ML workloads |
| EMR | Spark‑based ML pipelines |
| Glue | Data prep for ML |

Mental model:  
If you need full control over the ML stack, use EC2/ECS/EKS/EMR.

---

# Architect’s Decision Tree (SAA‑Optimized)

Is the ML problem solved by a pre-trained API?
→ Yes → Use an AI Service (Rekognition, Comprehend, Polly, etc.)
→ No →
Do you need to build/train/deploy a custom model?
→ Yes → Use SageMaker
→ No → Use ML infrastructure (EC2/EKS/EMR)