# Modeling Food Serving Sizes Through Nutrition Profiles

## Problem Statement

Creating a new food product is a long and complex process. One of the many difficult determinations is establishing the portion size of the food. This is a delicate balance between many factors, including marketing, cost, and especially the nutrition aspects of the food in question. In order to get a head start on different aspects of the development process, such as marketing, branding, or further changes to the food itself, it would be helpful to have an approximate serving size available to the team before it has actually been established.

This project will attempt to compare a wide variety of food products and their nutrient contents (and/or ingredients), and to attempt to utilize this information to predict a fitting portion size for the new food in question. The prediction of the serving size will be performed by a regression model, as serving size is a continuous variable. In order to build the best model, two main metrics will be utilized, mean squared error, root mean squared error, as well as R<sup>2</sup> and adjusted R<sup>2</sup>. These metrics will give us a good profile of how much error there is in our predictions, as well as how well our models cover variance in the data points.


## Data

The data being used in the project is the USDA Branded Food Products Database<sup>1</sup>. It contains over 260,000 branded foods, with their ingredients, nutrition information, and many more aspects of those foods. The original data descriptions can be found in the datasets folder of this repository. The final table as compiled in this project contains the following fields:

|Category|Description|Example|
|---|---|---|
|fdc_id|The database ID of the food product|356425|
|brand_owner|Company that owns the brand of the food product|G. T. Japan, Inc.|
|branded_food_category|Market category of the food product|Ice Cream & Frozen Yogurt|
|description|Detailed description of the food product|MOCHI ICE CREAM BONBONS|
|ingredients|Ingredients list of the food product|SUGAR, CORNSTARCH.|
|serving_size|Serving size in grams of food product|40.0|
|household_serving_fulltext|The product-specific size of the portion|1 PIECE|
|energy|Calories in 100g of the food|200.0|
|fat_total|Total grams of fat in 100g of the food|6.25|
|fat_sat|Total grams of saturated fat in 100g of the food|3.75|
|fat_trans|Total grams of trans-fat in 100g of the food|3.57|
|chol|Total milligrams of cholesterol in 100g of the food|25.0|
|protein|Total grams of protein in 100g of the food|2.5|
|carbs|Total grams of carbohydrates in 100g of the food|35.00|
|fiber|Total grams of fiber in 100g of the food|3.6|
|sugars|Total grams of sugar in 100g of the food|30.0|
|sodium|Total milligrams of sodium in 100g of the food|75.0|

## Executive Summary

The first step in this project was to retrieve the desired data. The USDA hosts this data on a relational database with API access, but it also has the full dataset available as a zip file, which was the retrieval method in this case.

After some initial analysis, there were two types of serving size, and one subset of the data was isolated, so the remainder of the project was performed only on foods that have serving sizes in grams.

The next step was to properly clean the data, which was the bulk of the work in this project. Despite having legal standards for labeling practices, there is still much variation between food labels, and many nutrition declarations can be optional in certain cases, leading to many null values in the data. Utilizing the FDA guidelines, and the contextual information of the foods, much of the missing data was able to be imputed<sup>4<sup>.

After the cleaning, additional EDA was performed to determine some of the possible connections between the nutrition features and the serving size target.

The last step was to perform the modeling, which utilized several different regression types. These included linear, ridge, LASSO, and a feed forward neural network. The resulting best model was a feed forward neural network that minimized MSE below 1000, and had an R<sup>2</sup> score above 80%.

## Conclusions

Utilizing a feed forward neural network gave us the best results overall. This model utilized three hidden layers with 256, 128, and 64 nodes. Each hidden layer used a ReLU activation with an L2 regularization rate of 0.001, while the output layer used the identity function. The model was able to increase the R<sup>2</sup> and adjusted R<sup>2</sup> score above 80%, and still limit difference between the train and test sets to below 1.5%. It was also able to minimize MSE and RMSE far better than the other models that were made. However, this model was still not perfect, and there are still outliers in the residuals. Unfortunately, utilizing a neural network does not give us any kind of further interpretability beyond the metrics that were tested. Unlike the linear models, we do not have clear coefficients that can be related back to specific features in terms of importance.

As discussed above, this may be influenced by factors unseen by the model, such as the percentage of the food item that is not typically eaten. In addition, this model only takes certain attributes into account, and there are many other factors that can have an impact on serving size, such as package size, sale price, or targeted demographic. Many of these factors can be proprietary information to the manufacturing company, and are unavailable to the public, making a deeper analysis difficult. This could, however, be adapted within a specific company to account for some of these features, or to be trained on a more specific set of food products.

In the end, this model should still be fairly useful to a project team that is working to develop a new food product. If the standard nutrition facts and category can be entered, the resulting serving size should be fairly close to similar products on the market in that category, and can be useful in the development process. This way, researchers have a good idea of what their final servings size might be, and can have a head start on things like branding and marketing.

## Recommendations

One of the main recommendations for this project would be to conduct further analysis of the vectorized ingredients. Utilizing the ingredients as features did not appear to help our models in the current scope, though with more time to optimize, they may be able to improve the model further. A more complex method of cleaning and vectorizing this feature may allow it to be more effectively be incorporated into the model. As ingredients lists are always in order of largest to smallest amounts, it may be possible to use some kind of weight attribute on ingredients to show the impact of that ingredient of the food's nutrition and serving size. Further use of NLP could also be used to analyze the food descriptions or brand owners as well.

Another interesting step to take would be to perform PCA on the nutrient features. This would be able to definitively eliminate any possibility of multicolinearity in the X variables. It would also ensure that only the most valuable elements of each of the features were being effectively used to make the prediction.

Further utilization of the neural network grid search function. The project timeline and available computing power were severe limits on fully fleshing out the neural network. Of course the possibilities are truly endless, but even within the scope of layers, nodes, and regularization that were searched through here, there is most likely further optimization that could be done.

Another modeling option could be to use a support vector machine (SVM), as this may be a more fitting model for this type of data. Unfortunately, due to the large amount of data and features being used, there was once again a computing power issue preventing this type of model from being run. It may also be possible to use a decision tree-based regressor model on this data.

Overall, the computational issues in this project could possibly be overcome by utilizing cloud computing services, such as those available on Amazon Web Services, or perhaps even just using a more powerful home computer.

The last recommendation would be to continually maintain the dataset, as the USDA periodically updates the information stored in it. This could entail downloading the zip file when a new version comes out, or it could be linked to the API access port to continually update.

## Sources

The sources used throughout this project have been compiled below:

1. https://data.nal.usda.gov/dataset/usda-branded-food-products-database
2. https://energyeducation.ca/encyclopedia/Joule
3. https://dietarysupplementdatabase.usda.nih.gov/ingredient_calculator/help.php
4. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfcfr/CFRSearch.cfm?fr=101.9
5. https://my.clevelandclinic.org/health/articles/4182-fat-and-calories
6. https://www.ewg.org/foodscores/products/610563222087-SweetActionIceCreamBrownSugarBananaBrownSugarBanana
7. https://www.instacart.com/giant/products/17900558-kitchens-seafood-shoreline-feast-mussels-clams-shrimp-sausage-and-veggies-in-a-flavorful-broth-4-lb
8. https://www.nutritionvalue.org/Spices%2C_chili_powder_nutritional_value.html
9. https://www.instacart.com/town-and-country/products/3344349-tapatio-spice-packet-8-ct
10. https://fortune.com/global500/2019/
11. https://www.sciencedirect.com/science/article/pii/B9781845690182500088
12. https://www.ncbi.nlm.nih.gov/pubmed/3863796
13. https://www.sciencedaily.com/terms/citric_acid.htm