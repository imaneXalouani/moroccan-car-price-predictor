# Moroccan Car Price Predictor

A Streamlit application that estimates **used-car asking prices in Moroccan dirhams (MAD)** from vehicle characteristics. It combines a serialized regression model with feature preparation and a guided user interface.

**Academic project by Marouane Daouki and Imane Alouani.**

## What the code demonstrates

- Preparing numeric and categorical vehicle features with Pandas and NumPy.
- Applying saved brand/model frequency mappings and location encodings.
- Loading a trained model and supporting artifacts through Joblib.
- Integrating predictions into a Streamlit interface with Plotly visualizations.

[Prediction logic](model.py) · [Application](app.py) · [Dependencies](requirements.txt)

## Prediction workflow

```mermaid
flowchart LR
    U[Vehicle details] --> F[Feature preparation and saved mappings]
    F --> M[Serialized regression model]
    M --> P[Estimated price in MAD]
    P --> S[Streamlit result]
```

Inputs include brand, model, year, mileage, fiscal power, doors, fuel, transmission, condition, origin and location.

## Run locally

```bash
git clone https://github.com/shirahex/moroccan-car-price-predictor.git
cd moroccan-car-price-predictor
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
streamlit run app.py
```

Open http://localhost:8501. Run from the repository root: the application and model code load the `.pkl` artifacts through relative paths. A serialized model may require library versions compatible with the original training environment; an exact training-environment lockfile is not included.

## Repository map

| File | Role |
| --- | --- |
| [app.py](app.py) | Input forms, prediction display and visualizations |
| [model.py](model.py) | Feature transformation and model inference |
| `best_car_price_model.pkl` | Saved model |
| `*_list.pkl`, `*_freq.pkl`, `*_mapping.pkl` | Category lists and feature mappings |
| [requirements.txt](requirements.txt) | Runtime packages |

The supporting artifacts are in the root directory. The raw listing dataset, scraping code and complete training/evaluation notebook are not included in this checkout.

## Data and evaluation

The project's original documentation identifies Avito.ma vehicle listings as the data source. Treat the prediction as an estimate of listing-market patterns rather than a verified transaction value.

Earlier documentation reported performance metrics, but the repository does not provide the split, evaluation predictions or training notebook needed to reproduce them. Consequently, this README does not present those numbers as verified results. A reproducible evaluation should publish the dataset snapshot, split procedure, training code, package versions and error analysis.

## Known limitations

The current feature-preparation code includes category fallbacks, notably mapping diesel to the petrol flag and mapping a customs-cleared origin to a local-origin flag. These choices can bias predictions and should be revisited against the original training pipeline before real valuation use. Unseen categories and market changes can also reduce reliability.

The price is an educational model output, not an official valuation, purchase recommendation or guarantee. Do not use application visualizations as evidence of current market statistics without the underlying dataset.

## Next improvements

Reconstruct a reproducible training pipeline, persist preprocessing with the estimator, validate category handling and report held-out MAE/RMSE alongside a simple baseline.

## Credits

Marouane Daouki · Imane Alouani. Original project created for academic purposes. This repository does not currently include a standalone software license.
