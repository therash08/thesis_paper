# Thesis Research Experiments

This repository contains the implementation, experimental pipelines, analysis code, and reproducible research workflow developed as part of my thesis research.

The project is organized into **two major experiments**, focusing on computational mental health, natural language processing (NLP), machine learning, and transformer-based text classification.

---

## 📌 Repository Overview

The repository currently contains two experiments:

### Experiment 1 — Loneliness vs. Depression

This experiment investigates the computational distinction between **loneliness-related** and **depression-related** textual patterns using traditional machine learning and NLP techniques.

The workflow includes:

- Data preprocessing and cleaning
- Text normalization
- Dataset preparation
- Author/group-aware train-validation-test splitting
- TF-IDF feature extraction
- Classical machine learning baselines
- Model training and evaluation
- Performance comparison
- Experimental result generation

Classical machine learning models and feature-based approaches are used to establish strong baseline performance before moving toward more advanced deep learning methods.

**Main directory:**

```text
Experiment_1_Loneliness_vs_Depression/
```

Typical experimental components include:

```text
Experiment_1_Loneliness_vs_Depression/
├── outputs/
│   ├── baselines/
│   ├── cleaning/
│   ├── features/
│   └── splits/
├── notebooks / scripts
└── experiment-related resources
```

Large intermediate datasets, serialized objects, extracted feature matrices, and trained model files are intentionally excluded from Git tracking where appropriate.

---

## 🧠 Experiment 2 — Transformer-Based Emotion Classification

The second experiment focuses on **emotion classification using transformer-based language models**.

Several pretrained transformer architectures are investigated to evaluate their effectiveness for emotion-related text classification.

The experiment includes models such as:

- **BERT**
- **RoBERTa**
- **ClinicalBERT**
- **MentalBERT**

The workflow includes:

- Text preprocessing
- Dataset preparation
- Tokenization
- Transformer fine-tuning
- Validation and model selection
- Checkpoint management
- Performance evaluation
- Comparative analysis across transformer architectures
- Final model generation

**Main directory:**

```text
Experiment_2_Transformer-Based Emotion_Classification/
```

The experimental output structure includes components such as:

```text
Experiment_2_Transformer-Based Emotion_Classification/
├── outputs/
│   ├── checkpoints/
│   │   ├── bert/
│   │   ├── clinicalbert/
│   │   ├── mentalbert/
│   │   └── roberta/
│   │
│   └── final_models/
│       ├── bert/
│       ├── clinicalbert/
│       ├── mentalbert/
│       └── roberta/
├── notebooks / scripts
└── experiment-related resources
```

Large transformer weights and model checkpoints are excluded from the repository to keep the Git history lightweight.

---

# 🔬 Research Workflow

The overall research pipeline can be summarized as:

```text
Raw Data
   │
   ▼
Data Cleaning
   │
   ▼
Preprocessing
   │
   ▼
Dataset Splitting
   │
   ├──────────────────────────────┐
   │                              │
   ▼                              ▼
Experiment 1                   Experiment 2
Classical ML                  Transformers
   │                              │
TF-IDF                         Tokenization
   │                              │
ML Baselines                   Fine-Tuning
   │                              │
Evaluation                     Evaluation
   │                              │
   └──────────────┬───────────────┘
                  │
                  ▼
        Comparative Analysis
                  │
                  ▼
          Thesis Results
```

---

# 📂 Repository Structure

```text
thesis_paper/
│
├── Experiment_1_Loneliness_vs_Depression/
│   ├── outputs/
│   │   ├── baselines/
│   │   ├── cleaning/
│   │   ├── features/
│   │   └── splits/
│   └── ...
│
├── Experiment_2_Transformer-Based Emotion_Classification/
│   ├── outputs/
│   │   ├── checkpoints/
│   │   └── final_models/
│   └── ...
│
├── .gitignore
└── README.md
```

---

# ⚙️ Technologies Used

The experiments are primarily implemented using **Python** and common machine learning, NLP, and deep learning libraries.

