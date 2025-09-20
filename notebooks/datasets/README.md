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