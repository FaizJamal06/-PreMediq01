# 🧠 PreMediq: Health Insurance Premium Predictor

Ever wondered why your health insurance premium hits harder than Monday morning? 👀  
**PreMediq** is an intelligent machine learning application that predicts health insurance premiums based on comprehensive user demographics and health factors. Built with advanced ML models and a user-friendly Streamlit interface.

**Live Demo:** https://premediq01.streamlit.app/

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Model Architecture](#model-architecture)
- [Input Parameters](#input-parameters)
- [Technical Implementation](#technical-implementation)
- [Dependencies](#dependencies)
- [Contributing](#contributing)

## 🎯 Overview

PreMediq leverages machine learning to provide accurate health insurance premium predictions by analyzing multiple factors including demographics, health conditions, lifestyle choices, and insurance plan preferences. The application uses age-segmented models to improve prediction accuracy across different age groups.

## 🚀 Features

- **🏥 Intelligent Premium Prediction**: Advanced ML models trained on comprehensive health insurance datasets
- **👥 Age-Segmented Modeling**: Separate optimized models for young adults (≤25) and older demographics (>25)
- **📊 Multi-Factor Analysis**: Considers 12+ key factors including demographics, health history, and lifestyle
- **🌐 Interactive Web Interface**: Clean, responsive Streamlit-based UI with real-time predictions
- **⚡ Real-Time Processing**: Instant predictions with preprocessing and feature engineering
- **🔒 Robust Data Handling**: Comprehensive input validation and error handling
- **📈 Normalized Risk Scoring**: Advanced medical history risk assessment algorithm

## 📁 Project Structure

```
PreMediq/
├── artifacts/                    # Trained models and preprocessing objects
│   ├── model_young.joblib       # ML model for users ≤25 years
│   ├── model_rest.joblib        # ML model for users >25 years
│   ├── scaler_young.joblib      # Feature scaler for young demographic
│   └── scaler_rest.joblib       # Feature scaler for older demographic
├── main.py                      # Streamlit web application interface
├── prediction_helper.py         # Core prediction logic and preprocessing
├── requirements.txt             # Python dependencies
└── README.md                    # Project documentation
```

## 🛠️ Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd PreMediq
   ```

2. **Create virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   streamlit run main.py
   ```

5. **Access the application**
   - Open your browser and navigate to `http://localhost:8501`

## 🎮 Usage

### Web Interface

1. **Launch the application** using `streamlit run main.py`
2. **Fill in the required information**:
   - Personal details (Age, Gender, Marital Status)
   - Financial information (Income, Number of Dependants)
   - Health factors (BMI Category, Medical History, Genetic Risk)
   - Lifestyle choices (Smoking Status, Employment Status)
   - Insurance preferences (Plan type, Region)
3. **Click "Predict"** to get your estimated premium
4. **View results** displayed in an easy-to-read format

### Programmatic Usage

```python
from prediction_helper import predict

# Example input
user_data = {
    'Age': 30,
    'Gender': 'Male',
    'Number of Dependants': 2,
    'Income in Lakhs': 8,
    'Genetical Risk': 2,
    'Insurance Plan': 'Gold',
    'Employment Status': 'Salaried',
    'Marital Status': 'Married',
    'BMI Category': 'Normal',
    'Smoking Status': 'No Smoking',
    'Region': 'Northwest',
    'Medical History': 'No Disease'
}

predicted_premium = predict(user_data)
print(f"Predicted Premium: ₹{predicted_premium}")
```

## 🧠 Model Architecture

### Age-Segmented Approach
- **Young Adult Model (≤25 years)**: Optimized for younger demographics with different risk profiles
- **General Adult Model (>25 years)**: Trained on broader age range with comprehensive feature set

### Feature Engineering
- **Normalized Risk Scoring**: Medical conditions weighted by severity
  - Diabetes: 6 points
  - Heart Disease: 8 points  
  - High Blood Pressure: 6 points
  - Thyroid: 5 points
  - Combined conditions: Additive scoring
- **Categorical Encoding**: One-hot encoding for categorical variables
- **Feature Scaling**: StandardScaler applied to numerical features

### Model Pipeline
1. **Input Validation**: Ensures all required fields are present
2. **Preprocessing**: Feature engineering and encoding
3. **Risk Calculation**: Medical history normalization
4. **Model Selection**: Age-based model routing
5. **Scaling**: Age-appropriate feature scaling
6. **Prediction**: Final premium estimation

## 📊 Input Parameters

### Required Fields

| Parameter | Type | Options/Range | Description |
|-----------|------|---------------|-------------|
| **Age** | Integer | 18-100 | User's age in years |
| **Gender** | Categorical | Male, Female | User's gender |
| **Number of Dependants** | Integer | 0-20 | Number of family dependants |
| **Income in Lakhs** | Integer | 0-200 | Annual income in Indian Lakhs |
| **Genetical Risk** | Integer | 0-5 | Genetic predisposition risk score |
| **Insurance Plan** | Categorical | Bronze, Silver, Gold | Desired insurance plan tier |
| **Employment Status** | Categorical | Salaried, Self-Employed, Freelancer | Current employment type |
| **Marital Status** | Categorical | Married, Unmarried | Marital status |
| **BMI Category** | Categorical | Normal, Obesity, Overweight, Underweight | Body Mass Index category |
| **Smoking Status** | Categorical | No Smoking, Regular, Occasional | Smoking habits |
| **Region** | Categorical | Northwest, Southeast, Northeast, Southwest | Geographic region |
| **Medical History** | Categorical | Various conditions | Current/past medical conditions |

### Medical History Options
- No Disease
- Diabetes
- High blood pressure  
- Diabetes & High blood pressure
- Thyroid
- Heart disease
- High blood pressure & Heart disease
- Diabetes & Thyroid
- Diabetes & Heart disease

## ⚙️ Technical Implementation

### Core Components

#### `main.py` - Streamlit Interface
- **Responsive Layout**: 4-row, 3-column grid layout for optimal UX
- **Input Validation**: Built-in Streamlit validators for numerical inputs
- **Real-time Updates**: Instant prediction on button click
- **Error Handling**: Graceful handling of invalid inputs

#### `prediction_helper.py` - Prediction Engine
- **Model Loading**: Efficient joblib-based model persistence
- **Feature Engineering**: Comprehensive preprocessing pipeline
- **Risk Assessment**: Advanced medical history scoring algorithm
- **Scaling Management**: Age-appropriate feature normalization

### Key Functions

#### `calculate_normalized_risk(medical_history)`
Converts medical history into normalized risk scores (0-1 scale):
- Parses complex medical conditions
- Applies evidence-based risk weights
- Normalizes to standard scale for model input

#### `preprocess_input(input_dict)`
Transforms raw user input into model-ready features:
- One-hot encoding for categorical variables
- Insurance plan numerical mapping
- Feature alignment with training data structure

#### `handle_scaling(age, df)`
Applies age-appropriate feature scaling:
- Routes to correct scaler based on age
- Maintains feature consistency across models
- Handles temporary columns for processing

#### `predict(input_dict)`
Main prediction orchestrator:
- Coordinates preprocessing pipeline
- Selects appropriate model based on age
- Returns integer premium prediction

## 📦 Dependencies

### Core ML & Data Processing
- **pandas (2.3.0)**: Data manipulation and analysis
- **numpy (2.3.1)**: Numerical computing foundation
- **scikit-learn (1.7.0)**: Machine learning algorithms and preprocessing
- **xgboost (3.0.2)**: Gradient boosting framework
- **joblib (1.5.1)**: Model serialization and persistence

### Web Application
- **streamlit (1.46.1)**: Interactive web application framework
- **altair (5.5.0)**: Statistical visualization library

### Supporting Libraries
- **scipy (1.16.0)**: Scientific computing utilities
- **pillow (11.2.1)**: Image processing capabilities
- **requests (2.32.4)**: HTTP library for API calls
- **python-dateutil (2.9.0.post0)**: Date/time utilities

### Development & Deployment
- **GitPython (3.1.44)**: Git repository interaction
- **watchdog (6.0.0)**: File system event monitoring
- **tornado (6.5.1)**: Web server framework

## 🤝 Contributing

We welcome contributions to improve PreMediq! Here's how you can help:

### Development Setup
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Add tests if applicable
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Areas for Contribution
- **Model Improvements**: Enhanced algorithms, feature engineering
- **UI/UX Enhancements**: Better interface design, accessibility
- **Documentation**: Code comments, user guides, API documentation
- **Testing**: Unit tests, integration tests, performance testing
- **Deployment**: Docker containerization, cloud deployment guides

### Code Style
- Follow PEP 8 Python style guidelines
- Add docstrings for all functions and classes
- Include type hints where appropriate
- Write descriptive commit messages

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Healthcare data providers for training datasets
- Open-source ML community for tools and frameworks
- Streamlit team for the excellent web framework

## 📞 Support

For questions, issues, or suggestions:
- Create an issue on GitHub
- Visit the live demo: https://premediq01.streamlit.app/

---

**Built with ❤️ for better healthcare accessibility**