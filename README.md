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

### À faire

**A — Extraire \(S_t\)** (plus gros impact)
- Coefficients saisonniers (moyennes par mois)
- Principe de conservation : additif → moyenne des coeffs = 0 ; multiplicatif → moyenne = 1
- Désaisonnaliser \(Y_t\)

**B — Extraire \(T_t\)** sur la série désaisonnalisée
- Si \(S_t\) présent : pas de régression directe sur \(Y_t\) brut
- Trend déterministe → régression ; sinon → MA / lissage / lissage expo

**C — Obtenir \(R_t\)**
- Reste après retrait de \(S_t\) et \(T_t\)

**D — Forecast de chaque composant**
- \(S_t\) : profil saisonnier ; \(T_t\) : prolonger le modèle ; \(R_t\) : moyenne / MA(p) / lissage expo

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
