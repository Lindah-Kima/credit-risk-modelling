# Credit Risk Modelling

A practical credit risk project focused on borrower risk assessment, credit scorecard development, default prediction and lending decisions using statistical analysis and machine learning.

**Status:** In Development

---

## 1. Project Overview

This project explores how financial institutions assess and manage credit risk using customer, loan and repayment data.

Using synthetic datasets generated with Tonic Fabricate, the project covers credit risk measurement, exploratory data analysis, statistical modelling, machine learning, scorecard development and portfolio analysis.

The objective is to build an end-to-end credit risk modelling workflow, from data preparation and model development to model evaluation, API integration and application-level prediction.

The project also explores how predictive models can be integrated into applications, allowing users to submit borrower information, receive model-generated predictions and interpret the results through an interactive interface.

---

## 2. Key Areas

### 2.1 Exploratory Data Analysis

- Analyse customer demographics, financial characteristics and loan behaviour.
- Investigate default patterns across customer and loan segments.
- Identify relationships between borrower characteristics and repayment outcomes.
- Examine missing values, outliers and class imbalance.

### 2.2 Credit Risk Measurement

- **Probability of Default (PD):** Estimate the likelihood of a borrower defaulting over a defined period.
- **Exposure at Default (EAD):** Estimate the outstanding exposure when default occurs.
- **Loss Given Default (LGD):** Estimate the proportion of exposure not recovered after default.
- **Expected Loss (EL):** Calculate expected credit loss using PD × EAD × LGD.

### 2.3 Credit Scorecard Development

- Data binning and variable transformation.
- Weight of Evidence (WOE) and Information Value (IV).
- Logistic regression modelling.
- Scorecard development and scaling.
- Score interpretation and reason codes.

### 2.4 Default Prediction

- Develop models to estimate borrower default risk.
- Establish a logistic regression baseline.
- Compare machine learning models such as Random Forest and XGBoost.
- Handle class imbalance and feature selection.
- Evaluate model performance and probability calibration.

### 2.5 Loan Limit Modelling

- Analyse historical lending patterns and customer affordability indicators.
- Develop models to estimate potential loan limits.
- Evaluate predictions against historical lending outcomes.
- Apply affordability and risk-based lending constraints.

### 2.6 Credit Decisioning

- Combine credit scores, predicted default probabilities and lending rules.
- Define approval, rejection and manual review criteria.
- Generate decision explanations.
- Examine the impact of different decision thresholds.

### 2.7 Portfolio Risk Analysis

- Analyse portfolio exposure and expected losses.
- Compare default rates across customer segments.
- Examine risk concentration and portfolio composition.
- Develop visualisations for monitoring portfolio performance.

### 2.8 Model Serving and Application Integration

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

---

## 3. Modelling and Evaluation

Models will be assessed using metrics appropriate to credit risk, including:

- ROC-AUC and Gini coefficient.
- Kolmogorov-Smirnov (KS) statistic.
- Precision, recall and F1-score.
- Confusion matrix and classification thresholds.
- Brier score and probability calibration.
- Population Stability Index (PSI).
- Feature importance and model explainability.

Time-based validation will be used where the data supports it, with particular attention to target leakage and observation windows.

---

## 4. Technology Stack

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

---

## 5. Architecture

The project follows a layered architecture separating data management, model development, prediction services and application interaction.

### 5.1 End-to-End Workflow

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

### 5.2 Application Prediction Flow

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

---

## 6. Repository Structure

The project is organised into separate directories to keep data, modelling logic, application code, configuration and documentation manageable as the project grows.

