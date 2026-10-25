# ⚡ Explainable Multimodal EV Battery Diagnostic System

## 📌 Project Overview & Architecture

The system is organized into two main components:

### 1. Multimodal AI Backend — Python & FastAPI

- **Vision Branch:** Uses MobileNetV2 to extract spatial features from 224 × 224 × 3 infrared (IR) thermal images.
- **Telemetry Branch:** Uses a Bidirectional LSTM (BiLSTM) to analyze sequential electrical measurements, including voltage, current, temperature, and internal resistance.
- **Multimodal Fusion:** Combines image and telemetry features to generate battery health and thermal hazard predictions.
- **State of Health (SOH) Estimation:** Predicts battery health as a continuous percentage.
- **Thermal Hazard Classification:** Classifies battery conditions into `Safe`, `Thermal Warning`, and `Thermal Runaway Critical`.
- **Explainable AI (XAI):** Uses Grad-CAM for visual heatmap explanations and Integrated Gradients for sensor attribution.

### 2. Interactive Frontend Dashboard — React, TypeScript & Vite

- Provides an interactive dashboard for submitting thermal images and battery telemetry.
- Displays predicted State of Health (SOH), thermal hazard classification, confidence scores, and class probabilities.
- Presents diagnostic results and explainability information in a user-friendly interface.
- Integrates with the FastAPI backend through HTTP API requests.
- Uses reusable React components to organize the dashboard, diagnostic forms, results, navigation, and explainability views.

The frontend and backend run as separate services and communicate through the backend's REST API.
---

## 📂 Project Repository Structure

```text
Major-Project--I/
│
├── app/
│   ├── routes/
│   │   ├── health.py
│   │   └── predict.py
│   ├── config.py
│   ├── explainability.py
│   ├── model_loader.py
│   ├── schemas.py
│   └── utils.py
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── DashboardOverview.tsx
│   │   │   ├── DiagnosticForm.tsx
│   │   │   ├── DiagnosticResults.tsx
│   │   │   ├── ExplainabilityPanel.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Topbar.tsx
│   │   │   └── PageFooter.tsx
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── tsconfig.json
│   └── vite.config.ts
│
├── artifacts/                 # Evaluation artifacts and plots
├── models/                    # Model weights, if tracked
├── test_dataset/              # Sample thermal test images
├── test_telemetry/            # Sample telemetry JSON files
├── explainability.py           # Root-level explainability module, if retained
├── main.py                    # FastAPI application entry point
├── requirements.txt           # Python dependencies
├── test_model.ipynb            # Model testing notebook
├── train_multimodal.ipynb      # Model training notebook
├── .gitignore
└── README.md
```

### Technology Stack

**Backend**
- Python
- TensorFlow / Keras
- FastAPI
- Pydantic
- Uvicorn

**Frontend**
- React
- TypeScript
- Vite
- Tailwind CSS, if enabled in the current frontend configuration
- Recharts for data visualizations
- Lucide React for icons

**Machine Learning & Explainability**
- MobileNetV2
- Bidirectional LSTM (BiLSTM)
- Attention-based multimodal feature fusion
- Grad-CAM
- Integrated Gradients

### Frontend Structure

```text
frontend/
├── public/
└── src/
    ├── assets/
    ├── components/
    │   ├── DashboardOverview.tsx
    │   ├── DiagnosticForm.tsx
    │   ├── DiagnosticResult.tsx
    │   ├── ExplainabilityPanel.tsx
    │   ├── PageFooter.tsx
    │   ├── Sidebar.tsx
    │   └── Topbar.tsx
    ├── hooks/
    └── services/
```

**Frontend Components**

- **DashboardOverview.tsx** — Dashboard overview and battery diagnostic summaries.
- **DiagnosticForm.tsx** — Interface for submitting thermal image and telemetry inputs.
- **DiagnosticResult.tsx** — Displays battery health predictions and thermal hazard results.
- **ExplainabilityPanel.tsx** — Presents explainability outputs, including Grad-CAM heatmaps and sensor attributions.
- **Sidebar.tsx** — Dashboard navigation.
- **Topbar.tsx** — Dashboard header and top-level controls.
- **PageFooter.tsx** — Footer section of the dashboard.

The frontend uses React and TypeScript, with Vite for development and building. It communicates with the Python FastAPI backend to retrieve battery diagnostic predictions and explainability results.
