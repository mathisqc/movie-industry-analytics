# Movie Industry Analytics — Dataiku & Power BI

Personal data analysis project on the movie industry, from data preparation to analysis and visualization.

**Tools:** Dataiku | Power BI | DAX  
**Methods:** Data Cleaning | Data Quality | KPI | Medians | Top 10 | Pearson Correlation | Data Visualization

---

## 1. Project Overview

This project focuses on the analysis of data from 7,668 movies released between 1980 and 2020 from North America, Europe and East Asia.

The main objective is to study the factors associated with the commercial performance of movies and the characteristics of the biggest box-office successes.

Several questions guided my analysis:

- Which genres generate the highest box-office revenue?
- Do movies with higher budgets also generate more revenue?
- Are audience scores associated with commercial performance?
- Is the number of votes associated with box-office revenue?
- Is movie runtime associated with box-office revenue?
- Which production companies show the best performance?
- Which movies generate the highest profits?
- Which movies have the highest ROI?
- Which genres are the most profitable?
- Is the release period associated with commercial performance?
- How have budgets and box-office revenue changed over the years?
- Are there differences in budget and profitability between countries?

The success of a movie obviously depends on many other factors.

Marketing, distribution, franchises, actor popularity or the popularity of a license can for example have an important impact.

However, this information is not available in the dataset.

My analysis therefore focuses only on the factors that can be studied with the available data.

---

## 2. Dataset

For this project, I used the public **Movie Industry** dataset available on Kaggle.

The original dataset contains:

- **7,668 movies**
- **15 variables**
- A period from **1980 to 2020**

The available data includes:

- Title
- Genre
- Year and release date
- Budget
- Box-office revenue
- Audience score
- Number of votes
- Director
- Writer
- Main actor
- Production company
- Country
- Runtime

The raw data requires several checks and transformations before analysis.

---

## 3. Data Preparation with Dataiku

I prepared and cleaned the data using **Dataiku**.

The objective is to obtain a clean and structured dataset before using it in Power BI.

### 3.1 Data Quality Checks

I performed several checks to verify the quality of my data, such as:

- Missing value analysis
- Duplicate detection
- Data type verification
- Consistency checks
- Analysis of financial variables

No duplicates were identified based on the combination **title + year + director**, which I checked in Dataiku.

Based on the analysis of the different variables in the dataset, budget is the main incomplete financial variable.

Around **28% of the movies do not have a budget value**.

With so many missing values, I decided not to replace them artificially because this could introduce inaccurate estimates into the profit and ROI calculations. With this amount of missing data, these analyses could become misleading.

### 3.2 Data Transformation

I then performed several transformations.

The `votes` variable was converted to an integer because it represents a number of voters.

The original `released` column contains several pieces of information in a single variable.

I therefore processed it to create:

- `released_date`
- `released_country`
- `release_month`

The `release_month` variable allows me to study possible seasonality in commercial performance.

I also created new financial indicators.

**Profit:**

`Profit = Revenue - Budget`

**ROI:**

`ROI = Profit / Budget`

Profit measures the financial gain in absolute value.

ROI compares this gain with the initial budget of the movie.

I also created profitability categories.

### 3.3 Dataiku Flow

The final Flow contains the different preparation, control and analysis steps performed in Dataiku.

![Dataiku Flow](images/dataiku-flow.png)

### 3.4 Preparation Recipe

The Prepare recipe contains the main cleaning, transformation and new variable creation operations.

![Dataiku Preparation](images/dataiku-preparation.png)

After preparation, the final dataset contains **7,668 rows and 21 variables**.

I then exported it to Power BI.

---

## 4. Analysis and Visualization with Power BI

The next step was to import the dataset I had prepared in Dataiku into Power BI.

I then created several measures and columns in DAX, such as:

- Number of movies
- Median box-office revenue
- Median budget
- Median profit
- Median ROI
- Percentage of profitable movies
- Average score
- Correlation indicators, such as the correlation between a movie's budget and its box-office revenue

I mainly used medians for financial variables.

Budgets, box-office revenue, profits and ROI contain important extreme values.

The median helps limit the influence of these values on the results.

My dashboard is organized into three pages: an overview, an analysis of the factors associated with commercial success, and finally a market analysis.

### 4.1 Overview and Trends

The first page gives a general overview of the movie market over the **1980-2019** period.

It includes:

- Main KPIs
- Evolution of median box-office revenue
- Evolution of median budgets
- Differences in budget and revenue between genres
- Filters by year and genre

![Power BI Overview](images/powerbi-overview.png)

Median budgets and box-office revenue generally increase over the period studied.

Important differences also appear between genres.

I quickly noticed that the year 2020 was incomplete and contained much less data, with only a small number of movies. This can of course be explained by the COVID crisis, which strongly affected the movie industry. The year **2020 is therefore excluded from the time analysis**.

The dataset contains only a small number of movies for this year and the sample is not comparable with previous years.

