# Modélisation des risques d'AVC à l'aide de la statistique des extrêmes et du machine learning

_Projet de mémoire de Master en Data Science / Mathématiques appliquées_

## Contexte et objectif

Ce dépôt contient le code et les documents associés à mon mémoire intitulé  
**« Modélisation des risques d'AVC à l'aide de la statistique des extrêmes et des techniques de machine learning »**.[file:1]

L’objectif est d’identifier et de quantifier le risque d’AVC en fonction de différents facteurs (âge, hypertension, maladie cardiaque, taux de glucose, IMC, tabagisme, etc.) en combinant :
- Analyse exploratoire des données.
- Régression logistique.
- Méthodes de statistique des extrêmes (POT, GEV).
- Modèles de machine learning (avec rééchantillonnage SMOTE, normalisation, etc.).[file:1][web:8][web:11]

## Données

- **Source** : à compléter (base publique / base hospitalière / autre).[file:1]  
- **Nombre d’observations** : 5110.[file:1]  
- **Nombre de variables** : 11 (3 numériques, 8 catégorielles).[file:1]  

Principales variables utilisées :
- `Genre` : sexe du patient (Male, Female, Other) – catégorielle.[file:1]  
- `Age` : âge en années – numérique.[file:1]  
- `Hypertension` : 1 si hypertension, 0 sinon.[file:1]  
- `MaladieCardiaque` : 1 si maladie cardiaque, 0 sinon.[file:1]  
- `SituationMatrimoniale` : statut matrimonial (Yes/No).[file:1]  
- `Typetravail` : type d’emploi (Private, Self-employed, etc.).[file:1]  
- `Residence` : milieu de résidence (Urban/Rural).[file:1]  
- `Tauxglucosemoyen` : moyenne du taux de glucose – numérique.[file:1]  
- `IMC` : indice de masse corporelle – numérique.[file:1]  
- `StatutFumer` : tabagisme (never smoked, formerly smoked, smokes, unknown).[file:1]  
- `AVC` : variable cible, 1 si AVC, 0 sinon.[file:1]  

## Méthodologie

### 1. Analyse exploratoire des données (EDA)

- Description statistique des variables.
- Visualisation de la distribution des variables (histogrammes, boxplots).
- Analyse bivariée entre les facteurs de risque et la variable AVC.[file:1]

### 2. Modélisation par régression logistique

- Modèle initial avec toutes les variables explicatives.
- Sélection de variables par méthode **backward**.[file:1]  
- Estimation des **odds ratios** et de leurs intervalles de confiance (âge, hypertension, maladie cardiaque, taux de glucose, etc.).[file:1]  
- Calcul des probabilités prédites d’AVC :
  - En fonction de l’âge seulement.
  - En fonction de l’âge et de l’hypertension / maladie cardiaque.
  - Par classes d’âge (découpage en 3 classes) et facteurs de risque.[file:1]

### 3. Statistique des extrêmes (POT, GEV)

- Modélisation de la queue de distribution de certains indicateurs (par exemple taux de glucose ou âge extrêmes, à préciser selon ton mémoire).  
- Ajustement de modèles POT/GEV pour estimer le risque dans des situations extrêmes.[file:1]

*(Tu pourras détailler ici : choix du seuil, diagnostics, interprétation des paramètres.)*

### 4. Modèles de machine learning

- Rééchantillonnage des données avec **SMOTE** pour traiter le déséquilibre de la variable cible.[file:1]  
- Normalisation des variables numériques.[file:1]  
- Séparation en **train** et **test** (par exemple 70 % / 30 %).  
- Entraînement d’un modèle (régression logistique ML, ou autres modèles que tu as utilisés).  
- Évaluation des performances :
  - Matrice de confusion.
  - Taux de bon et mauvais classement.
  - AUC, courbe ROC, etc.[file:1][web:9]

## Structure du dépôt

```text
.
├── data/
│   └── base_avc.csv           # Données brutes (ou script pour les télécharger)
├── R/                         # Scripts R
│   ├── 01_eda.R               # Analyse exploratoire
│   ├── 02_logistic_regression.R
│   ├── 03_extreme_values.R    # POT, GEV
│   ├── 04_ml_models.R         # SMOTE, ML, métriques
│   └── utils.R                # Fonctions utilitaires (si besoin)
├── reports/
│   ├── 01_eda_report.pdf
│   ├── 02_logistic_report.pdf
│   ├── 03_extremes_report.pdf
│   └── 04_ml_report.pdf
├── figures/
│   ├── prob_avc_age.png
│   ├── prob_avc_age_htn_heart.png
│   └── boxplots_risk_factors.png
└── README.md
