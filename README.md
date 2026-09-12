# Movie Industry Analytics — Dataiku & Power BI

Projet personnel d'analyse de données sur l'industrie cinématographique, de la préparation des données jusqu'à leur analyse et leur visualisation.

**Outils :** Dataiku | Power BI | DAX  
**Méthodes :** Data Cleaning | Data Quality | KPI | Médianes | Corrélation de Pearson | Data Visualization

---

## 1. Présentation du projet

Le projet repose sur l'analyse de données concernant 7 668 films sortis entre 1980 et 2020.

L'objectif principal est d'étudier les facteurs associés à la performance commerciale des films et les caractéristiques des plus grands succès au box-office.

Plusieurs questions ont guidé l'analyse :

- Quels genres génèrent les recettes les plus importantes ?
- Les films avec les budgets les plus élevés génèrent-ils également davantage de recettes ?
- Les notes des spectateurs sont-elles associées aux performances commerciales ?
- Le nombre de votes est-il associé aux recettes ?
- La durée d'un film est-elle associée aux recettes ?
- Quels studios présentent les meilleures performances ?
- Quels films génèrent les profits les plus élevés ?
- Quels films présentent les meilleurs ROI ?
- Quels genres sont les plus rentables ?
- La période de sortie est-elle associée aux performances ?
- Comment les budgets et les recettes ont-ils évolué au fil des années ?
- Observe-t-on des différences de budget et de rentabilité selon les pays ?

Le succès d'un film dépend évidemment de nombreux autres éléments.

Le marketing, la distribution, les franchises, la notoriété des acteurs ou encore la popularité d'une licence peuvent par exemple avoir un impact important.

Ces informations ne sont pas disponibles dans le dataset.

L'analyse se concentre donc uniquement sur les facteurs pouvant être étudiés avec les données disponibles.

---

## 2. Jeu de données

Le projet utilise le dataset public **Movie Industry**, disponible sur Kaggle.

Le dataset initial contient :

- **7 668 films**
- **15 variables**
- Une période allant de **1980 à 2020**

Les données disponibles concernent notamment :

- Le titre
- Le genre
- L'année et la date de sortie
- Le budget
- Les recettes au box-office
- Le score des spectateurs
- Le nombre de votes
- Le réalisateur
- Le scénariste
- L'acteur principal
- La société de production
- Le pays
- La durée

Les données brutes nécessitent plusieurs contrôles et transformations avant leur analyse.

---

## 3. Préparation des données avec Dataiku

La préparation et la fiabilisation des données sont réalisées avec **Dataiku**.

L'objectif est d'obtenir un dataset propre et structuré avant son utilisation dans Power BI.

### 3.1 Contrôle de la qualité des données

Plusieurs contrôles sont réalisés :

- Analyse des valeurs manquantes
- Recherche de doublons
- Vérification des types
- Contrôles de cohérence
- Analyse des variables financières

Aucun doublon n'est identifié avec la combinaison **titre + année + réalisateur**.

Le budget représente la principale variable financière incomplète.

Environ **28 % des films ne disposent pas d'un budget renseigné**.

Ces valeurs ne sont pas remplacées artificiellement.

Cela évite d'introduire des estimations dans les calculs de profit et de ROI.

### 3.2 Transformation des données

Plusieurs transformations sont ensuite réalisées.

La variable `votes` est convertie en entier puisqu'elle représente un nombre de votants.

La colonne originale `released` contient plusieurs informations dans une seule variable.

Elle est donc traitée afin de créer :

- `released_date`
- `released_country`
- `release_month`

La variable `release_month` permet notamment d'étudier l'existence d'une saisonnalité dans les performances commerciales.

De nouveaux indicateurs financiers sont également créés.

**Profit :**

`Profit = Recettes - Budget`

**ROI :**

`ROI = Profit / Budget`

Le profit permet de mesurer le gain financier absolu.

Le ROI permet de comparer ce gain au budget initial du film.

