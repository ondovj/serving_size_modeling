## Problem Statement

Creating a new food product is a long and complex process. One of the many difficult determinations is establishing the potion size of the food. This is a delicate balance between many factors, including marketing, cost, and especially the nutrition aspects of the food in question. In order to get a head start on different aspects such as marketing, branding, or further changes to the food itself, it would be helpful to have an approximate serving size available to the team before it has actually been established.

This project will attempt to compare a wide variety of food products and their nutrient contents (and/or ingredients), and to attempt utilize this information to predict a fitting portion size for the new food in question. The prediciton of the serving size will be performed by a regression model, as serving size is a continuous variable. In order to buld the best model, two main metrics will be utilized, mean squared error, and R<sup>2</sup>. These two metrics will give us agood profile of how much error there is in our predictions, as well as how well our models cover variance in the datapoints.


## Data

The data being used in the project is the USDA Branded Food Products Database. It contains over 260,000 branded foods, with their ingredients, nutrition information, and many more aspects of those foods. 

|Category|Description|Example|
|---|---|---|
|fdc_id|The database ID of the food product|356425|
|brand_owner|Company that owns the brand of the food product|G. T. Japan, Inc.|
|branded_food_category|Market category of the food product|Ice Cream & Frozen Yogurt|
|description|Deailed description of the food product|MOCHI ICE CREAM BONBONS|
|ingredients|Ingredients list of the food product|SUGAR, CORNSTARCH.|
### need to finish dictionary

## Executive Summary

The first step in this project was to retrieve the desired data. The USDA hosts this data on a relational database with API access, but it also has the full dataset available as a zip file, which was the retrieval method in this case.

After some initial analysis, there were two types of serving size, and one subset of the data was isolated, so the remainder of the project was performed only on foods that have serving sizes in grams.

The next step was teh properly clean the data, which was the bulk of the work in this project. Despite having legal standards for labeling practices, ther eis still much variation beteween foods, and many label options can be optional in certain cases, lading to many null values in the data. Utilizing the FDA guidelines, and the contextual information, much of the missing data was able to be imputed.

After the cleaning, EDA was performed to determine some of the possible connections between the features and the serving size target.

The last step was to perfrom the modeling, which utilized several different regression types. These included linear, ridge, LASSO, and a neural network. The resulting best model was a neural network that minimized MSE below 1000, and had an R<sup>2</sup> score above 90%.

## Conclusions

Utilizing a neural network gave use the best results overall. It was able to increase the R<sup>2</sup> score above 90%, and still limit variance to less than 2%. It was also able to minimize MSE fra better than the other models that were made. However, this model was still not perfect, and was subject to significant underpredcition as the true serving size increased. 

As discussed above, this may be influence by factors unseen by the model, such as the percentage of the food item that is not typically eaten. In addition, this model only takes certain attributes into account, and there are many other factors that can have an impact on serving size, such as package size, sale price, or targeted demographic. Many of these factors can be proprietary information to the manufacturing company, and are unavailable to the public, making a deeper analysis difficult. This could, however, be adapted within a specific company to account for some of these features, or to be trained on a more specific set of foods products.

In the end, this model should still be fairly useful to a project team that is working to develop a new food product. If the standard nutrition facts and category can be enterered, the resulting serving size should be fairly close to similar products on the market in that category, and can be useful in the development process. This way, researchers have a good idea of what their final servings size might be, and can have a head start on things like branding and marketing.

## Recommendations

One of the main recommendations for this project would be to conduct further analysis of the vectorized ingredients. Utilizing the ingredients as features did not appear to help our models in the current scope, though with more time to optimize, they may be able to improve the model further.

Another interesting step to take would be to perform PCA on the nutrient features. This would be able to definitively eliminate any possibility of multicolinearity in the X variables. It would also ensure that only the most valuable elements of each of the features were being effectively used to make the prediction.

Further utilization of the neural network grid search function. The project timeline and available computing power were severe limits on fully fleshing out the neural network. Of course the possibilities are truly endless, but even within the scope of layers, nodes, and regularization that were searched through here, there is most likely further optimization that could be done.

Another modeling option could be to use a support vector machine (SVM), as this may be a more fitting model for this type of data. Unfortunately, due to the large amount of data and features being used, there was once again a computing power issue preventing this type of model from being run.

Overall, the computational issues in this project could possibly be overcome by utilizing cloud computing services, such as those available on Amazon Web Services, or perhaps even just using a more powerful home computer.

The last recommendation would be to continually maintain the dataset, as the USDA periodically updates the information store in it. This could entail downloading the zip file when a new version comes out, or it could be linked to the API access to continually update.