Financial amounts are not adjusted for inflation.

Financial trends over several decades should therefore be interpreted with caution.

---

### 4.2 Factors Associated with Commercial Success

The second page aims to identify variables associated with box-office revenue.

Four relationships are studied:

- Budget / Revenue
- Number of votes / Revenue
- Score / Revenue
- Runtime / Revenue

Scatter plots and trend lines are used to visualize these relationships.

The **Pearson correlation coefficient** is used to measure the strength of the linear relationship between each variable and box-office revenue.

The results are:

| Relationship | Correlation |
|---|---:|
| Budget / Box-office | **0.74** |
| Votes / Box-office | **0.63** |
| Runtime / Box-office | **0.25** |
| Score / Box-office | **0.19** |

![Power BI Success Factors](images/powerbi-success-drivers.png)

**Budget shows the strongest relationship with box-office revenue (r = 0.74)**.

I can therefore conclude that movies with higher budgets tend to generate more revenue.

The **number of votes also shows an important association (r = 0.63)**.

Here, I also observe a relationship between the number of votes and the success of a movie. Movies with more votes tend to be more popular. However, this result should be interpreted with caution because the number of votes can itself increase because of the visibility and popularity of a movie.

The **score shows a weak association with box-office revenue (r = 0.19)**.

This result shows me that a movie with an excellent score is not always guaranteed to have major commercial success.

**Runtime also shows a weak association (r = 0.25)**.

Based on this result, the runtime of a movie does not seem to be directly related to its commercial success. For example, animated movies often have relatively short runtimes compared with other movies and can still achieve major commercial success.

Additional analyses also compare median box-office revenue between production companies and movie ratings.

---

### 4.3 Profitability and Market Analysis

The third page focuses on **profitability** and not only on box-office revenue.

![Power BI Profitability](images/powerbi-profitability.png)

The main indicators I selected are:

- **Median profit: $13.77M**
- **Median ROI: 80.72%**
- **Profitable movies: 67.77%**

Around two thirds of the movies with the necessary financial information therefore have a positive profit in the dataset.

Profit and ROI allow me to study two different aspects of performance.

**Profit** measures financial gain in absolute value.

**ROI** measures this gain compared with the initial budget.

A blockbuster can therefore generate a very high profit without having the highest ROI.

On the other hand, a low-budget movie can achieve a very high ROI with a lower absolute profit.

I performed several additional analyses such as:

- Ranking movies by profit
- Ranking movies by ROI
- Median profit by genre
- Median ROI by genre
- Median box-office revenue by release month
- Median budget and profit by release month
- Median budget by country
- Median ROI by country

Minimum movie count thresholds are applied to some comparisons.

This prevents a category containing only a few movies from artificially dominating the results.

**Animation** shows a particularly high median profit in the sample studied.

**Animation and Horror** also show high median ROI.

**June and December** stand out with particularly high median box-office revenue.

Comparisons between countries should be interpreted with caution because sample sizes are very different.

---

## 5. Main Results

The main results I obtained are:

- **Budget** shows the strongest association with box-office revenue (**r = 0.74**).
- The **number of votes** is also associated with box-office revenue (**r = 0.63**).
- **Score** shows a much weaker association (**r = 0.19**).
- **Runtime** also shows a weak association (**r = 0.25**).
- Around **67.8% of movies** with the necessary financial data are profitable.
- Profit and ROI highlight two different forms of financial performance.
- Animation and Horror show good profitability indicators in the sample studied.
- June and December show particularly high median box-office revenue.

It is important to keep in mind that no single variable can explain the commercial success of a movie.

Among the numerical variables studied, budget shows the strongest association with box-office revenue.

Other factors such as marketing, franchise popularity, distribution or actor popularity can also have an impact.

These variables are not available in the dataset and are therefore not measured in this analysis.

---

## 6. Analysis Limitations

- The dataset does not contain all movies released between 1980 and 2020.
- Data for 2020 is incomplete due to the COVID period.
- Around **28% of budget values are missing**.
- Financial amounts are not adjusted for inflation.
- Sample sizes vary significantly between genres, countries and production companies.
- The number of votes may be related to movie visibility as much as audience engagement.
- Marketing expenses are not available.
- Distribution scale is not available.
- Franchise membership is not directly provided.
- Correlation indicates an association, not a causal relationship.

---

## 7. Tools and Skills

**Tools**

- Dataiku
- Power BI
- DAX

**Data Preparation**

- Data Cleaning
- Data Quality
- Missing Value Analysis
- Duplicate Detection
- Data Transformation
- New Variable Creation

**Data Analysis**

- Exploratory Data Analysis
- KPI
- Median Analysis
- Profitability Analysis
- Pearson Correlation
- Time Analysis
- Segmentation
- Data Visualization

---

## 8. Project Workflow

**Raw Data → Data Quality → Dataiku Preparation → Variable Creation → Clean Dataset → Power BI → DAX and Statistical Analysis → Dashboard → Results**