```text
credit-risk-modelling/
│
├── .github/
│   └── workflows/                  # GitHub Actions workflows for automated testing and CI/CD
│
├── api/                            # FastAPI backend, API routes and prediction endpoints
│
├── app/                            # Gradio interface for user inputs and prediction results
│
├── configs/                        # Application, model and experiment configuration files
│
├── data/
│   ├── raw/                        # Original synthetic datasets
│   ├── interim/                    # Data undergoing cleaning and transformation
│   └── processed/                  # Cleaned datasets ready for analysis and modelling
│
├── docker/                         # Dockerfiles and Docker-related configuration
│
├── docs/                           # Technical documentation, methodology and project notes
│
├── logs/                           # Application, API and model execution logs
│
├── migrations/                     # Database schema changes and migration scripts
│
├── models/                         # Saved models and preprocessing artefacts
│
├── notebooks/                      # Jupyter notebooks for exploration and experimentation
│
├── reports/
│   ├── figures/                    # Charts, graphs and visual outputs
│   └── summaries/                  # Analysis findings and model evaluation summaries
│
├── scripts/                        # Standalone scripts for data preparation, training and other tasks
│
├── sql/                            # SQL queries for data extraction and manipulation
│
├── src/
│   └── credit_risk/
│       ├── __init__.py
│       │
│       ├── data/                   # Data loading, cleaning and preparation functions
│       ├── features/               # Feature engineering and variable transformations
│       ├── evaluation/             # Model evaluation metrics and validation procedures
│       ├── models/                 # Model training, inference and prediction logic
│       ├── scoring/                # Scorecard development, WOE, IV and score scaling
│       └── decisioning/            # Credit decision rules, risk grades and lending recommendations
│
├── tests/                          # Automated tests for data, models, APIs and application logic
│
├── utils/                          # General-purpose reusable helper functions
│
├── .dockerignore                   # Files and folders excluded from Docker build context
├── .editorconfig                   # Shared code formatting and editor settings
├── .env.example                    # Template for required environment variables
├── .gitignore                      # Files and folders Git should not track
├── .python-version                 # Intended Python version for the project
├── pyproject.toml                  # Project metadata, dependencies and development tool configuration
├── README.md                       # Project overview and documentation
└── requirements.txt                # Python package dependencies
```

### 6.1 Understanding the Main Directories

| Directory | Purpose |
|---|---|
| `.github/workflows/` | Automates tasks such as running tests when changes are pushed to GitHub. |
| `api/` | Contains the FastAPI backend that receives application requests and returns model predictions. |
| `app/` | Contains the Gradio interface that users interact with. |
| `configs/` | Stores settings that control how different parts of the project run. |
| `data/` | Organises datasets according to their stage of preparation. |
| `docker/` | Contains instructions for packaging the application and its dependencies into containers. |
| `docs/` | Holds explanations of how the project works and the methodologies used. |
| `logs/` | Keeps records of application activity, errors and execution events. |
| `migrations/` | Tracks changes made to database tables and structures over time. |
| `models/` | Stores trained models and supporting files required to make predictions. |
| `notebooks/` | Provides an interactive environment for exploring data and experimenting with modelling approaches. |
| `reports/` | Stores analysis outputs, charts and model evaluation results. |
| `scripts/` | Holds standalone Python scripts for specific project tasks. |
| `sql/` | Stores SQL statements used to retrieve and manipulate data. |
| `src/credit_risk/` | Contains the reusable Python code powering the credit risk functionality. |
| `tests/` | Contains automated checks to ensure different parts of the project work correctly. |
| `utils/` | Holds general helper functions shared across the project. |

### 6.2 Understanding the Main Python Modules

Within `src/credit_risk/`, responsibilities are separated into smaller modules:

| Module | Purpose |
|---|---|
| `data/` | Loads, cleans and prepares datasets. |
| `features/` | Creates and transforms variables used by the models. |
| `evaluation/` | Measures model performance and validates predictions. |
| `models/` | Handles model training, loading and inference. |
| `scoring/` | Develops and manages credit scorecards, including WOE, IV and score scaling. |
| `decisioning/` | Converts model outputs into lending decisions and risk categories. |

**Architecture principle:** Keep reusable business and modelling logic inside `src/credit_risk/`. The API and Gradio application should consume this functionality rather than duplicate it.

---

## 7. Development Approach

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

---

## 8. Disclaimer

All datasets used in this project are synthetic. The results are intended for educational and technical demonstration and should not be used to make real lending decisions.

---

## 9. Project Status

This project is under active development. Analysis, model results, visualisations, API implementation and application integration will be documented as each component is completed.