Des catégories de rentabilité sont également créées.

### 3.3 Flow Dataiku

Le Flow final regroupe les différentes étapes de préparation, de contrôle et d'analyse réalisées dans Dataiku.

![Flow Dataiku](images/dataiku-flow.png)

### 3.4 Recette de préparation

La recette Prepare contient les principales opérations de nettoyage, de transformation et de création de nouvelles variables.

![Préparation Dataiku](images/dataiku-preparation.png)

Après préparation, le dataset final contient **7 668 lignes et 21 variables**.

Il est ensuite exporté vers Power BI.

---

## 4. Analyse et visualisation avec Power BI

Le dataset préparé dans Dataiku est importé dans **Power BI**.

Plusieurs mesures et colonnes calculées en DAX sont créées :

- Nombre de films
- Recettes médianes
- Budget médian
- Profit médian
- ROI médian
- Pourcentage de films rentables
- Score moyen
- Indicateurs de corrélation

Les médianes sont principalement utilisées pour les variables financières.

Les budgets, recettes, profits et ROI présentent des valeurs extrêmes importantes.

La médiane permet de limiter l'influence de ces valeurs sur les résultats.

Le dashboard est organisé en trois pages.

### 4.1 Vue d'ensemble et tendances

La première page donne une vue générale du marché du cinéma sur la période **1980-2019**.

Elle présente notamment :

- Les principaux KPI
- L'évolution des recettes médianes
- L'évolution des budgets médians
- Les différences de budget et de recettes selon les genres
- Des filtres par année et par genre

