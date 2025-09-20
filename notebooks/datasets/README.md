# ANIP Challenge – Visualisation de Données
ANIP Challenge – Tâche 1 : Collecte & Préparation des Données

Nom : Olivier FATOMBI
Date : 20/09/2025
Projet : Visualisation de données pour l’Agence Nationale d’Identification des Personnes (Bénin)


# 1- Objectif du projet

Cette Tâche 1 vise à collecter, nettoyer, harmoniser et consolider des données démographiques, économiques et sociales pour le Bénin.
Le but est de produire un dataset final prêt à l’analyse et documenté, afin de préparer des visualisations et dashboards interactifs.


# 2- Contenu du dépôt
Tache_1_Olivier_FATOMBI_Notebook_20092025/
│
├── tache1_collecte_preparation.ipynb      # Notebook Python complet
├── datasets/
│   └── final/
│       ├── benin_multi.csv               # Dataset final multi-source
│       ├── anomalies.csv                 # Lignes présentant des anomalies détectées
│       └── glossaire_variables.csv       # Dictionnaire des variables
└── README.md                             # Ce fichier


# 3- Sources de données

Démographiques et économiques : Banque Mondiale (World Bank API)

Sportives : Wikipédia – Jeux Olympiques (aucune donnée disponible fiable pour le Bénin, colonne nb_participants_olympiques vide)

Remarque : aucune anomalie majeure détectée, une seule ligne isolée dans anomalies.csv


# 4- Description des étapes

# 4.1 Collecte des données

Utilisation de l’API Banque Mondiale via pandas_datareader.wb

Téléchargement des indicateurs :

SP.POP.TOTL : Population totale

NY.GDP.MKTP.CD : PIB en USD courants

Période : 2000 à 2023

Pays : Bénin (BJ)

# 4.2 Nettoyage & harmonisation

Conversion de la colonne year en entier

Suppression des lignes vides

Calcul du PIB par habitant : gdp_per_capita = gdp_usd / population

Tri par année pour faciliter l’analyse

# 4.3 Détection des anomalies

Vérification des valeurs manquantes

Détection des valeurs négatives ou aberrantes

Une seule ligne identifiée et isolée dans anomalies.csv


# 5- Glossaire des variables
| Variable         | Nom complet       | Définition                    | Unité        | Source          | Période   | Géographie |
| ---------------- | ----------------- | ----------------------------- | ------------ | --------------- | --------- | ---------- |
| year             | Année             | Année de la mesure            | année        | Banque Mondiale | 2000-2023 | Bénin      |
| population       | Population totale | Nombre total d’habitants      | personnes    | Banque Mondiale | 2000-2023 | Bénin      |
| gdp\_usd         | PIB               | Produit Intérieur Brut en USD | USD          | Banque Mondiale | 2000-2023 | Bénin      |
| gdp\_per\_capita | PIB par habitant  | PIB / population              | USD/personne | Calculé         | 2000-2023 | Bénin      |


# 6- Notes complémentaires

Dataset final prêt à l’analyse pour la Tâche 2 (exploration et visualisation).

Documentation complète des variables et anomalies.

Tous les fichiers sont disponibles sur le dépôt GitHub ou peuvent être inclus dans un zip pour soumission.
