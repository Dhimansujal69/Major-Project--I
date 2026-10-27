# ⚡ Explainable Multimodal EV Battery Diagnostic System

An AI-powered Electric Vehicle (EV) battery diagnostic platform designed to estimate battery State of Health (SOH), classify thermal hazard risk, and provide explainable predictions using thermal images and sensor telemetry.

The system combines a **FastAPI backend**, a **React + TypeScript frontend**, and a multimodal deep learning model to support battery condition monitoring and diagnostic visualization.

## 📌 Key Features

- **Multimodal Battery Diagnostics:** Combines infrared (IR) thermal images with electrical sensor telemetry.
- **State of Health (SOH) Estimation:** Supports continuous battery health estimation.
- **Thermal Hazard Classification:** Classifies battery conditions into Safe, Thermal Warning, and Thermal Runaway Critical categories.
- **Explainable AI (XAI):** Supports visual and sensor-level explanations of model predictions.
- **REST API:** Provides FastAPI endpoints for health checks, predictions, and explainability.
- **Interactive Dashboard:** React and TypeScript frontend for submitting diagnostic inputs and viewing results.
- **Organized Test Data:** Includes sample thermal images and telemetry JSON files for testing and validation.

---

## 🏗️ System Architecture

The project consists of three main components.

### 1. Multimodal Deep Learning Model

The model is designed to combine two types of input:

- **Vision branch:** Processes 2D infrared thermal images to extract spatial temperature patterns.
- **Telemetry branch:** Processes time-series sensor measurements, including voltage, current, temperature, and internal resistance.
- **Multimodal fusion:** Combines visual and temporal features for diagnostic predictions.
- **Diagnostic outputs:** Estimates battery SOH and predicts the battery's thermal hazard category.

### 2. FastAPI Backend

The backend manages model loading, input validation, preprocessing, inference, and API responses.

- Health-check endpoint
- Battery prediction endpoint
- Explainability endpoint
- Pydantic request and response schemas
- Image and telemetry preprocessing utilities
- Model configuration and loading

### 3. React Frontend

The frontend provides the user interface for interacting with the diagnostic system.

- React and TypeScript
- Vite development server
- Reusable UI components
- API integration through frontend services
- Custom styling and dashboard interfaces

---

## 📂 Project Structure

The following structure reflects the current repository layout.

```text
Major-Project--I/
│
├── app/
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── health.py
│   │   └── predict.py
│   │
│   ├── __init__.py
│   ├── config.py
│   ├── model_loader.py
│   ├── schemas.py
│   └── utils.py
│
├── frontend/
│   ├── public/
│   │   ├── favicon.svg
│   │   └── icons.svg
│   │
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── App.css
│   │   ├── App.tsx
│   │   ├── index.css
│   │   ├── main.tsx
│   │   └── types.ts
│   │
│   ├── .gitignore
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   ├── tsconfig.app.json
│   ├── tsconfig.json
│   ├── tsconfig.node.json
│   └── vite.config.ts
│
├── models/
│   └── battery_multimodal_model.keras
│
├── test_dataset/
│   ├── critical/
│   ├── safe/
│   └── warning/
│
├── test_telemetry/
│   ├── critical/
│   ├── safe/
│   └── warning/
│
├── .gitignore
├── explainability.py
├── main.py
├── requirements.txt
├── test_model.ipynb
├── train_multimodal.ipynb
└── README.md
```

### Important Files

| File or directory | Purpose |
|---|---|
| `main.py` | Entry point for the FastAPI application |
| `app/routes/health.py` | Health-check API route |
| `app/routes/predict.py` | Prediction and related diagnostic API routes |
| `app/config.py` | Application configuration |
| `app/model_loader.py` | Model loading and access |
| `app/schemas.py` | Pydantic request and response schemas |
| `app/utils.py` | Input preprocessing utilities |
| `explainability.py` | Explainability-related implementation |
| `models/` | Trained model artifact |
| `frontend/src/components/` | Reusable frontend components |
| `frontend/src/services/` | Frontend API and service logic |
| `test_dataset/` | Thermal image test data |
| `test_telemetry/` | Sensor telemetry test data |
| `train_multimodal.ipynb` | Model training notebook |
| `test_model.ipynb` | Model testing notebook |

---

## 🛠️ Technology Stack

### Backend and Machine Learning

- Python
- FastAPI
- Uvicorn
- TensorFlow / Keras
- NumPy
- Pydantic

### Frontend

- React
- TypeScript
- Vite
- CSS
- npm

> The exact versions and additional libraries are defined in `requirements.txt` and `frontend/package.json`.

---

## 🚀 Installation and Setup

### Prerequisites

Install the following before running the project:

- Git
- Python version compatible with the project's dependencies
- Node.js and npm
- VS Code (recommended)

### 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd Major-Project--I
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with your repository URL.

### 2. Create and Activate the Python Environment

Create a virtual environment in the project root:

```bash
python -m venv .venv
```

