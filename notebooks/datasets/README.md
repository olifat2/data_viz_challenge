# ANIP Challenge – Visualisation de Données

# Nom : Olivier FATOMBI
# Date : 20/09/2025
# Projet : Visualisation de données pour l’Agence Nationale d’Identification des Personnes (Bénin)

# Tâche 1 : Collecte & Préparation des Données

# 1. Objectif du projet

La Tâche 1 vise à collecter, nettoyer, harmoniser et consolider des données démographiques, économiques, sociales et sanitaires pour le Bénin.
L’objectif est de produire un dataset final prêt à l’analyse, documenté, pour permettre la création de visualisations et dashboards interactifs.

# 2. Contenu du dépôt

Tache_1_Olivier_FATOMBI_Notebook_20092025/
│
├── tache1_collecte_preparation.ipynb      # Notebook Python complet
├── datasets/
│   └── final/
│       ├── benin_multi.csv               # Dataset final multi-source initial
│       ├── benin_multi_enriched.csv      # Dataset enrichi avec WDI
│       ├── benin_multi_enriched_apis.csv # Dataset enrichi avec WHO
│       ├── anomalies.csv                 # Lignes présentant des anomalies détectées
│       └── glossaire_variables.csv       # Dictionnaire des variables
└── README.md                             # Ce fichier

# 3. Sources de données

| Type                         | Source                            | Remarques                                                                      |
| ---------------------------- | --------------------------------- | ------------------------------------------------------------------------------ |
| Démographiques & Économiques | Banque Mondiale (World Bank API)  | Période 2000–2023, Pays : Bénin(BJ)                                           |
| Sociaux & Éducatifs          | Banque Mondiale (WDI)             | Nouveaux indicateurs : scolarisation primaire, alphabétisation adulte          |
| Sanitaires                   | WHO Global Health Observatory API | Nouveaux indicateurs : espérance de vie, mortalité <5 ans                      |
| Sportives                    | Wikipédia – Jeux Olympiques       | Colonne `nb_participants_olympiques` vide (aucune donnée
iable pour le Bénin) |

# 4. Description des étapes
# 4.1 Collecte des données

API Banque Mondiale via pandas_datareader.wb pour les indicateurs principaux :

SP.POP.TOTL : Population totale

SP.URB.TOTL : Population urbaine

NY.GDP.MKTP.CD : PIB en USD courants

FP.CPI.TOTL : Inflation

SL.UEM.TOTL.ZS : Taux de chômage

NE.EXP.GNFS.CD : Exportations

SP.DYN.LE00.IN : Espérance de vie (WDI initial)

SE.ADT.LITR.ZS : Alphabétisation adulte (WDI initial)

SE.PRM.ENRR : Scolarisation primaire (WDI initial)

Scraping Wikipédia pour les participations aux JO (nb_participants_olympiques)

Téléchargement API WHO pour les indicateurs sanitaires :

life_expectancy : Espérance de vie à la naissance

under5_mortality_per1000 : Taux de mortalité des moins de 5 ans

# 4.2 Nettoyage & harmonisation

Conversion de la colonne year en entier

Suppression des lignes vides ou aberrantes

Calcul du PIB par habitant : gdp_per_capita = gdp_usd / population

Tri par année pour faciliter l’analyse

Fusion multi-source : WDI + WHO + données sportives

# 4.3 Indicateurs dérivés

Croissance annuelle de la population : pop_growth_pct

Croissance annuelle du PIB : gdp_growth_pct

# 4.4 Détection des anomalies

Vérification des valeurs manquantes et aberrantes

Détection des valeurs négatives pour : population, gdp_usd, gdp_per_capita

Vérification des bornes réalistes pour : adult_literacy_pct (<150%) et under5_mortality_per1000 (≥0)

Les lignes problématiques sont isolées dans anomalies.csv

# 5. Glossaire des variables

| Variable                     | Nom complet                        | Définition                                          | Unité        | Source           | Période   | Géographie |
| ---------------------------- | ---------------------------------- | --------------------------------------------------- | ------------ | ---------------- | --------- | ---------- |
| year                         | Année                              | Année de la mesure                                  | année        | Banque Mondiale  | 2000-2023 | Bénin      |
| population                   | Population totale                  | Nombre total d’habitants                            | personnes    | Banque Mondiale  | 2000-2023 | Bénin      |
| population\_urbaine          | Population urbaine                 | Nombre d’habitants en milieu urbain                 | personnes    | Banque Mondiale  | 2000-2023 | Bénin      |
| gdp\_usd                     | PIB                                | Produit Intérieur Brut en USD courants              | USD          | Banque Mondiale  | 2000-2023 | Bénin      |
| gdp\_per\_capita             | PIB par habitant                   | PIB / population                                    | USD/personne | Calculé          | 2000-2023 | Bénin      |
| inflation                    | Inflation                          | Variation annuelle des prix à la consommation       | %            | Banque Mondiale  | 2000-2023 | Bénin      |
| taux\_chomage                | Taux de chômage                    | Proportion de la population active au chômage       | %            | Banque Mondiale  | 2000-2023 | Bénin      |
| exportations                 | Exportations                       | Valeur totale des exportations de biens et services | USD          | Banque Mondiale  | 2000-2023 | Bénin      |
| nb\_participants\_olympiques | Participants aux JO                | Nombre de participants béninois aux Jeux Olympiques | personnes    | Wikipédia        | 2000-2023 | Bénin      |
| primary\_enrolment\_gross    | Scolarisation primaire (taux brut) | Gross enrolment ratio - primaire                    | %            | World Bank (WDI) | 2000-2023 | Bénin      |
| adult\_literacy\_pct         | Taux d'alphabétisation adulte      | % d'adultes (15+) sachant lire et écrire            | %            | World Bank (WDI) | 2000-2023 | Bénin      |
| life\_expectancy             | Espérance de vie à la naissance    | Espérance de vie totale (années)                    | années       | WHO              | 2000-2023 | Bénin      |
| under5\_mortality\_per1000   | Mortalité <5 ans                   | Taux de mortalité des moins de 5 ans (pour 1000)    | pour 1000    | WHO              | 2000-2023 | Bénin      |