![Vue d'ensemble Power BI](images/powerbi-overview.png)

Les budgets et les recettes médianes augmentent globalement au cours de la période étudiée.

Des différences importantes apparaissent également selon les genres.

L'année **2020 est exclue de l'analyse temporelle**.

Le dataset ne contient qu'un faible nombre de films pour cette année et l'échantillon n'est pas comparable aux années précédentes.

Les montants ne sont pas corrigés de l'inflation.

L'évolution financière sur plusieurs décennies doit donc être interprétée avec prudence.

---

### 4.2 Facteurs associés au succès commercial

La deuxième page cherche à identifier les variables associées aux recettes au box-office.

Quatre relations sont étudiées :

- Budget / Recettes
- Nombre de votes / Recettes
- Score / Recettes
- Durée / Recettes

Des nuages de points et des droites de tendance permettent de visualiser ces relations.

Le **coefficient de corrélation de Pearson** est utilisé pour mesurer la force de la relation linéaire entre chaque variable et les recettes.

Les résultats obtenus sont :

| Relation | Corrélation |
|---|---:|
| Budget / Box-office | **0,74** |
| Votes / Box-office | **0,63** |
| Durée / Box-office | **0,25** |
| Score / Box-office | **0,19** |

![Facteurs de succès Power BI](images/powerbi-success-drivers.png)

Le **budget présente la relation la plus forte avec les recettes (r = 0,74)**.

Dans le dataset, les films disposant de budgets plus importants ont tendance à générer davantage de recettes.

Le **nombre de votes présente également une association importante (r = 0,63)**.

Ce résultat doit cependant être interprété avec prudence.

Le nombre de votes peut lui-même augmenter avec la visibilité et la popularité d'un film.

Le **score présente une association faible avec les recettes (r = 0,19)**.

Une excellente note ne garantit donc pas un important succès commercial.

La **durée présente également une association faible (r = 0,25)**.

Des analyses complémentaires comparent également les recettes médianes selon les sociétés de production et les classifications des films.

---

### 4.3 Rentabilité et analyse du marché

La troisième page s'intéresse à la **rentabilité** et non uniquement aux recettes.

![Rentabilité Power BI](images/powerbi-profitability.png)

Les principaux indicateurs sont :

- **Profit médian : 13,77 M$**
- **ROI médian : 80,72 %**
- **Films rentables : 67,77 %**

Environ deux tiers des films disposant des informations financières nécessaires présentent donc un profit positif dans le dataset.

Le profit et le ROI permettent d'étudier deux aspects différents de la performance.

Le **profit** mesure le gain financier en valeur absolue.

Le **ROI** mesure ce gain par rapport au budget initial.

Un blockbuster peut donc générer un profit très important sans obtenir le meilleur ROI.

À l'inverse, un film avec un petit budget peut obtenir un ROI très élevé avec un profit absolu plus faible.

Plusieurs analyses complémentaires sont réalisées :

- Classement des films selon le profit
- Classement des films selon le ROI
- Profit médian par genre
- ROI médian par genre
- Recettes médianes selon le mois de sortie
- Budget et profit médians selon le mois de sortie
- Budget médian selon le pays
- ROI médian selon le pays

Des seuils minimums de nombre de films sont appliqués pour certaines comparaisons.

Cela permet d'éviter qu'une catégorie contenant seulement quelques films domine artificiellement les résultats.

L'**Animation** présente notamment un profit médian élevé dans l'échantillon étudié.

L'**Animation et l'Horreur** présentent également des ROI médians élevés.

Les mois de **juin et décembre** ressortent avec des recettes médianes particulièrement importantes.

Les comparaisons entre pays doivent être interprétées avec prudence car les tailles des échantillons sont très différentes.

---

## 5. Principaux résultats

Les principaux résultats obtenus sont :

- Le **budget** présente la plus forte association avec les recettes (**r = 0,74**).
- Le **nombre de votes** est également associé aux recettes (**r = 0,63**).
- Le **score** présente une association beaucoup plus faible (**r = 0,19**).
- La **durée** présente également une association faible (**r = 0,25**).
- Environ **67,8 % des films** disposant des données financières nécessaires sont rentables.
- Le profit et le ROI mettent en évidence deux formes différentes de performance financière.
- L'Animation et l'Horreur présentent de bons indicateurs de rentabilité dans l'échantillon étudié.
- Juin et décembre présentent des recettes médianes particulièrement élevées.

Aucune variable ne permet à elle seule d'expliquer la réussite commerciale d'un film.

Parmi les variables numériques étudiées, le budget présente l'association la plus importante avec les recettes.

D'autres éléments comme le marketing, la puissance d'une franchise, la distribution ou la notoriété des acteurs peuvent également intervenir.

Ces variables ne sont pas présentes dans le dataset et ne sont donc pas mesurées dans cette analyse.

---

## 6. Limites de l'analyse

- Le dataset ne contient pas l'ensemble des films sortis entre 1980 et 2020.
- Les données de 2020 sont incomplètes.
- Environ **28 % des budgets sont manquants**.
- Les montants financiers ne sont pas corrigés de l'inflation.
- Les tailles d'échantillon varient fortement selon les genres, pays et sociétés de production.
- Le nombre de votes peut être lié à la visibilité du film autant qu'à l'engagement des spectateurs.
- Les dépenses marketing ne sont pas disponibles.
- L'ampleur de la distribution n'est pas disponible.
- L'appartenance à une franchise n'est pas directement renseignée.
- Une corrélation indique une association et non une relation de causalité.

---

## 7. Outils et compétences

**Outils**

- Dataiku
- Power BI
- DAX

**Préparation des données**

- Data Cleaning
- Data Quality
- Analyse des valeurs manquantes
- Recherche de doublons
- Transformation des données
- Création de nouvelles variables

**Analyse des données**

- Analyse exploratoire
- KPI
- Analyse par médiane
- Analyse de rentabilité
- Corrélation de Pearson
- Analyse temporelle
- Segmentation
- Data Visualization

---

## 8. Workflow du projet

**Données brutes → Data Quality → Préparation Dataiku → Création de variables → Dataset nettoyé → Power BI → DAX et analyses statistiques → Dashboard → Résultats**