**Windows PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1
```

**Linux/macOS:**

```bash
source .venv/bin/activate
```

Upgrade pip and install the backend dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If a dependency fails to install, check the Python version required by that package and the project.

### 3. Install Frontend Dependencies

Open a terminal in the project root and run:

```bash
cd frontend
npm install
```

This installs the dependencies declared in `frontend/package.json`.

---

## ⚙️ Running the Application

Run the backend and frontend in **two separate terminals**.

### 1. Start the FastAPI Backend

In Terminal 1, navigate to the project root and activate the virtual environment.

```powershell
cd C:\path\to\Major-Project--I
.\.venv\Scripts\Activate.ps1
python -m uvicorn main:app --host 127.0.0.1 --port 8000 --reload
```

Replace the example project path with your actual location.

When the server starts, the backend should be available at:

- **API base URL:** http://127.0.0.1:8000
- **Swagger documentation:** http://127.0.0.1:8000/docs
- **ReDoc documentation:** http://127.0.0.1:8000/redoc

The interactive API documentation lets you inspect and test the available endpoints.

### 2. Start the React Frontend

In Terminal 2:

```powershell
cd C:\path\to\Major-Project--I\frontend
npm run dev
```

Vite will print the local frontend URL in the terminal, usually:

http://localhost:5173

Open the URL printed by Vite in your browser.

**Note:** Keep both terminals running while using the application. The frontend must be configured to communicate with the backend API URL.

---

## 📡 API Overview

The FastAPI backend exposes diagnostic functionality through REST endpoints.

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/api/v1/health` | Check backend and model status |
| `POST` | `/api/v1/predict` | Submit diagnostic inputs for prediction |
| `POST` | `/api/v1/explain` | Request predictions with explainability information |

The exact request fields, response schemas, and input formats are defined by the implementation in `app/routes/`, `app/schemas.py`, and the related backend modules.

For the latest endpoint definitions, start the backend and visit:

http://127.0.0.1:8000/docs

### Example Health-Check Request

```http
GET /api/v1/health
```

The response depends on the backend implementation and whether the model has loaded successfully.

### Prediction and Explainability

The prediction and explainability routes are intended to support diagnostic results, including SOH estimates, hazard classifications, and any explanation data implemented by the model and backend.

Refer to Swagger documentation for the required request body and actual response fields.

---

## 🧪 Testing and Model Development

The repository includes datasets and notebooks to support model testing and development.

### Thermal Image Dataset

```text
test_dataset/
├── critical/
├── safe/
└── warning/
```

### Telemetry Dataset

```text
test_telemetry/
├── critical/
├── safe/
└── warning/
```

### Jupyter Notebooks

- `train_multimodal.ipynb` — model training workflow.
- `test_model.ipynb` — model evaluation and testing workflow.

Use the notebooks to inspect the training and evaluation procedures before making changes to the trained model or inference pipeline.

---

## 🔍 Explainable AI

Explainability is an important part of the project because battery hazard predictions should be easier to investigate and interpret.

Depending on the implemented model and API response, explanations can include:

- **Thermal image explanations:** Visual highlights of image regions that influence a prediction.
- **Sensor attribution:** Feature-level contributions from telemetry inputs.
- **Diagnostic context:** Predicted battery health and hazard category.

The implementation is maintained in `explainability.py` and the relevant backend route modules.

---

## 🔐 Configuration and Security

- Keep credentials, API keys, and environment variables out of version control.
- Use `.gitignore` to exclude `.env`, `.venv/`, caches, and generated files.
- Avoid committing large datasets or model artifacts unless they are required and suitable for GitHub storage.
- Configure CORS for the frontend's actual development or deployment origin rather than allowing unrestricted access in production.
- Do not expose development servers directly to the public internet without appropriate security controls.

---

## 🐛 Troubleshooting

### `ModuleNotFoundError`

Ensure that the Python virtual environment is activated and that dependencies have been installed:

```bash
python -m pip install -r requirements.txt
```

### Uvicorn Cannot Import `main:app`

Run Uvicorn from the project root, where `main.py` is located. Also confirm that `main.py` defines the FastAPI application as `app`, or adjust the command to match the actual variable name.

### Frontend Dependencies Are Missing

Run:

```powershell
cd frontend
npm install
npm run dev
```

### Frontend Cannot Reach the Backend

Confirm that the backend is running, check the API base URL in `frontend/src/services/`, and verify that the backend CORS configuration allows the frontend origin.

### Model Loading Errors

Verify that the expected model file exists:

```text
models/battery_multimodal_model.keras
```

Also check that the model loader, TensorFlow version, and model architecture are compatible.

---

## 🎯 Project Objective

The objective of this project is to build an integrated, explainable diagnostic platform that combines thermal imaging and electrical telemetry to support EV battery health assessment and thermal hazard identification.

By integrating deep learning, explainability, a REST API, and a modern web interface, the system provides a foundation for exploring multimodal AI in battery monitoring.

---

## 👨‍💻 Development Notes

This repository contains the backend, frontend, model artifact, test data, and model development notebooks.

For setup or integration issues, consult the API documentation at `/docs`, inspect the project configuration, and review the relevant source modules before modifying the application.

**Disclaimer:** This project is intended for research and development. Its predictions should not be treated as a substitute for validated battery safety systems or professional engineering assessment.
