# Walmart Weekly Sales Prediction

## 🎯 Objectif du projet
Prédire les ventes hebdomadaires des magasins Walmart à partir d'indicateurs économiques et contextuels, afin d'aider les équipes marketing à planifier leurs campagnes.

## 📊 Jeu de données
- Fichier : `Walmart_Store_sales.csv`
- Variables :
  - `Store` : identifiant du magasin (catégoriel)
  - `Date` : semaine de l'observation
  - `Weekly_Sales` : ventes de la semaine (cible)
  - `Holiday_Flag` : indique si la semaine contient un jour férié
  - `Temperature`, `Fuel_Price`, `CPI`, `Unemployment` : indicateurs économiques

## 🧠 Méthodologie
1. **Analyse exploratoire** : visualisation des distributions, détection des outliers, corrélations.
2. **Prétraitement** :
   - Suppression des lignes où la cible est manquante.
   - Extraction de features temporelles (année, mois, jour, jour de la semaine, et composantes cycliques sin/cos).
   - Clipping des valeurs aberrantes (bornes à ±3 écarts-types).
   - Imputation des valeurs manquantes (moyenne pour les numériques, mode pour les catégorielles).
   - Standardisation des variables numériques et One‑Hot encoding des variables catégorielles (`Store`, `Holiday_Flag`).
3. **Modélisation** :
   - Régression linéaire (baseline).
   - Régression Ridge et Lasso avec sélection automatique du paramètre de régularisation par validation croisée.
4. **Évaluation** : R², RMSE, MAE sur un ensemble de test (20%).
5. **Interprétation** : analyse des coefficients pour identifier les facteurs influents.

## 📈 Résultats
| Modèle | R² (test) | RMSE | MAE |
|---|---|---|---|
| Régression linéaire | 0.96 | ~140 k$ | ~110 k$ |
| Ridge (retenu) | **0.97** | **~115 k$** | **~85 k$** |
| Lasso | 0.96 | ~130 k$ | ~100 k$ |

- Le modèle **Ridge** offre la meilleure généralisation.
- Les facteurs les plus influents sont la saisonnalité (composantes cycliques), le CPI et le taux de chômage.
- Certains magasins présentent structurellement des ventes plus élevées.

## 📁 Structure du projet
Walmart_Sales/
├── Walmart_Store_sales.csv # Données brutes
├── Walmart_Ds2.ipynb # Notebook principal (code + analyses)
├── README.md # Ce fichier
├── requirements.txt # Dépendances Python figées
└── .gitignore # Fichiers à exclure de Git


## ⚙️ Installation

### 1. Cloner le dépôt
```bash
git clone <url-du-repo>
cd Walmart_Sales


### 2. Créer et activer un environnement virtuel 
python3 -m venv venv
source venv/bin/activate        # Sur Windows : venv\Scripts\activate

### 3. Installer les dépendances
pip install -r requirements.txt

### 4. Enregistrer le kernel pour Jupyter/ VS Code
python -m ipykernel install --user --name=walmart_venv --display-name="Python (Walmart Venv)"



### Utilisation
Ouvrir Walmart_Ds2.ipynb dans VS Code ou Jupyter Lab.

Sélectionner le kernel "Python (Walmart Venv)".

Exécuter toutes les cellules (Run All).

### Technologies utilisées
Python 3.9+

pandas, numpy

scikit-learn

matplotlib, seaborn

Jupyter / VS Code

### Limites et perspectives
Taille modeste du dataset (136 lignes après nettoyage).

Multicolinéarité entre CPI et Unemployment.

Pistes : intégrer des données externes (météo, événements), tester des modèles non-linéaires (Random Forest, XGBoost), déployer une API.