Core technologies may include:

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Scikit-learn
- SciPy
- Matplotlib
- PyTorch
- Hugging Face Transformers
- Tokenizers
- Joblib

---

# 🚀 Getting Started

Clone the repository:

```bash
git clone https://github.com/therash08/thesis_paper.git
```

Navigate to the project directory:

```bash
cd thesis_paper
```

Create a virtual environment:

```bash
python -m venv .venv
```

### Windows / Git Bash

Activate the environment:

```bash
source .venv/Scripts/activate
```

### Windows Command Prompt

```bash
.venv\Scripts\activate
```

Install the required dependencies if a `requirements.txt` file is available:

```bash
pip install -r requirements.txt
```

---

# 📊 Experiment 1

Navigate to:

```bash
cd Experiment_1_Loneliness_vs_Depression
```

This experiment contains the workflow for distinguishing and analyzing loneliness- and depression-related text using traditional NLP and machine learning methods.

Important stages include:

```text
Cleaning
   ↓
Dataset Splitting
   ↓
TF-IDF Feature Extraction
   ↓
Machine Learning Baselines
   ↓
Evaluation
   ↓
Result Analysis
```

---

# 🤖 Experiment 2

Navigate to:

```bash
cd Experiment_2_Transformer-Based\ Emotion_Classification
```

This experiment focuses on fine-tuning and comparing pretrained transformer models for emotion classification.

The general workflow is:

```text
Dataset
   ↓
Preprocessing
   ↓
Tokenizer
   ↓
Transformer Model
   ↓
Fine-Tuning
   ↓
Validation
   ↓
Best Model Selection
   ↓
Test Evaluation
```

Transformer architectures investigated include:

```text
BERT
RoBERTa
ClinicalBERT
MentalBERT
```

---

# 💾 Large Files and Model Artifacts

Large experimental artifacts are intentionally not stored directly in this GitHub repository.

Examples include:

```text
*.pkl
*.npz
*.joblib
*.safetensors
*.pt
*.pth
*.ckpt
```

These files may include:

- Preprocessed datasets
- Train/validation/test serialized datasets
- TF-IDF feature matrices
- Classical ML model objects
- Transformer checkpoints
- Fine-tuned transformer weights
- Final trained models

This keeps the repository lightweight and prevents unnecessary storage of multi-gigabyte generated artifacts.

---

# 🔁 Reproducibility

The repository is designed to preserve the experimental code and workflow required to reproduce the thesis experiments.

For reproducibility, users should maintain the same:

- Dataset preparation procedure
- Preprocessing steps
- Train/validation/test split strategy
- Random seeds
- Model configuration
- Training hyperparameters
- Evaluation methodology

Large generated artifacts should be recreated locally by executing the corresponding experimental pipeline.

---

# 📈 Research Objectives

The broader objectives of this repository are to:

1. Investigate linguistic and computational patterns associated with mental-health-related text.
2. Establish classical machine learning baselines using conventional NLP representations.
3. Evaluate modern transformer architectures for emotion-related text classification.
4. Compare general-domain and domain-specific pretrained language models.
5. Maintain a structured and reproducible experimental pipeline.
6. Support systematic analysis for thesis and future research work.

---

# ⚠️ Research Use

This repository is intended primarily for **academic research, experimentation, and reproducibility**.

The models and experimental outputs should not be interpreted as clinical diagnoses or substitutes for professional mental health assessment.

---

# 📌 Project Status

The repository represents an active thesis research workflow.

```text
Experiment 1 — Loneliness vs. Depression
Status: Experimental pipeline developed

Experiment 2 — Transformer-Based Emotion Classification
Status: Transformer training and evaluation pipeline developed
```

Additional analysis, experiments, evaluation procedures, and explainability components may be incorporated as the thesis research progresses.

---

# 📚 Citation

If this repository contributes to future academic work, please cite the corresponding thesis or publication once the final bibliographic information becomes available.

---

## 👨‍💻 Author

**Rasidul Hoque Chowdhury**