## Problem Statement


#### 1. Creating a new food product is a long and complex process. One of the many difficult determinations is establishing the potion size of the food. This is a delicate balance between many factors, including the nutrition aspects of the food in question. This project will attempt to compare a wide variety of food products and their nutrient contents (and/or ingredients), and to attempt utilize this information to predict a fitting portion size for the new food in question. 


#### 2. Recommender system that can take a product decription/category/ingredients list, and give options for other similar/healthier (lower fat etc) products. DOES THIS EVEN MAKE SENSE IN CONTEXT OF A RECOMMENDER SYSTEM?








(hopefully)
Performing unsupervised learning on the USDA database of branded food products in the US. This exploration will find ### FIGURE OUT SPECIFIC GOAL ### certain types of relationships between foods, their ingredients, nutrients, and manufacturers.

### Possible goals:
1. **grouping common ingredients of zero-fat foods by brand owner (which are the ingredients companies most often use for "healthier" foods like those without fat?) This would help people trying to buy healthy foods stay away from companies that use less favorable ingredients???**
2. What are the trade-offs/trends in other nutrients when a food is non-fat? (this is kind of already known?)
3. Comparing number of ingredients to nutrition facts, trends of companies that have longer ingredients compared to specific types of foods (this might be the same as above?)
4. brand opportunities - where do companies have dead spots in terms of food nutrition?



### old statements

The food industry is an extremely competitive business. In order for companies to keep up with each other, there is constant research being performed on competitors' products. This type of research often times means working with products that have little to no branding or identifying information, and could be produced by a secondary manufacturer on contract. Fortunately, the USDA maintains a database of over 250,000 branded food products currently on the market. This project will attempt to use a combination of nutrient information and ingredients (evaluated with natural language processing) on a selection of these products to create a predictive model that can classify the manufacturer of unknown foods for these research purposes.

ALSO/OR something about consumers beign able to use this to determine who made a specific food. People are becoming more invested in the supply chain of their foods, and have concerns with certain sourcing or practices related to growing/processing/manufacturing. At the same time, With so many food companies being owned by other entitites, it can be difficult to tell what company a specific food came from. This project attempt to create a classification model that uses a combination of product nutrient information, and product ingredients (evaluated with natural language processing) that can predict the manufcaturer of a given food. 