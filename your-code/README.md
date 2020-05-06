<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100" align="right"/>


#   Project Ironhack Data Bootcamp: Job offers' Fraud-Detection with NLP

Miguel Ángel Ávalos Barrios, Javier Carrasco Morente, Miguel García MElgar and Karla Vizcarra

*Data Part Time Barcelona Dic 2019*


## Content
- [Project Description](#project)
- [Dataset](#Dataset)
- [Workflow](#workflow)
- [Results](#results)

<a name="project"></a>

## Project Description

### Overview

In order to experience how to work in a ML project as a group, and to learn more on NLP we have been working on a job offers' dataset so as to train a classification model able to distinguish genuine from fraudulent offers.


### Technical Requirements (not yet)

The technical requirements for this project have been:

* Trying to apply everything I have learned so far about data analysis such as data cleaning, data manipulation, data visualization, and various statistical analysis methods.


### Deliverables (not yet)

The following deliverables were pushed to our Github repo for this chapter.

* **A Jupyter Notebook (fraud-detection_NLP.ipynb)** containing our Python codes, outputs, and data visualizations. Making sure to include explanations for each step in Markdown cells or Python comments.
* **A folder named "data"** containing the dataset we used as well as "heavy" data we exported from our notebook.
* **A folder named "images"** containing the images we used as input in our EDA and some plots we exported.
* **This README.md** containing a detailed explanation of the followed approach for carrying out this project.

<a name="Datasets"></a>

## Dataset
 
We used this dataset from Kaggle, [[Real or Fake] Fake JobPosting Prediction](https://www.kaggle.com/shivamb/real-or-fake-fake-jobposting-prediction), that holds around 18K job descriptions out of which about 900 are fake. The data consists of both textual information and meta-information about the jobs. 
  
<a name="workflow"></a>


## Introduction

As said above, we've worked on a dataset of job descriptions and their meta information in which a small proportion of these descriptions were fake or scam, which can be identified by the column "fraudulent".

**Columns**:
* `job_id` Unique Job ID
* `title` The title of the job ad entry.
* `location` Geographical location of the job ad.
* `department` Corporate department (e.g. sales).f
* `salary_range` Indicative salary range (e.g. $50,000-$60,000)
* `company_profile` A brief company description.
* `description` The details description of the job ad.
* `requirements` Enlisted requirements for the job opening.
* `benefits` Enlisted offered benefits by the employer.
* `telecommuting` True for telecommuting positions.
* `has_company_logo` True if company logo is present.
* `has_questions` True if screening questions are present.
* `employment_type` Full-type, Part-time, Contract, etc.
* `required_experience` Executive, Entry level, Intern, etc.
* `required_education` Doctorate, Master’s Degree, Bachelor, etc.
* `industry Automotive` IT, Health care, Real estate, etc.
* `function Consulting` Engineering, Research, Sales etc.
* `fraudulent` **target** Classification attribute


## Workflow (not yet)

###  Introduction
####  Objectives
####  Imports

###  1. Exploratory Data Analysis
####  Context
####  Global EDA
#### Numerical columns
#### Categorical variables: Here we plotted every categorical column plus we created a BoW of long-text categorical variables by tokenizing with spaCy.

###  2. Preprocessing
####  Categorical: It refers to columns of categorical variables which are not whole sentences/paragraphs. We cleaned them and used One-Hot Encoding.
####  Numerical: We created a new salary range column that indicates presence or absence of salary in the previouys salary range column or listed in benefits.
####  Text: It refers to columns of categorical variables which are whole sentences/paragraphs. Those columns have been combined into 1 and have been cleaned and lemmatized to form new BoW based on it's lemmes. After that we use TF-IDF to vectorize each word.
#### Merge

###  3. Model building and evaluation
####  Undersampling of the dataset and trial of 12 different classification methods to train our model.

###  4. Hyperparameter Tunning of the Models (not yet)

###  5. Ensemble (not yet)


## Conclusions (not yet)

##### Hofstede's six-dimensions model (2015) correlations

**Most correlations seem to be negligible but there's still some significant ones:**
`Power distance` highly negatively correlates with `Individualism vs Collectivism`, and has low but significant correlations with `Uncertainty Avoidance`, positively, and negativley with  `Indulgence vs Restraint`. The latter also correlates moderately negatively with `Long Term versus Short Term Orientation`.

So the **more hierarchy** is accepted in a country, the **more colectivistic** the culture seems being also quite probable citizens' tendency to **avoid risk** and **surpress emotions and pleasure**.
In those countries where **pleasure seek is indulged**, usually there's also a common tendencty to think in the **short-term future**.

##### World Happiness Report 2015

**As the 6 indexes the test uses were chosen from factorizing Happiness Score, we will just focus on correletions between them.**
They all positively correlate except `Generosity` with a negligible negative correlation with `Economy`.
Moreover, the top 3 correlations, being correlations over 0.5, are the top 3 Happiness Score factors: `Economy`, `Family` and `Health`.

##### Comments about VGC 2020 Usage % and Base Stats Mean relationship

Pokémon's usage in VGC 2020 online competitions seems to be ***positively correlated*** with each Pokémon's Base Stats Mean forming a ***logarithmic growth*** so that Stats Means grow a lot without affecting much to VGC Usage %, and from 70 base stats means, usage starts increasing really fast, and it almost stops growing from 85-90 mean values.

##### Correlations of the merged and standardized dataset (Happiness Score + 6 cultural dimensions)
**Most correlations seem to be negligible but there's still some significant ones:**
`Happiness Score` highly positively correlates with `Indulgence vs Restraint`(0.73), and moderately correlates with `Power distance` and `Individualism vs Collectivism`, respectively in a negative (-0.56) and in a positive(0.44) way.

So that **higher levels of happiness** are registered in coutries where **pleasure seek is indulged** and can be described as **egalitarian** and **individualistic**.

##### Hypothesis testing
As the hypothesis were sided and we have standardized data a one sided T-Test with a 95% confidence interval was performed. 

H0: Individualistic societies are happier (>) than colectivistic ones.
H1: Individualistic societies aren't happier (<=) than colectivistic ones.

With a stat=0.445 and p=0.001; **H0 has been accepted**.


##### According to the regression analysis using a multivariate OLS model:

The most important variables in the model are, in this order, "ind", "lto", "pdi" and "idv"; having an R-squared of 0.759, so that a lot of its variability depends on the variables included in the model.

It is kinda curious as its correlations coefficient were:

- `Indulgence vs Restraint` = 0.73, which is coherent with the regression coefficient of 0.77
- `Power - distance` = -0.56, differing in size from the regression coefficient, -0.21
- `Individualism vs Collectivism` = 0.44, which as PDI has a regression coef "halving" its correlation one being  0.163
- `Long Term vs Short Term Orientation` = -0.11, which is pretty interesting as its regression coefficient doubles and turns positive, 0.23

##### After doing a PCA

**87,9% of variance can be explained with 4 of the 6 possible components**, they're probably the top 4 obtained from the regression model but we can't be sure. 

We have also seen that with a 5th component 95% of the variability would be explained, but remember there were just 6, so it is not really a good idea to focus on few components we you are already using just a few.

## Future Improvements (not yet)

* We have to find out why correlation coeficients differ but one of the main issues could be that the sample was not that big and it had to be reduced a lot. 

* There are currently 247 countries but one of our datasets had results from 111 countries and the other only considered 158 and they didn't always coincide plus there were some NaN values. We ended up with a dataset of just 57 countries' results. I should try to look for more complete and up-to-date data.

* It would be interesting to analyze how other indexes that conform Happiness Score correlate with the 6 cultural dimensions.
