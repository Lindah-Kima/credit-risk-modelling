# Credit Risk Modelling

A practical credit risk project focused on borrower risk assessment, credit scorecard development, default prediction and lending decisions using statistical analysis and machine learning.

**Status:** In development

## Project Overview

This project explores how financial institutions assess and manage credit risk using customer, loan and repayment data.

Using synthetic datasets generated with Tonic Fabricate, the project covers credit risk measurement, exploratory data analysis, statistical modelling, machine learning, scorecard development and portfolio analysis.

The objective is to build an end-to-end credit risk modelling workflow, from data preparation and model development to model evaluation, API integration and application-level prediction.

The project also explores how predictive models can be integrated into applications, allowing users to submit borrower information, receive model-generated predictions and interpret the results through an interactive interface.

## Key Areas

### 1. Exploratory Data Analysis
- Analyse customer demographics, financial characteristics and loan behaviour.
- Investigate default patterns across customer and loan segments.
- Identify relationships between borrower characteristics and repayment outcomes.
- Examine missing values, outliers and class imbalance.

### 2. Credit Risk Measurement
- **Probability of Default (PD):** Estimate the likelihood of a borrower defaulting over a defined period.
- **Exposure at Default (EAD):** Estimate the outstanding exposure when default occurs.
- **Loss Given Default (LGD):** Estimate the proportion of exposure not recovered after default.
- **Expected Loss (EL):** Calculate expected credit loss using PD × EAD × LGD.

### 3. Credit Scorecard Development
- Data binning and variable transformation.
- Weight of Evidence (WOE) and Information Value (IV).
- Logistic regression modelling.
- Scorecard development and scaling.
- Score interpretation and reason codes.

### 4. Default Prediction
- Develop models to estimate borrower default risk.
- Establish a logistic regression baseline.
- Compare machine learning models such as Random Forest and XGBoost.
- Handle class imbalance and feature selection.
- Evaluate model performance and probability calibration.

### 5. Loan Limit Modelling
- Analyse historical lending patterns and customer affordability indicators.
- Develop models to estimate potential loan limits.
- Evaluate predictions against historical lending outcomes.
- Apply affordability and risk-based lending constraints.

### 6. Credit Decisioning
- Combine credit scores, predicted default probabilities and lending rules.
- Define approval, rejection and manual review criteria.
- Generate decision explanations.
- Examine the impact of different decision thresholds.

### 7. Portfolio Risk Analysis
- Analyse portfolio exposure and expected losses.
- Compare default rates across customer segments.
- Examine risk concentration and portfolio composition.
- Develop visualisations for monitoring portfolio performance.

### 8. Model Serving and Application Integration

Explore how trained machine learning models are made accessible to applications and used to generate predictions.

**Model API Development**
- Package trained models and their preprocessing components for inference.
- Develop REST API endpoints using FastAPI.
- Define request and response schemas using Pydantic.
- Validate incoming application data.
- Expose model predictions through HTTP endpoints.

**Application Development**
- Build an interactive Gradio application for submitting borrower information.
- Design input forms for customer financial and credit characteristics.
- Connect the Gradio interface to the FastAPI prediction service.
- Send application inputs to API endpoints using HTTP requests and JSON payloads.
- Receive and process API responses.
- Display credit scores, default probabilities and predicted loan limits through the interface.

**Understanding API Integration**

A key part of this project is understanding the complete interaction between an application, an API and a machine learning model.

The intended prediction workflow is:

1. A user enters borrower information through the Gradio interface.
2. Gradio collects and structures the input data.
3. The application sends an HTTP request containing a JSON payload to the FastAPI endpoint.
4. FastAPI validates the request and passes the data to the appropriate model.
5. The model applies the required preprocessing and generates a prediction.
6. FastAPI returns the prediction as a JSON response.
7. Gradio receives the response and displays the result to the user.

This establishes an understanding of how an independently deployed prediction service can be consumed by an application, beyond simply developing and exposing an API.

## Modelling and Evaluation

Models will be assessed using metrics appropriate to credit risk, including:

- ROC-AUC and Gini coefficient.
- Kolmogorov-Smirnov (KS) statistic.
- Precision, recall and F1-score.
- Confusion matrix and classification thresholds.
- Brier score and probability calibration.
- Population Stability Index (PSI).
- Feature importance and model explainability.

Time-based validation will be used where the data supports it, with particular attention to target leakage and observation windows.

## Technology Stack

| Area | Tools |
|---|---|
| Synthetic data | Tonic Fabricate |
| Database | PostgreSQL, Aiven |
| Database management | DBeaver |
| Analysis | Python, SQL, Pandas, NumPy |
| Visualisation | Matplotlib, Seaborn, Power BI |
| Statistical modelling | Statsmodels, Scikit-learn |
| Machine learning | Scikit-learn, XGBoost |
| Experiment tracking | MLflow |
| API development | FastAPI, Pydantic |
| Application interface | Gradio |
| API communication | HTTP, REST, JSON |
| Deployment | Docker, GitHub Actions |
| Model monitoring | Evidently AI |

## Architecture

The project follows a layered architecture separating data management, model development, prediction services and application interaction.

```text
Tonic Fabricate
      |
      v
Synthetic Customer and Loan Data
      |
      v
PostgreSQL (Aiven)
      |
      v
Data Exploration and Preparation
      |
      v
Feature Engineering
      |
      v
Credit Risk Analysis
      |
      v
Scorecard and Predictive Models
      |
      v
Model Evaluation and Explainability
      |
      v
Model Packaging and Versioning
      |
      v
FastAPI Prediction Service
      |
      v
Gradio Application
      |
      v
User Inputs and Model Predictions
```

