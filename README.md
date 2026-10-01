# TSA-EPF — Time Series Analysis

Forecast de l'intérêt Google Trends pour la recherche **« Idée de cadeau »** en France.

## Approche

Décomposition de la série temporelle, puis recomposition pour le forecast.

## Dataset

`time_series_FR_20040101-0100_20261001-1602.csv` — intérêt mensuel (échelle 0–100), France, 2004–2026.

## Lancer le notebook

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Ouvrir `TSA_Report_Idee_de_cadeau.ipynb` et sélectionner le kernel `.venv`.
