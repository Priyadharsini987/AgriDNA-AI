# AgriDNA AI 🌱

**AgriDNA AI** is an AI-powered precision-agriculture platform designed to help farmers monitor crop health, identify potential plant diseases from leaf images, understand soil-nutrient conditions, and make more informed crop-care decisions.

The project combines a React frontend with a Flask backend and a deep-learning image-classification model. Its farmer-focused workflow is organised into five stages:

**Capture → Diagnose → Analyse → Recommend → Act**

## Key features

- **Crop disease detection:** Farmers can upload a crop-leaf image for AI-assisted disease classification.
- **Soil health monitoring:** Tracks soil nitrogen (N), phosphorus (P), and potassium (K) values and displays soil-health status.
- **Weather-aware guidance:** Uses supplied weather conditions and temperature to provide spray-timing advice.
- **Treatment recommendations:** Provides disease-specific pesticide guidance or bio-based solutions, including preparation and application timing where available in the recommendation data.
- **Crop-care planning:** The project’s advisory scope includes crop-rotation strategies, spray schedules, bio-pesticide suggestions, and laboratory-testing recommendations.
- **Farm dashboard and history:** Displays scan results, soil trends, alerts, and previous disease scans.
- **Farmer account flow:** Includes registration, login, and onboarding screens.
- **Visual analytics:** Uses charts and dashboard components to make crop and soil information easier to understand.
- **Multilingual interface support:** The frontend includes language switching for Indian languages.

> Recommendations are decision-support information, not a substitute for local agricultural experts, laboratory diagnosis, or pesticide-label instructions. Always verify treatment choice, dosage, and local regulations before application.

## Five-stage workflow

| Stage | What happens |
|---|---|
| **1. Capture** | The farmer uploads a crop-leaf image and provides relevant farm or weather details. |
| **2. Diagnose** | The backend preprocesses the image and runs it through the trained EfficientNet-B3 classification model. |
| **3. Analyse** | The application considers the predicted disease, weather inputs, and available soil NPK information. |
| **4. Recommend** | The recommendation logic returns relevant disease-care guidance, spray advice, and soil-related actions. |
| **5. Act** | Farmers can review the suggested actions, monitor soil-health changes, and refer to previous scan results. |

## Technology stack

### Frontend
- React 18
- JavaScript, HTML, and CSS
- Recharts for data visualisation
- Axios / frontend API integration

### Backend and AI
- Python
- Flask and Flask-CORS
- PyTorch and Torchvision
- `timm` for the EfficientNet-B3 model architecture
- Pillow for image handling and preprocessing
- Image processing and deep-learning-based classification

### Data storage
- SQLite for farmer accounts, soil nutrient values, and scan history
- JSON for storing recommendation details

## Project structure

~~~text
AgriDNA-AI/
├── backend/
│   ├── app.py                 # Flask application and REST API routes
│   ├── get_recom.py           # Disease recommendations and soil-impact logic
│   └── best_model.pth         # Trained model checkpoint (provide locally)
├── agridna-ai-v3/
│   └── agridna-v2/
│       ├── public/
│       ├── src/               # React application source
│       ├── package.json
│       └── README.md
├── get_recom.py               # Earlier standalone recommendation module
└── README.md
~~~

## Getting started

### 1. Frontend

Open a terminal in the frontend directory:

~~~bash
cd agridna-ai-v3/agridna-v2
npm install
npm start
~~~

The React development server normally runs at [http://localhost:3000](http://localhost:3000).

### 2. Backend

The backend source is in the `backend/` directory. Create and activate a Python virtual environment, then install the packages imported by the application:

~~~bash
cd backend
python -m venv .venv
~~~

Activate the environment:

**Windows PowerShell**
~~~powershell
.venv\Scripts\Activate.ps1
~~~

**macOS / Linux**
~~~bash
source .venv/bin/activate
~~~

Install the backend packages:

~~~bash
pip install flask flask-cors torch torchvision timm pillow
~~~

The backend expects a trained checkpoint named `best_model.pth` in the `backend/` working directory. Obtain the project model file separately and place it there before starting the application. The model checkpoint is not included in this repository.

Start the API from inside `backend/`:

~~~bash
python app.py
~~~

The Flask application is configured to run on port `5000`. Start the backend before using frontend features that call its API.

> **Setup note:** A pinned backend dependency file and a model-download location are not currently included in the repository. The install command above lists the packages imported by the current Flask application; compatible PyTorch and Torchvision versions may need to be selected for your Python and hardware environment.

## Backend API overview

The Flask application currently defines these routes:

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/register` | Register a farmer account |
| POST | `/api/login` | Authenticate a farmer |
| POST | `/api/scan` | Process a leaf image and return disease and recommendation data |
| GET | `/api/history/<user_id>` | Retrieve a farmer’s scan history |
| GET | `/api/soil/<user_id>` | Retrieve soil NPK values and soil-health information |
| POST | `/api/soil/heal` | Update soil nutrient values through the soil-restoration flow |

## Configuration and security

- Keep API keys, passwords, and private configuration in local environment variables or a secure deployment configuration.
- Do not commit `.env` files, credentials, or private model checkpoints.
- The frontend's translation integration documents a `REACT_APP_ANTHROPIC_KEY` setting. Values prefixed with `REACT_APP_` are bundled into browser code, so do not use a private production API key there; route sensitive API requests through a protected backend instead.
- Configure CORS with the specific frontend origin before deploying the backend publicly.
- Use production-grade server settings rather than Flask's development server and debug mode for deployment.

## Current implementation notes

- The Flask backend loads the EfficientNet-B3 checkpoint at startup and uses a 300 × 300 image transform with ImageNet normalisation.
- If the checkpoint cannot be loaded, the current backend contains a fallback prediction path. A fallback result should not be treated as a real model prediction.
- The disease recommendation knowledge base and soil-impact values are maintained in `backend/get_recom.py`.
- The frontend has additional interface details in [the frontend README](agridna-ai-v3/agridna-v2/README.md).

---

**AgriDNA AI — supporting smarter crop-health monitoring and more informed farming decisions.**
