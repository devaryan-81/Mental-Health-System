# Mental Health Score Predictor

A machine learning web application that predicts a student’s mental health score based on social-media usage, academic habits, lifestyle, and stress levels.

> This project is for educational purposes only. It is not a medical tool, diagnosis, or replacement for professional mental-health support.

## Project Structure

```text
Mental_health_score_predictor/
├── Student Social Media And Mental Health Impact.csv
├── regression.ipynb
├── Mental_Health_Pipeline.pkl
├── main.py
├── requirements.txt
├── index.html
├── script.js
├── style.css
└── .venv/
```

## Features

- Predicts a continuous mental-health score
- Interactive web interface
- FastAPI backend
- Pydantic input validation
- Pre-trained scikit-learn regression pipeline
- Responsive frontend design
- Client-side and server-side validation
- Score interpretation using three signal bands:
  - Strained
  - Balanced
  - Strong

## Input Features

The model uses the following student information:

```text
Age
Gender
Country
Academic Level
Most Used Platform
Purpose of Use
Average Daily Usage Hours
Daily Unlocks
Study Hours
Physical Activity Hours
Sleep Hours Per Night
Stress Level
```

The target variable is:

```text
Mental_Health_Score
```

## Technologies Used

- Python
- FastAPI
- Uvicorn
- Pydantic
- Pandas
- Scikit-learn
- Joblib
- HTML
- CSS
- JavaScript
- Jupyter Notebook

## Requirements

Install the Python dependencies listed in `requirements.txt`:

```text
fastapi
uvicorn
pydantic
joblib
pandas
scikit-learn
```

Python 3.12 or newer is recommended.

## Installation

Open PowerShell in the project directory:

```powershell
cd "E:\PYTHON (COURSE)\Mental_health_score_predictor"
```

Create a virtual environment:

```powershell
py -3.12 -m venv .venv
```

Activate the environment:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If PowerShell blocks activation, run:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

## Run the Backend

Start the FastAPI server:

```powershell
uvicorn main:app --reload
```

The API will run at:

```text
http://127.0.0.1:8000
```

Available endpoints:

```text
GET  /
POST /predict
GET  /docs
```

FastAPI documentation:

```text
http://127.0.0.1:8000/docs
```

## Run the Frontend

The frontend currently sends requests to the deployed API:

```javascript
const API_BASE = "https://mental-health-system-148g.onrender.com";
```

To use the local backend, update it in `script.js`:

```javascript
const API_BASE = "http://127.0.0.1:8000";
```

Start a local frontend server in a second terminal:

```powershell
python -m http.server 5500
```

Open the application:

```text
http://127.0.0.1:5500
```

Using a local web server is recommended instead of opening `index.html` directly.

## LIVE LINK

[Deployed website](https://mental-health-system-1-4y2a.onrender.com/)

## API Request Example

Send a `POST` request to:

```text
http://127.0.0.1:8000/predict
```

Example JSON body:

```json
{
  "age": 21,
  "gender": "Male",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Entertainment",
  "avg_daily_usage_hours": 5.5,
  "daily_unlocks": 65,
  "study_hours": 4,
  "physical_activity_hours": 1,
  "sleep_hours_per_night": 7,
  "stress_level": "Medium"
}
```

Example response:

```json
{
  "predicted_mental_health_score": 7.42
}
```

## Backend Validation

The API validates the following values:

- Age: between 10 and 100
- Average daily usage: between 0 and 24 hours
- Study hours: between 0 and 24 hours
- Physical activity: between 0 and 24 hours
- Sleep: between 0 and 24 hours
- Daily unlocks: zero or greater
- Gender: `Male` or `Female`
- Academic level: `High School`, `Undergraduate`, or `Graduate`
- Stress level: `Low`, `Medium`, `High`, or `Very High`

Countries outside the main country list are grouped as `other` during prediction.

## Machine Learning Workflow

The `regression.ipynb` notebook contains the complete machine-learning workflow:

1. Load the student mental-health dataset
2. Inspect the data
3. Analyze missing values
4. Explore numerical and categorical features
5. Study relationships between features and mental-health score
6. Split the data into training and testing sets
7. Build preprocessing pipelines
8. Train regression models
9. Tune model parameters
10. Evaluate model performance
11. Save the final pipeline as `Mental_Health_Pipeline.pkl`

The saved pipeline contains preprocessing and the trained regression model together, allowing the API to make predictions from raw input data.

## Model File

The backend loads the trained model from:

```text
Mental_Health_Pipeline.pkl
```

This file must be located in the same directory as `main.py`.

## Deployment

Example deployment configuration for Render or a similar platform:

```text
Build Command:
pip install -r requirements.txt
```

```text
Start Command:
uvicorn main:app --host 0.0.0.0 --port $PORT
```

The deployment must include:

```text
main.py
requirements.txt
Mental_Health_Pipeline.pkl
```

## Troubleshooting

### Model file not found

Make sure `Mental_Health_Pipeline.pkl` is in the same folder as `main.py`.

### Cannot connect to the API

Check that:

- The FastAPI server is running
- The API URL in `script.js` is correct
- The frontend is being served through `http://127.0.0.1:5500`
- Port `8000` is available

### Validation error

Check that all required fields are filled and that values match the allowed ranges and categories.

## Disclaimer

This application estimates a score based on patterns in a dataset. It should not be used to diagnose mental-health conditions or make medical decisions. Anyone experiencing distress should contact a qualified mental-health professional or an appropriate local support service.
