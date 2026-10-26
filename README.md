# EmberWatch

EmberWatch is a Flask web application that estimates the **Fire Weather Index (FWI)** from weather observations and fire-weather indicators. It uses a trained Ridge Regression model and a fitted `StandardScaler` stored in the `models/` directory.

## Features

- Landing page with an overview of the prediction workflow.
- Form-based FWI prediction at `/predictdata`.
- Prediction model and preprocessing artifacts included in the repository.
- Exploratory data analysis and model-training notebooks.
- AWS Elastic Beanstalk WSGI configuration.

## Requirements

- Python 3.9 or newer
- `pip`

Install the Python dependencies in a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows PowerShell, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

## Run locally

Start the Flask application:

```bash
python application.py
```

Then open [http://localhost:5001](http://localhost:5001) in a browser. The application listens on `0.0.0.0:5001` by default.

## Prediction inputs

The predictor expects the following numeric values:

| Input | Unit or encoding |
| --- | --- |
| Temperature | °C |
| RH | Relative humidity (%) |
| Ws | Wind speed (km/h) |
| Rain | Rainfall (mm) |
| FFMC | Fine Fuel Moisture Code |
| DMC | Duff Moisture Code |
| ISI | Initial Spread Index |
| Classes | Numeric class encoding |
| Region | Numeric region encoding |

Use the same units and encoding scheme used when the model was trained. The result is a model estimate and should be treated as one input to operational decision-making, not as a substitute for expert assessment.

## Project structure

```text
.
├── application.py                 # Flask application and prediction route
├── models/
│   ├── ridge.pkl                  # Trained Ridge Regression model
│   └── scaler.pkl                 # Fitted feature scaler
├── notebooks/
│   ├── 2.0-EDA And FE Algerian Forest Fires.ipynb
│   ├── 3.0-Model Training.ipynb
│   └── Algerian_forest_fires_dataset.csv
├── static/style.css               # Application styles
├── templates/                     # Flask HTML templates
├── requirements.txt               # Python dependencies
└── .ebextensions/python.config    # AWS Elastic Beanstalk WSGI settings
```

## Notebooks and data

The notebooks use the Algerian Forest Fires dataset, which contains observations from the Bejaia and Sidi Bel-Abbes regions of Algeria. The included analysis covers exploratory data analysis, feature engineering, and model training.

To work with the notebooks:

```bash
pip install jupyter
jupyter notebook
```

Open the notebooks from the `notebooks/` directory. Some notebook cells contain local development paths or refer to intermediate datasets that are not part of the application runtime.

## AWS Elastic Beanstalk

The repository includes `.ebextensions/python.config`, which configures Elastic Beanstalk to use `application:application` as the WSGI entry point. Deploy the repository as a Python application after installing the dependencies from `requirements.txt`.

## License

No license is currently specified for this project.
