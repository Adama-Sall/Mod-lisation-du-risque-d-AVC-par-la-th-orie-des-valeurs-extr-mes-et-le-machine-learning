# Modélisation des risques d'AVC à l'aide de la statistique des extrêmes et du machine learning

_Projet de mémoire de Master en Data Science / Mathématiques appliquées_

## Contexte et objectif





Ce dépôt contient le code et les documents associés à mon mémoire intitulé  
**« Modélisation des risques d'AVC à l'aide de la statistique des extrêmes et des techniques de machine learning »**.
Ce projet vise à modéliser et prédire le risque d’AVC en combinant des approches issues de la théorie des valeurs extrêmes (EVT) et du machine learning (ML).

L’objectif est d’identifier et de quantifier le risque d’AVC en fonction de différents facteurs (âge, hypertension, maladie cardiaque, taux de glucose, IMC, tabagisme, etc.) en combinant :
- Analyse exploratoire des données.
- Régression logistique.
- Méthodes de statistique des extrêmes (POT, GEV).
- Modèles de machine learning (avec rééchantillonnage SMOTE, normalisation, etc.).

- Ce travail a été réalisé dans le cadre d’un mémoire de Master en Mathématiques appliquées / Science des données.

## Données

- **Source** : à compléter (base publique / base hospitalière / autre). 
- **Nombre d’observations** : 5110.  
- **Nombre de variables** : 11 (3 numériques, 8 catégorielles).  

Principales variables utilisées :
- `Genre` : sexe du patient (Male, Female, Other) – catégorielle. 
- `Age` : âge en années – numérique. 
- `Hypertension` : 1 si hypertension, 0 sinon. 
- `MaladieCardiaque` : 1 si maladie cardiaque, 0 sinon. 
- `SituationMatrimoniale` : statut matrimonial (Yes/No).  
- `Typetravail` : type d’emploi (Private, Self-employed, etc.). 
- `Residence` : milieu de résidence (Urban/Rural).  
- `Tauxglucosemoyen` : moyenne du taux de glucose – numérique. 
- `IMC` : indice de masse corporelle – numérique. 
- `StatutFumer` : tabagisme (never smoked, formerly smoked, smokes, unknown). 
- `AVC` : variable cible, 1 si AVC, 0 sinon. 

## Méthodologie

### 1. Analyse exploratoire des données (EDA)

- Description statistique des variables.
- Visualisation de la distribution des variables (histogrammes, boxplots).
- Analyse bivariée entre les facteurs de risque et la variable AVC.

### 2. Modélisation par régression logistique

- Modèle initial avec toutes les variables explicatives.
- Sélection de variables par méthode **backward**. 
- Estimation des **odds ratios** et de leurs intervalles de confiance (âge, hypertension, maladie cardiaque, taux de glucose, etc.). 
- Calcul des probabilités prédites d’AVC :
  - En fonction de l’âge seulement.
  - En fonction de l’âge et de l’hypertension / maladie cardiaque.
  - Par classes d’âge (découpage en 3 classes) et facteurs de risque.

### 3. Statistique des extrêmes

Cette section applique la **théorie des valeurs extrêmes** pour étudier le comportement du risque d’AVC dans des situations extrêmes (par exemple valeurs très élevées d’âge, de taux de glucose ou de probabilité prédite d’AVC).  

#### 3.1 Modèle GEV (Generalized Extreme Value)

**Approche par maxima de blocs :**
- Construction de blocs (par exemple par période, par sous-groupes d’âge ou par partitions des données) et extraction des maxima de la variable d’intérêt (ex. taux de glucose, âge, score de risque prédite, à préciser selon le mémoire).
- Ajustement d’une loi **GEV** sur ces maxima pour modéliser la distribution des extrêmes.

**Estimation des paramètres :**
- Estimation des paramètres de la GEV :
  - Paramètre de **localisation**.
  - Paramètre d’**échelle**.
  - Paramètre de **forme** (qui contrôle l’épaisseur de la queue).
- Utilisation de méthodes numériques d’estimation (maximum de vraisemblance, etc.) via les fonctions des packages R (par ex. `extRemes`, `evd`).

**Quantiles extrêmes et niveaux de retour :**
- Calcul de **quantiles extrêmes** associés à de faibles probabilités d’occurrence (par exemple quantile à 0,99 ou 0,999).
- Analyse des **niveaux de retour (Return Levels)** : estimation de la valeur extrême attendue sur un horizon de retour N (par exemple 10 ans, 50 ans), pour interpréter la fréquence de survenue de conditions de risque très élevé.
- Visualisation des **courbes de niveaux de retour** (Return Level Plots) pour illustrer la relation entre période de retour et intensité de l’événement extrême, et mettre en évidence les niveaux de risque élevé.

#### 3.2 Modèle POT (Peaks Over Threshold)

**Sélection du seuil :**
- Choix d’un **seuil élevé** au-delà duquel les observations sont considérées comme extrêmes (par exemple via inspection graphique, mean residual life plots, ou critères de stabilité des paramètres).
- Sensibilité de l’analyse au choix du seuil discutée dans le rapport.

**Ajustement par la loi de Pareto généralisée (GPD) :**
- Modélisation des **dépassements au-dessus du seuil** avec une loi de **Pareto généralisée (GPD)**.
- Estimation des paramètres de la GPD pour caractériser la queue de distribution (échelle et forme).

**Analyse de la queue et niveaux de risque :**
- Étude de la **queue de distribution** afin de quantifier la probabilité d’observer des valeurs extrêmes (ex. très forts taux de glucose, valeurs de risque d’AVC élevées).
- Estimation de quantiles extrêmes et de **niveaux de retour** dans le cadre POT, pour des horizons de retour donnés.
- Interprétation de ces résultats en termes de **niveaux de risque élevé** (par exemple probabilité d’atteindre un certain niveau de risque dans un horizon N) et visualisation des graphiques associés (diagnostics GPD, return level plots).

*(Les détails techniques, les choix de seuils, les diagnostics de bonté d’ajustement et les interprétations fines sont présentés dans le rapport de mémoire.)*



### 4. Modèles de machine learning

- Rééchantillonnage des données avec **SMOTE** pour traiter le déséquilibre de la variable cible.
- Normalisation des variables numériques. 
- Séparation en **train** et **test** (par exemple 70 % / 30 %).  
- Entraînement d’un modèle (régression logistique ML, Arbre de décision, Random forest, SVM, Gradient Boosting,Réseau de neuron etc... ).  
- Évaluation des performances :
  - Matrice de confusion.
  - Taux de bon et mauvais classement.
  - AUC, courbe ROC, etc.

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
