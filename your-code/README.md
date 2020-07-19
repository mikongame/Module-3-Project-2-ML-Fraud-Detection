<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Project Ironhack Data Bootcamp: Job offers' Fraud-Detection with NLP
**Miguel Ángel Ávalos Barrios, Javier Carrasco Morente, Miguel García Melgar and Karla Vizcarra**

*Data Analytics Part-Time, Barcelona, Dec19*

## Content
- [Project Description](#project-description)
- [Objective](#objective)
- [Dataset](#dataset)
- [Introduction](#introduction)
- [Workflow](#workflow)
  * [Exploratory Data Analysis](#exploratory-data-analysis)
  * [Preprocessing](#preprocessing)
  * [Model Training and Evaluation](#model-training-and-evaluation)
  * [Conclusion](#conclusion)
- [Future improvements](#future-improvements)
- [Tools and requirements](#tools-and-requirements)
- [Links](#links)

## Project Description
In order to experience how to work in a ML project as a group and to learn more on NLP, we have been working on a job offers' dataset so as to train a classification model able to distinguish genuine from fraudulent offers.

## Objective
We mainly wanted to create a **classification model using text data features and meta-features to predict which job descriptions are fraudulent**. As well as, finding out if there are **key traits/features** (words, entities, phrases) of job descriptions which are **intrinsically fraudulent**.

## Dataset
We used this dataset from Kaggle, [[Real or Fake] Fake JobPosting Prediction](https://www.kaggle.com/shivamb/real-or-fake-fake-jobposting-prediction), that holds around 18K job descriptions out of which about 900 are fake. The data consists of both textual information and meta-information about the jobs.

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
* `fraudulent` **target** Classification attribute.

## Workflow
### Exploratory Data Analysis
First off all, we checked how the data looked like as well as its shape, columns and dtypes. Then we confirmed there where no nulls or duplicates.
#### Numerical columns
With the raw data we can only find a single correlationship with the target "fraudulent" that is somewhat significative:

It seems it is slightly more common for fraudulent job offers to not contain the company logo, though the relationship is of -0.26.
#### Categorical variables 
Here we plotted every categorical column plus we created a BoW of long-text categorical variables by tokenizing with spaCy.

<img src="images/output_images/mbti_count.png" align="middle">

When I checked for unique values and target distribution I found out that in posts there was a unique value per entrance, and that the distribution was horribly unbalanced, especially considering distributions found by the original researchers and authors of this psychometric measure (MBTI).

<img src="images/mbti_distr_spain.PNG" align="middle">

Finally, I created a Bag of Words by tokenizing posts column using Spacy, so as to use them to create a word cloud and visualize text before starting cleaning it.

<img src="images/output_images/mbti_token_cloud.png" align="middle">

### Preprocessing
* I used SpaCy to clean and lemmatise the words from each post.
* Once cleaned I transformed the corpus of the text to a matrix using TfidfVectorizer.
* As the sparse matrix was quite big I tried on 3 different ways to reduce its dimensionality:
  * Using Truncated SVD with 100 components.
  * Using UMAP.
  * Using Truncated SVD and then UMAP on its results.
* Enclosing preprocessing, I encoded my target labels i two different ways. One would use all 16 types, and the other would rather focus on its 4 axes. Thereafter, I created 6 different datasets that I will use to train the models by combining each dimensionality reduction strategy which each kind of labelling the target variable. 

### Model Training and Evaluation
#### Machine Learning Models
From the 6 datasets mentioned above, I trained quite a few models by combining different algorithms for each dataset, and each target, but also with the original dataset size and also with resampled versions:
* The algorithms used were `GaussianNB`, `LogisticRegression`, `KNeighborsClassifier`, `DecisionTreeClassifier`, `RandomForestClassifier`, `GradientBoostingClassifier` and `MLPClassifier`.
* So using 7 models, 2 sample sizes, 5 different labels (type + 4 possible dimensions) and 3 dimensionality reduction methods, I ended up training 210 different models. 

<img src="https://github.com/mikongame/NLP-to-predict-Myers-Briggs-Personality-Type/blob/master/images/Model_TSVD_Types.PNG?raw=true" align="middle">

* The table shows the results of training the different algorithms with the results from applying TSVD (100 components) to reduce the dimensionality of the types' dataset without resampling, as the best results were obtained from GraddientBoostingClassiffier using this particular sample.
#### Deep Learning Models

Before proceeding further with hyperparameters tuning of the ML models previously evalueted, I lets try with a combinatio nof unsupervised ML and DL.

I will use GloVe, an unsupervised learning algorithm for obtaining vector representations for words, altogether with a LSTM recurrent neural network to train two models, one for personality types and another one for dimensional trait axes.

<img src="images/output_images/types_history.png" align="middle">
<img src="images/output_images/dimensions_history.png" align="middle">

As you can see the results are lower than the ones using Gradient Booster and Random Forest.

#### Fine tuning of the best models

<img src="images/tuned_types.PNG" align="middle">

### Conclusion

The model trained has an F1 Score of 0.651957, that is, this model can predict MBTI personality type 65,2% of times.

Despite not seeming particularly outstanding results, as a multiclass classification (16 types), randomness baseline was located at 6.25%. So predictions from this model would be more than 10 times more accurate than guessing.

## Future improvements
Future improvements would include further hyperparameter tuning, training the best couple of models using better-balanced samples and testing the resulting best model on a completely different sample.  

Ideally, I would also like to adapt it to the Big Five model, as is the personality models of the highest predictive validity. Still, adapting it/ doing a new similar model for predicting other psychological metrics out of text would be mesmerizing too.


## Tools and requirements
In order to train more models simultaneously, we've been both using Jupyter Notebooks on our own machines and also using default virtual machines with Google Colab.

We have also used the latest Conda with the last version of the following packages and libraries:
* os
* pandas
* numpy
* scipy
* math
* random
* seaborn
* matplotlib
* PIL
* wordcloud
* re
* itertools
* spacy
* en_core_web_sm
* string
* collections
* pickle
* umap
* imblearn
* sklearn 

## Links
[Repository](https://github.com/mikongame/Module-3-Project-2-ML-Fraud-Detection/tree/develop/your-code)  

[Slides](https://drive.google.com/file/d/1yxGmtVNFPa4AZYL16zA0mP8AgQVconof/view?usp=sharing) cambiar
