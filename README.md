
![title](https://raw.githubusercontent.com/emdemor/prediction-house-prices-on-Brazil/master/source/title.png)



**Author**: Eduardo M. de Morais, MSc.

**Date**: Jul 17 2020

# Table of Contents
1. [Introduction](#intro)
2. [Methodology](#method)
3. [Conclusions](#conc)

<a id="intro"></a>
# 1.  Introduction


Through this notebook, I have attempted to predict rental prices from a dataset containing data from Brazil. Of course, this is and study case and some idealized procedure was assumed. The main objective here is to study and understand the data to use the knowledge to construct a model to predict the total rental price. The source dataset has the following columns:


* **city** (*categorical*): City where the house or apartment is located. Here, we have two option of cities that the collector didn't specified. 
* **area** (*integer*): Area of constructed  property (The unity is not informed. I'm am assuming that is squared meters, the most usual in Brazil)
* **rooms** (*integer*): The number of rooms in the property
* **bathroom** (*integer*): The number of bathrooms in the property
* **parking spaces** (*integer*): The number of parking spaces at the garage
* **floor**: (*integer*): The number of the floor (if the property is an apartment)
* **animal** (*boolean*): If is allowed to have animals at the house
* **furniture**: (*boolean*): If is a furnished property
* **hoa** (*float*): Homeowners association fee.
* **rent amount** (*float*): Base value of rent
* **property tax** (*float*): State property tax (ad valorem tax)
* **fire insurance** (*float*): The value of fire insurance
* **total** (*float*): The total money spent on rental activity

<a id="method"></a>
# 2. Methodology
In general, when planning a place to live, we have to take into account all expenses and taxes to choose the best place. Because of this, the adopted target to this dataset will be the **total** column.


In real cases applications, the user has no information concerned to property cost, like  **hoa**, **rent amount**, **property tax**, **fire insurance** and **total**. In general, this variables are mutually correlated, firstly, because **total** is the sum the others and; secondly, because in real life, the taxes and fees are  proportional to property value and, somehow, to the rental price. An applicable model must be capable to predict the rental price based only on **city**, **area**, **rooms**, **bathroom**, **parking spaces**, **floor**, **animal** and **furniture**.   However, since this is a idealized study of case, which objective is only to practice the regression models, let's assume that the cost variables is accessible to user. So, our task here is to define the best model to the **total** rental price from the information of other columns.

To construct a system capable to make good recommendations, it is necessary to understand how the features influence the desired variable. To make this, I will split my work in three stages:

**1. Exploring**: An exploratory analysis, to understand the structure of data, missing values, correlations and etc, to select the best set of features to be used at the analysis.


**2. Modeling**: In this step, I try to find the best and simplest model for describing the data. I do this by testing the influence of features on total values. Since that the definition of a best model is something complicated and subjective, I will choose the model  which best efficiency in the follow approach:

>A. Split dataset into test (33%) and training (67%)

>B. Use training dataset to fit the parameters of model

>C. Use the trained model to predict the **total** of test dataset

>D. Use predicted an original **total** to evaluate the *mean average error* and *R2 score* metrics

The model with the lowest mean average error value will be considered the best model. In case of a tie, the one with the highest R2 will be chosen.

**3. Optimizing**: With the chosen model, I want to give to user a system that returns the distribution of prices from a specified set of features. (*To be implemented in next versions*)

<a id="conc"></a>
# 3. Conclusions
Using the complete set of feature columns, we could fit a Linear Model which predicts the total rental value extremely well. The mean absolute error is something about R$ 77,00 and the R2 0.998. However, this cannot be considered a real applicable model because, as we argued before, the cost variables used to define this model are correlated with the target. From a didactic perspective, it was possible to understand the influence of the number of features and its correlations on the quality of model and, in particular, it was possible to see that in certain situations, regression models can provide quite different results.

Following the same steps, I tried to build a realistic model using only the property's features, like city, area, rooms, bathroom, parking spaces, floor, animal and furniture (that are the features accessible to the user), to predict the total. In this case, the predictability of the models significantly reduces. The best regression approach for this considerations is the Random Forest, with mean error of R$ 1848,75 and R2 score of 0.65. Although these metrics are quite bad compared to the ideal case, it is possible to find advantages in using this model. The mean of total columns is R$ 5816,84 with and the standard deviation of R$ 4643,00. So, as our model is predicting data with mean absolute error significantly less than the standard deviation, we can conclude that there exists an influence of this feature to the total rental cost. For a most efficient approach, however, it is necessary to consider a greater number of features.