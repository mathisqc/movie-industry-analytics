# Movie Industry Analytics

Projet personnel d'analyse de données visant à étudier les principaux facteurs associés à la performance commerciale des films.

**Outils :** Dataiku | Power BI | DAX | Data Quality | Data Visualization

---

## 1. Présentation du projet

L'objectif de ce projet est d'analyser les données de l'industrie cinématographique afin d'identifier les principaux facteurs associés à la performance commerciale des films.

L'analyse cherche principalement à répondre à la problématique suivante :

> **Quels facteurs sont associés à la performance commerciale des films, et quelles caractéristiques distinguent les plus grands succès au box-office ?**

Le projet couvre l'ensemble du processus d'analyse, depuis la préparation et la fiabilisation des données dans Dataiku jusqu'à leur analyse et leur visualisation dans Power BI.

L'objectif est d'identifier des associations présentes dans les données et non d'établir des relations de causalité.

---

## 2. Jeu de données

Le projet utilise le jeu de données public **Movie Industry**, disponible sur Kaggle.

Le dataset initial contient **7 668 films et 15 variables**, couvrant la période de **1980 à 2020**.

Il contient notamment des informations sur :

- le titre et le genre du film ;
- l'année et la date de sortie ;
- le budget et les recettes au box-office ;
- le score et le nombre de votes ;
- le réalisateur, l'acteur principal et la société de production ;
- le pays et la durée du film.

Le jeu de données contient plusieurs valeurs manquantes ainsi que des variables nécessitant une préparation avant de pouvoir être utilisées pour l'analyse.

---

## 3. Préparation des données avec Dataiku

La préparation et les contrôles de qualité des données ont été réalisés avec **Dataiku**.

L'objectif était de transformer les données brutes en un dataset propre et structuré, prêt à être exploité dans Power BI.

Les principales étapes de préparation ont été :

- analyse des valeurs manquantes ;
- recherche de doublons ;
- vérification et conversion des types de données ;
- extraction de la date, du pays et du mois de sortie ;
- création d'un indicateur de **profit** à partir des recettes et du budget ;
- calcul du **retour sur investissement (ROI)** ;
- création de catégories de rentabilité ;
- contrôles de cohérence et de qualité des données.

Les budgets manquants n'ont pas été artificiellement remplacés afin de ne pas introduire d'hypothèses supplémentaires dans l'analyse financière.

### Flow Dataiku

Le Flow final permet de visualiser les différentes étapes de préparation, de transformation et d'analyse des données.

![Flow Dataiku](images/dataiku-flow.png)

### Préparation des données

La recette Prepare a permis de nettoyer, transformer et enrichir le dataset initial avant son export vers Power BI.

![Préparation Dataiku](images/dataiku-preparation.png)

---

## 4. Analyse et visualisation avec Power BI

Le dataset nettoyé dans Dataiku a ensuite été exporté et analysé dans **Power BI**.

Plusieurs mesures et colonnes calculées en DAX ont été créées afin d'analyser notamment :

- les recettes au box-office ;
- le budget ;
- le profit ;
- le ROI ;
- la proportion de films rentables ;
- le score moyen ;
- les corrélations entre la performance commerciale et différentes caractéristiques des films.

Les médianes ont principalement été utilisées pour les indicateurs financiers afin de limiter l'influence des valeurs extrêmes présentes dans les distributions.

Le dashboard est organisé en trois pages complémentaires.

### Page 1 — Vue d'ensemble et tendances

La première page présente une vue générale du marché et de son évolution entre **1980 et 2019**.

Elle comprend notamment :

- les principaux indicateurs de performance ;
- l'évolution du budget et des recettes médianes ;
- une comparaison du budget et des recettes selon le genre ;
- des filtres par année et par genre.

L'année 2020 a été exclue de l'analyse temporelle car le dataset ne contient qu'un nombre limité de films pour cette année.

![Power BI Overview](images/powerbi-overview.png)

### Page 2 — Facteurs associés au succès

La deuxième page analyse les différents facteurs associés aux recettes au box-office.

Des nuages de points et des corrélations de Pearson ont été utilisés afin d'étudier les relations entre les recettes et :

- le budget ;
- le nombre de votes ;
- le score des spectateurs ;
- la durée du film.

Des analyses complémentaires permettent également de comparer les recettes selon les sociétés de production et les classifications des films.

![Power BI Success Drivers](images/powerbi-success-drivers.png)

### Page 3 — Rentabilité et analyse du marché

La troisième page se concentre sur la rentabilité des films et certaines caractéristiques du marché.

Elle comprend notamment :

- le profit médian et le ROI médian ;
- la proportion de films rentables ;
- les films générant les profits les plus élevés ;
- les films présentant les ROI les plus élevés ;
- la rentabilité selon le genre ;
- les performances selon le mois de sortie ;
- l'évolution du budget et du profit selon le mois de sortie ;
- des comparaisons de budget et de ROI entre différents pays.

Des seuils minimums de nombre de films ont été appliqués pour certaines analyses par genre et par pays afin d'éviter de tirer des conclusions à partir d'échantillons trop faibles.

![Power BI Profitability](images/powerbi-profitability.png)

---

## 5. Principaux résultats

Plusieurs résultats ressortent de l'analyse :

- Le **budget et les recettes présentent une forte association positive (r = 0,74)**.
- Le **nombre de votes et les recettes sont également positivement associés (r = 0,63)**.
- Le score des spectateurs présente une association beaucoup plus faible avec les recettes (**r = 0,19**).
- La durée du film présente également une association faible avec les recettes (**r = 0,25**).
- Environ **67,8 % des films** disposant des données financières nécessaires sont rentables.
- Les genres Animation et Horreur présentent des ROI médians élevés au sein de l'échantillon analysé.
- Juin et décembre ressortent comme des périodes particulièrement fortes en termes de recettes médianes.

Ces résultats représentent les tendances observées dans le dataset et ne doivent pas être interprétés comme des relations de causalité.

---

## 6. Limites de l'analyse

Cette analyse présente plusieurs limites :

- le dataset ne représente pas de manière exhaustive tous les films sortis entre 1980 et 2020 ;
- les données disponibles pour 2020 sont incomplètes ;
- les informations de budget sont manquantes pour environ **28 % des films** ;
- les montants financiers sont exprimés en dollars nominaux et ne sont pas corrigés de l'inflation ;
- le nombre de films varie fortement selon les pays, les genres et les sociétés de production ;
- le nombre de votes peut refléter la popularité et la visibilité d'un film autant que l'engagement des spectateurs ;
- une corrélation ne démontre pas une relation de causalité.

---

## 7. Outils et compétences

### Outils

- **Dataiku** — préparation, transformation et contrôle de la qualité des données
- **Power BI** — analyse et visualisation des données
- **DAX** — création de mesures, colonnes calculées et indicateurs

### Compétences mises en œuvre

- Préparation des données
- Nettoyage et transformation
- Data Quality
- Analyse exploratoire
- Création de KPI
- Analyse de corrélations
- DAX
- Data Visualization
- Interprétation des résultats

---

## Workflow du projet

**Données brutes → Dataiku → Data Quality & Transformation → Dataset nettoyé → Power BI → Analyse & Insights**
