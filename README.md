Overview
The goal of this project is to analyze housing data in King County Washington to figure out what features have what sort of impact on the sale price, we then use this data to solve some real world problem.  Along the way we will need to clean our data (replace or drop columns with nul values, normalize data, converting categorical/ordinal data to integer values, etc), explain and display our work/findings, and come up with the best model to predict house prices.

Business and Data Understanding
Explain your stakeholder audience here
Buisiness Problem
Substantial Realty Co. has hired me to find to predict the value of houses in the King County area.
Modeling
Regression Results
Conclusion


The Data

id - Unique identifier for a house -> This is not affecting house price.

date - Date house was sold

yr_built - Year when house was built
-> It may be a good idea to calculate the house age using the columns date and yr_built. Dates needs to be converted to datetime.

price - Sale price (prediction target)

bedrooms - Number of bedrooms

bathrooms - Number of bathrooms -> Bedrooms and bathrooms may have some correlation.

sqft_lot - Square footage of the lot

floors - Number of floors (levels) in house -> I believe number of floors will be highly impacting the price.

waterfront - Whether the house is on a waterfront

Includes Duwamish, Elliott Bay, Puget Sound, Lake Union, Ship Canal, Lake Washington, Lake Sammamish, other lake, and river/slough waterfronts
view - Quality of view from house

Includes views of Mt. Rainier, Olympics, Cascades, Territorial, Seattle Skyline, Puget Sound, Lake Washington, Lake Sammamish, small lake / river / creek, and other -> Waterfront and view columns seem to be correlated as well.
condition - How good the overall condition of the house is. Related to maintenance of house.

1-5 from poor to very good.
grade - Overall grade of the house. Related to the construction and design of the house.

1-13 from very poor to excellent. -> I think the condition and grade of the house are two very important factors in the price as well as the zipcode. These columns should be converted to integer values. Also, it is highly likely that thse two columns are correlated.
sqft_living - Square footage of living space in the home

sqft_above - Square footage of house apart from basement
sqft_basement - Square footage of the basement -> There is a high chance that sqft_living, sqft_above and sqft_basement columns are linearly related. I am guessing sqft_living = sqft_above + sqft_basement from the definition.

yr_renovated - Year when house was renovated -> Rather than the year renovated, knowing if the house was renovated or not, may be more informative and predictive.

zipcode - ZIP Code used by the United States Postal Service -> I am guessing zipcode is the most important factor in the price. The number itself does not mean anything for prediction, but the category is important, so I believe this should be one hot encoded.

lat - Latitude coordinate

long - Longitude coordinate -> I don't think lat and long coordinates add more information on top of the zipcode, may end up removing them. These can be used together to calculate the distance from city center or some important places in the city, which may help predict the price.

sqft_living15 - The square footage of interior housing living space for the nearest 15 neighbors

sqft_lot15 - The square footage of the land lots of the nearest 15 neighbors -> It may be a good idea to create new columns, a measure of how big the house is, compared to the houses in the neighborhood.





waterfront I will drop because it has a lot of null values.

view, condition and grade are ordinal. They have some meaningful ranking in terms of how they affect the price so I will convert them to integer values

According to a seaborn heatmap the variable most strongly associated with price seems to be sqft_living.
The next three seem to be sqft_ sqft_ and the number of bathrooms.
so the size of the unit and the number of bathrooms seem to have a big impact.

In our analysis, we iterated from simple linear model to multiple linear model by adding each mostly correlated column to the model and checking the multicollinearity at each iteration.






Rationale: Explaining why you are using statistical analyses rather than basic data analysis
For example, why are you using regression coefficients rather than just a graph?
What about the problem or data is suitable for this form of analysis?
For a data science audience, this includes your reasoning for the changes you applied while iterating between models.
Results: Describing the overall model metrics and feature coefficients
You need at least one overall model metric (e.g. r-squared or RMSE) and at least two feature coefficients.
For a business audience, make sure you connect any metrics to real-world implications. You do not need to get into the details of how linear regression works.
For a data science audience, you don't need to explain what a metric is, but make sure you explain why you chose that particular one.
Limitations: Identifying the limitations and/or uncertainty present in your analysis
This could include p-values/alpha values, confidence intervals, assumptions of linear regression, missing data, etc.
In general, this should be more in-depth for a data science audience and more surface-level for a business audience.
Recommendations: Interpreting the model results and limitations in the context of the business problem
What should stakeholders do with this information?