# 6. Notes complémentaires

Dataset final prêt pour la Tâche 2 : exploration et visualisation

Documentation complète des variables et anomalies

Fichiers disponibles sur le dépôt GitHub


# Tâche 2 : Exploration & Analyse

# 1. Objectifs

Cette tâche vise à transformer le dataset consolidé de la Tâche 1 en un support d’analyse riche et prêt pour un usage décisionnel (Power BI, Tableau, etc.).
    Les objectifs principaux sont :

    Explorer et comprendre les tendances démographiques, économiques, sociales et sanitaires.

    Détecter les anomalies et incohérences dans les données.

    Créer des indicateurs dérivés et avancés pour enrichir l’analyse.

    Préparer les données pour un usage interactif et décisionnel.

# 2. Missions
# 2.1 Exploration des données

Analyse descriptive :

    Tendances historiques : population, PIB, scolarisation primaire, alphabétisation adulte, espérance de vie, mortalité infantile.

    Dynamiques spatiales : variations entre régions simulées.

Statistiques principales : moyenne, médiane, min/max, écart-type, distribution.

Visualisations préliminaires : courbes temporelles, histogrammes, boxplots, matrices de corrélation.

# 2.2 Détection et documentation des anomalies

Identification des valeurs aberrantes ou incohérentes pour chaque indicateur.

Documentation des choix de traitement (suppression, interpolation, ou conservation selon le contexte).

Fichier généré : anomalies_2.csv pour les anomalies nationales, anomalies_region_2.csv pour les anomalies régionales.

Résultats :

Anomalies nationales détectées et sauvegardées : datasets/final/anomalies_2.csv

Anomalies régionales sauvegardées : datasets/final/anomalies_region_2.csv

# 2.3 Création de nouvelles variables et indicateurs

Indicateurs de croissance et ratios :

    Croissance annuelle de la population : pop_growth_pct

    Croissance annuelle du PIB : gdp_growth_pct

    Ratio scolarisation / alphabétisation : school_to_literacy_ratio

Indices composites :

    Indicateur de santé : health_index = esperance_vie / 1

Agrégations temporelles et spatiales :

    Moyennes mobiles ou glissantes pour lisser les tendances.

    Agrégations par région simulée, normalisation par habitant.

# 2.4 Corrélations croisées

Détection des relations entre variables clés :

    PIB vs espérance de vie

    Scolarisation primaire vs alphabétisation adulte

    Mortalité <5 ans vs indicateurs économiques

Visualisation via matrices de corrélation et scatter plots.

# 3. Livrables

Dataset enrichi : benin_multi_dashboard.csv
    Contient toutes les variables de la Tâche 1, plus les indicateurs dérivés et régionaux simulés.

Aperçu des statistiques descriptives nationales :

| Variable                     | count | mean       | std       | min       | 25%       | 50%        | 75%        | max        |
| ---------------------------- | ----- | ---------- | --------- | --------- | --------- | ---------- | ---------- | ---------- |
| population                   | 24    | 10,409,007 | 2,140,555 | 7,221,619 | 8,626,468 | 10,245,640 | 12,125,672 | 14,111,034 |
| population\_urbaine          | 24    | 4,650,441  | 1,334,089 | 2,768,263 | 3,530,420 | 4,494,797  | 5,687,776  | 7,069,628  |
| taux\_croissance\_pop        | 24    | 2.92       | 0.18      | 2.52      | 2.86      | 2.96       | 3.04       | 3.22       |
| gdp\_usd                     | 24    | 1.068e10   | 4.54e9    | 3.52e9    | 6.92e9    | 1.092e10   | 1.353e10   | 1.967e10   |
| esperance\_vie               | 24    | 58.61      | 1.19      | 56.59     | 57.91     | 58.51      | 59.55      | 60.77      |
| alphabetisation              | 6     | 37.74      | 6.90      | 28.70     | 33.46     | 36.94      | 42.59      | 47.10      |
| scolarisation\_primaire      | 22    | 110.18     | 13.41     | 80.11     | 98.53     | 112.54     | 121.01     | 127.12     |
| gdp\_per\_capita             | 24    | 981.42     | 252.72    | 487.42    | 801.72    | 1039.54    | 1156.04    | 1394.18    |
| nb\_participants\_olympiques | 24    | 0.0        | 0.0       | 0.0       | 0.0       | 0.0        | 0.0        | 0.0        |
| pop\_growth\_pct             | 23    | 2.96       | 0.19      | 2.55      | 2.89      | 3.00       | 3.08       | 3.27       |
| gdp\_growth\_pct             | 23    | 8.11       | 8.67      | -14.28    | 3.98      | 7.45       | 12.83      | 27.54      |
| school\_to\_literacy\_ratio  | 6     | 2.97       | 0.54      | 2.40      | 2.56      | 2.89       | 3.34       | 3.74       |
| health\_index                | 24    | 58.61      | 1.19      | 56.59     | 57.91     | 58.51      | 59.55      | 60.77      |

Notebook ou rapport intermédiaire : analyse exploratoire complète avec visualisations et méthodes détaillées.

Liste des anomalies : anomalies_2.csv et anomalies_region_2.csv.