### Application Prediction Flow

```text
User
 |
 v
Gradio Interface
 |
 | HTTP POST Request (JSON)
 v
FastAPI Endpoint
 |
 v
Input Validation (Pydantic)
 |
 v
Preprocessing and Feature Transformation
 |
 v
Trained Machine Learning Model
 |
 v
Prediction
 |
 v
JSON Response
 |
 v
Gradio Interface
 |
 v
Results Displayed to User
```

MLflow will support experiment tracking and model versioning. Docker and CI/CD will support reproducible packaging and deployment, while monitoring will help assess data and model stability.

## Repository Structure

```text
## Repository Structure

```text
credit-risk-modelling/
│
├── .github/
│   └── workflows/              # GitHub Actions workflows for automated testing and CI/CD
│
├── api/                        # FastAPI application: API routes, request handling and prediction endpoints
│
├── app/                        # Gradio user interface where users enter borrower details and view predictions
│
├── configs/                    # Configuration files for models, application settings and experiments
│
├── data/
│   ├── raw/                    # Original datasets as received or generated
│   ├── interim/                # Temporarily cleaned or transformed datasets
│   └── processed/              # Final datasets prepared for analysis and modelling
│
├── docker/                     # Dockerfiles and related files for packaging the application
│
├── docs/                       # Project documentation, technical notes and methodology explanations
│
├── logs/                       # Application, API and model execution logs
│
├── migrations/                 # Database migration files for tracking changes to database structure
│
├── models/                     # Saved and trained model files, encoders and preprocessing objects
│
├── notebooks/                  # Jupyter notebooks for exploration, analysis, experiments and prototyping
│
├── reports/
│   ├── figures/                # Charts, graphs and visual outputs from analysis
│   └── summaries/              # Written analysis, model evaluation results and project findings
│
├── scripts/                    # Standalone scripts for repetitive tasks such as data preparation and training
│
├── sql/                        # SQL queries for data extraction, transformation and database operations
│
├── src/
│   └── credit_risk/
│       ├── data/               # Reusable functions for loading, cleaning and preparing data
│       ├── features/           # Feature engineering and variable transformation logic
│       ├── evaluation/         # Model evaluation metrics and validation procedures
│       ├── models/             # Model training, prediction and modelling logic
│       ├── scoring/             # Credit scorecard development, WOE, IV and score scaling
│       └── decisioning/        # Credit decision rules, risk grades and lending recommendations
│
├── tests/                      # Automated tests for data processing, models, API endpoints and application logic
│
├── utils/                      # General-purpose helper functions shared across the project
│
├── .env.example                # Template showing the environment variables required by the project
├── .gitignore                  # Specifies files and folders Git should not track
├── .dockerignore               # Specifies files Docker should exclude when building an image
├── pyproject.toml              # Project metadata, dependencies and Python development tool configuration
├── README.md                   # Main project description, setup instructions and documentation
└── requirements.txt            # Python package dependencies
```

### Understanding the Main Folders

| Folder | What it means |
|---|---|
| `.github/workflows` | Automates tasks such as running tests whenever code is pushed to GitHub. |
| `api` | Contains the FastAPI backend that receives application requests and returns model predictions. |
| `app` | Contains the Gradio interface that users interact with. |
| `configs` | Stores settings that control how different parts of the project run. |
| `data` | Organises datasets according to their stage of preparation. |
| `docker` | Contains instructions for packaging the application and its dependencies into Docker containers. |
| `docs` | Holds explanations of how the project works and why particular approaches were used. |
| `logs` | Keeps records of application activity, errors and execution events. |
| `migrations` | Tracks changes made to database tables and structures over time. |
| `models` | Stores trained models and supporting files needed to make predictions. |
| `notebooks` | Provides an interactive environment for exploring data and experimenting with modelling approaches. |
| `reports` | Stores the outputs of analysis, charts and model evaluation. |
| `scripts` | Holds Python scripts that perform specific project tasks. |
| `sql` | Stores SQL statements used to retrieve and manipulate data. |
| `src` | Contains the main reusable Python code that powers the credit-risk functionality. |
| `tests` | Contains checks to make sure the different parts of the project work correctly. |
| `utils` | Holds small reusable helper functions that do not belong to a specific module. |

### Application Architecture

The project separates the user interface, API and modelling logic:

1. **Gradio (`app/`)** – provides the interface where a user enters borrower information.
2. **FastAPI (`api/`)** – receives the information through an HTTP request, validates it and sends it to the prediction logic.
3. **Credit Risk Logic (`src/`)** – handles preprocessing, model inference, scoring and decisioning.
4. **Models (`models/`)** – contains the saved models and preprocessing objects required for predictions.
5. **Gradio** – displays the prediction and relevant credit-risk results returned by the API.

```

## Development Approach

The project will follow a structured development process:

1. Generate and understand the synthetic datasets.
2. Explore the data and define credit risk targets.
3. Clean the data and develop predictive features.
4. Establish statistical and machine learning baselines.
5. Develop and evaluate credit scorecards.
6. Compare models and assess calibration and stability.
7. Translate model outputs into credit decision rules.
8. Package trained models and expose predictions through FastAPI.
9. Develop a Gradio application to consume the prediction API.
10. Test the complete application-to-model prediction workflow.
11. Containerise and deploy the application and prediction service.
12. Track experiments and monitor model performance.

## Disclaimer

All datasets used in this project are synthetic. The results are intended for educational and technical demonstration and should not be used to make real lending decisions.

## Project Status

This project is under active development. Analysis, model results, visualisations, API implementation and application integration will be documented as each component is completed.