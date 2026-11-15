# Bengaluru House Price Prediction

A Flask web app that estimates residential property prices in Bengaluru from a property's location, built-up area, number of bathrooms, and BHK count. The app uses a trained scikit-learn Ridge regression pipeline and displays estimates in Indian rupees.

## Features

- Choose a location from the locations in the cleaned dataset.
- Enter the property's square footage, number of bathrooms, and BHK count.
- Optionally enter a year to apply the app's 5% annual price adjustment for years after 2023.
- Get an estimated price from the saved model.

## Project files

| File | Description |
| --- | --- |
| `main.py` | Flask application and prediction endpoint |
| `templates/index.html` | Prediction form and results page |
| `RidgeModel.pkl` | Serialized preprocessing and Ridge regression pipeline |
| `Cleaned_data.csv` | Processed data used to populate the location selector |
| `Bengaluru_House_Data.csv` | Source Bengaluru housing dataset |
| `Predictor.ipynb` | Notebook covering data cleaning, model training, and model export |

## Requirements

- Python
- Flask
- NumPy
- pandas
- scikit-learn

The saved pickle model depends on scikit-learn. If loading it fails, install a scikit-learn version compatible with the one used to create `RidgeModel.pkl`.

## Run locally

1. Clone the repository and change into its directory:

   ```bash
   git clone <repository-url>
   cd House_price_prediction
   ```

2. (Optional) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   On Windows:

   ```powershell
   .venv\Scripts\Activate.ps1
   ```

   On macOS or Linux:

   ```bash
   source .venv/bin/activate
   ```

3. Install the dependencies:

   ```bash
   pip install Flask numpy pandas scikit-learn
   ```

4. Start the app from the project directory:

   ```bash
   python main.py
   ```

5. Open [http://127.0.0.1:5001](http://127.0.0.1:5001) in your browser.

## How predictions work

The training notebook prepares the housing data and evaluates Linear Regression, Lasso, and Ridge models. The deployed `RidgeModel.pkl` contains a pipeline that one-hot encodes the location, scales the features, and applies Ridge regression. The app converts the model's output from lakhs to rupees and returns the estimate. The optional year input applies the app's additional annual adjustment; it is not an input feature to the trained model.

The notebook reports an R² score of approximately `0.869` for its Ridge model evaluation. This is a notebook evaluation result, not a guarantee of prediction accuracy for an individual property.

## Notes

- Predictions are estimates based on the training data and are not professional valuations.
- Run `main.py` from the project directory so the app can find the CSV and model files.
- The Flask development server runs with debug mode enabled; use a production WSGI server and disable debug mode before deploying publicly.
