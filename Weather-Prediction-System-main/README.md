# 🌤️ Weather Prediction System

A comprehensive machine learning-powered weather prediction web application that forecasts weather conditions, temperature, wind speed, humidity, pressure, and other meteorological parameters based on geographic coordinates and current weather data.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Model Details](#model-details)
- [API Endpoints](#api-endpoints)
- [Screenshots](#screenshots)

## 🌟 Overview

This Weather Prediction System is a Flask-based web application that leverages machine learning to predict various weather parameters. The system uses both regression and classification models to provide comprehensive weather forecasts, including temperature, wind speed, humidity, pressure, cloud cover, precipitation, UV index, and weather conditions.

The application features an intuitive web interface with multiple input methods (coordinates, location names, or GPS), real-time predictions, and downloadable weather reports in PDF format.

## ✨ Features

### 🎯 Core Functionality
- **Multi-parameter Weather Prediction**: Temperature, wind speed, humidity, pressure, cloud cover, precipitation, UV index
- **Weather Condition Classification**: Predicts specific weather conditions (sunny, cloudy, rainy, etc.)
- **Multiple Input Methods**:
  - Manual latitude/longitude entry
  - Location name search with automatic coordinate lookup
  - GPS-based current location detection
- **PDF Report Generation**: Download detailed weather prediction reports
- **Responsive Web Interface**: Modern, mobile-friendly design

### 🤖 Machine Learning Models
- **Linear Regression Model**: For predicting continuous weather parameters
- **Random Forest Classifier**: For weather condition classification
- **Label Encoding**: Handles categorical weather conditions
- **Feature Engineering**: Optimized feature selection and preprocessing

### 🎨 User Experience
- **Interactive Web Interface**: Clean, modern design with gradient backgrounds
- **Real-time Validation**: Input validation and error handling
- **Geolocation Integration**: Automatic location detection
- **Visual Feedback**: Loading states and smooth transitions

## 🛠️ Technologies Used

### Backend
- **Python 3.x**: Core programming language
- **Flask**: Web framework for API and web interface
- **scikit-learn**: Machine learning library for model training and prediction
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **joblib**: Model serialization and loading

### Frontend
- **HTML5**: Structure and markup
- **CSS3**: Styling with modern features (gradients, transitions)
- **JavaScript (ES6+)**: Interactive functionality and API calls
- **OpenStreetMap Nominatim API**: Geocoding service for location lookup

### Data & Visualization
- **matplotlib**: Data visualization and plotting
- **seaborn**: Statistical data visualization
- **ReportLab**: PDF generation for weather reports

### Data Management
- **CSV**: Weather dataset storage
- **Pickle**: Model serialization format

## 📦 Installation

### Prerequisites
- Python 3.7 or higher
- pip (Python package installer)

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd weather-prediction-system
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Train the models** (if models are not pre-trained)
   ```bash
   python train_model.py
   ```

5. **Run the application**
   ```bash
   python app.py
   ```

6. **Access the application**
   - Open your browser and navigate to `http://localhost:5000`

## 🚀 Usage

### Web Interface Usage

1. **Launch the Application**: Start the Flask server and open the web interface
2. **Choose Input Method**:
   - **Coordinates**: Enter latitude and longitude manually
   - **Location Name**: Enter city/country name and get coordinates automatically
   - **Current Location**: Use GPS to get your current coordinates
3. **Enter Weather Data**: Input current temperature, wind speed, pressure, and humidity
4. **Get Prediction**: Click "Predict" to receive comprehensive weather forecast
5. **Download Report**: Generate and download a PDF report of the prediction

### Programmatic Usage

```python
# Load the trained models
import joblib
import pandas as pd

reg_model = joblib.load('models/weather_regressor.pkl')
cls_model = joblib.load('models/weather_classifier.pkl')
label_encoder = joblib.load('models/label_encoder.pkl')

# Prepare input data
input_data = {
    'latitude': 40.7128,
    'longitude': -74.0060,
    'temperature_celsius': 20.0,
    'wind_mph': 10.0,
    'pressure_mb': 1013.25,
    'humidity': 65.0
}

# Make predictions
input_df = pd.DataFrame([input_data])
regression_prediction = reg_model.predict(input_df)
classification_prediction = cls_model.predict(input_df)
weather_condition = label_encoder.inverse_transform([classification_prediction[0]])[0]
```

## 📁 Project Structure

```
weather-prediction-system/
├── app.py                          # Main Flask application
├── train_model.py                  # Model training script
├── utils.py                        # Utility functions
├── requirements.txt                # Python dependencies
├── README.md                       # Project documentation
├── data/
│   └── weather_data.csv           # Weather dataset
├── models/
│   ├── weather_regressor.pkl      # Regression model
│   ├── weather_classifier.pkl     # Classification model
│   └── label_encoder.pkl          # Label encoder
├── templates/
│   └── index.html                 # Main web interface
├── static/
│   ├── style.css                  # CSS styling
│   ├── script.js                  # JavaScript functionality
│   ├── *.png                      # Visualization images
│   └── weather_report.pdf         # Generated reports
└── venv/                          # Virtual environment
```

## 🧠 Model Details

### Dataset
- **Source**: Weather data from multiple global locations
- **Features**: Latitude, longitude, temperature, wind speed, pressure, humidity
- **Target Variables**: 
  - Regression: temperature, wind speed, humidity, pressure, cloud cover, precipitation, UV index
  - Classification: weather condition (sunny, cloudy, rainy, etc.)

### Model Architecture
- **Regression Model**: Linear Regression for continuous value prediction
- **Classification Model**: Random Forest with 100 estimators for weather condition classification
- **Preprocessing**: Label encoding for categorical variables, data cleaning and normalization

### Performance Metrics
- **Regression**: Mean Absolute Error (MAE) evaluation
- **Classification**: Accuracy score for weather condition prediction
- **Validation**: 80/20 train-test split with random state for reproducibility

## 🔌 API Endpoints

### `GET /`
- **Description**: Main application interface
- **Response**: HTML page with weather prediction form

### `POST /predict`
- **Description**: Weather prediction endpoint
- **Parameters**:
  - `latitude` (float): Geographic latitude
  - `longitude` (float): Geographic longitude
  - `temperature_celsius` (float): Current temperature
  - `wind_mph` (float): Wind speed in mph
  - `pressure_mb` (float): Atmospheric pressure in mb
  - `humidity` (float): Humidity percentage
- **Response**: HTML page with prediction results

### `POST /download_report`
- **Description**: Generate and download PDF weather report
- **Parameters**: Prediction data from previous request
- **Response**: PDF file download
