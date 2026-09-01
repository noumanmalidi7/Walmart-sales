# Walmart Weekly Sales Prediction

## 🎯 Objectif du projet
Prédire les ventes hebdomadaires des magasins Walmart à partir d'indicateurs économiques et contextuels, afin d'aider les équipes marketing à planifier leurs campagnes.

## 📊 Jeu de données
- Fichier : `Walmart_Store_sales.csv` (fourni dans le cadre du projet)
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

## 📁 Structure du projet
├── Walmart_Store_sales.csv # Données brutes
├── Walmart_Ds2.ipynb # Notebook principal (code et analyses)
├── README.md # Ce fichier
└── requirements.txt # Dépendances Python
