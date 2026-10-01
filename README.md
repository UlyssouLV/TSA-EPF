# TSA-EPF — Time Series Analysis

Forecast de l'intérêt Google Trends pour la recherche **« Idée de cadeau »** en France.

## Approche

Décomposition de la série temporelle, puis recomposition pour le forecast.

## Dataset

`time_series_FR_20040101-0100_20261001-1602.csv` — intérêt mensuel (échelle 0–100), France, 2004–2026.

## Plan de décomposition

### Fait
1. Modèle de décomposition (Buys-Ballot → additif / multiplicatif)
2. Présence de \(T_t\) et \(S_t\) (Fisher)
3. Ordre d'extraction par impact de variance → **\(S_t \rightarrow T_t \rightarrow R_t\)**
4. Extraction de \(S_t\) (coeffs + conservation + désaisonnalisation → \(Y_t^{SA}\))

### À faire

**B — Extraire \(T_t\)** sur \(Y_t^{SA}\) (série déjà désaisonnalisée)
- Pas de régression sur \(Y_t\) brut (\(S_t\) présent)
- Trend déterministe → régression OLS ; sinon → MA / lissage / lissage expo
- Stocker \(T_t\)

**C — Obtenir \(R_t\)**
- Multiplicatif : \(R_t = Y_t^{SA} / T_t\) (ou équivalent selon le modèle)
- Vérifier / visualiser le résidu

**D — Forecast de chaque composant**
- \(S_t\) : répéter le profil saisonnier \(s_j^*\)
- \(T_t\) : prolonger la régression ou le lissage
- \(R_t\) : moyenne naïve / MA(p) / lissage expo

**E — Recomposition**
- Additif : \(\hat{Y} = \hat{T} + \hat{S} + \hat{R}\)
- Multiplicatif : \(\hat{Y} = \hat{T} \times \hat{S} \times \hat{R}\)

## Lancer le notebook

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Ouvrir `TSA_Report_Idee_de_cadeau.ipynb` et sélectionner le kernel `.venv`.
