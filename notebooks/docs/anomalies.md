# Anomalies détectées – Tâche 1 (Exploration & Analyse)

## 1. Valeurs manquantes

- `alphabetisation` : 18 valeurs manquantes (probablement certaines années ou certaines désagrégations non publiées).  
  - Décision : conserver comme NA et documenter la limite de la source.  

- `adult_literacy_pct` : 18 valeurs manquantes.  
  - Décision : conserver comme NA, possibilité d’estimer par interpolation ou complétion avec une autre source (UNESCO, PNUD).  

- `scolarisation_primaire` : 2 valeurs manquantes.  
  - Décision : interpolation linéaire sur les années adjacentes.  

- `primary_enrolment_gross` : 2 valeurs manquantes.  
  - Décision : interpolation ou suppression si non critique pour les analyses.  

- `nb_participants_olympiques` : 24 valeurs manquantes.  
  - Décision : cohérent car le Bénin n’a pas participé à toutes les éditions → garder les NA comme information valide.  

- `pop_growth_pct` : 1 valeur manquante.  
  - Décision : recalcul possible à partir des années adjacentes (`population`).  

- `gdp_growth_pct` : 1 valeur manquante.  
  - Décision : recalcul possible à partir du PIB des années adjacentes.  

---

## 2. Valeurs incohérentes ou suspectes (extrait de `anomalies_2.csv`)

- **Colonnes vides dans le fichier anomalies** → cela signifie que aucune valeur négative ou aberrante n'a été détectée
  - Décision : continuer à surveiller mais pas d’action corrective nécessaire pour l’instant.  

---

## 3. Autres remarques

- Les **taux (%)** doivent logiquement être entre 0 et 100. Toute valeur >100 (ex. alphabétisation >100%) doit être marquée comme anomalie.  
- Les **espérances de vie** doivent être comprises entre 30 et 90 ans. Toute valeur hors plage est une anomalie.  
- Les **mortalités infantiles** (`under5_mortality_per1000`) doivent être >0 et en général <200.  

---

## 4. Décisions méthodologiques générales

- Interpolation linéaire pour petites séries temporelles (≤2 valeurs manquantes).  
- Conservation en NA pour grandes séries manquantes (alphabétisation, chômage) → car trop incertain à estimer.  
- Documentation systématique dans le glossaire.  
