![](https://github.com/ChadDelany/drought_prediction/blob/main/data/images/effect_of_drought_on_agriculture.jpg)

# **Drought Prediction using Rudimentary Meteorological & Soil Variables**

## Data Science Project

- For code and detailed analysis, go to [notebooks](https://github.com/ChadDelany/drought_prediction/tree/main/notebooks).
- For raw data, go to [data](https://github.com/ChadDelany/drought_prediction/tree/main/data).
- For the full report, presentation slides, and initial project proposal, go to [reports](https://github.com/ChadDelany/drought_prediction/tree/main/reports).

### Problem Statement

The United States has an abundance of weather and soil data compared to other countries. Using basic weather and rudimentary soil data, can we accurately predict droughts in the United States? Can a model be developed that has an accuracy greater than 80% within the next two months? Can these results be generalized to other countries with less available data resources?

### Context

With increasing climate change and an overall increase in global temperature, the occurrences of drought are expected to become more prevalent and occur in areas that historically over the last several hundred years have been less likely to experience drought. Drought impacts agriculture directly but also impacts water supply to urban areas as well. With a shifting pattern of drought, using long-term historical patterns is becoming increasingly unreliable to predict present-day conditions. Infrastructure to support both agriculture and urban areas has been developed around historic drought patterns and will need to adapt to permanently shifted present-day drought patterns. As well, the countries’ economies throughout the world have become inherently intertwined and drought in one part of the globe has significant impact on the rest of the world.

### Analysis

The dataset covered the time period from 2000 - 2020 with 18 daily meteorological variables, a weekly drought score, and 30 rudimentary soil variables for the 3,143 counties in the US.   The training data set contained approximately 2.3 million rows of data. Several linear regression models were tried with the dataset and the drought score target variable.  None of these models produced high enough accuracy.  The problem was converted to a classification one and the drought score target variable was convert from a continuous variable to an integer that corresponded with the original drought categories (see the [data dictionary](https://github.com/ChadDelany/drought_prediction/blob/main/notebooks/99_appendix_data_dictionary.ipynb) for more explanation).  Multiple classification models were tried.   The random forest model gave the most consistently accurate results.  The hyperparameters for the random forest were then tuned to increase the accuracy.  

### Results

This is a comparison of the classification models' accuracy.

| Model Metric         | ROC AUC | Total  Accuracy | Mean Accuracy  per Class | Accuracy per  Class STD |
| -------------------- | ------- | --------------- | ------------------------ | ----------------------- |
| Logistic  Regression | 0.844   | 60%             | 27%                      | 16%                     |
| Nearest  Neighbor    | 1.472   | 68%             | 55%                      | 9%                      |
| Random Forest        | 1.72    | 77%             | 75%                      | 5%                      |

The random forest model was trained on all available data, on select variables to decrease the correlation between variables and then applied to the test dataset to verify the model.  The table below breaks down the accuracy of each model by each drought category.

| Training: All Variables |           | Training: Select Variables |           | Test Set: All Variables |           |
| ----------------------: | :-------: | -------------------------: | --------- | ----------------------: | --------: |
|                   Class | Accuracy  |                      Class | Accuracy  |                   Class |  Accuracy |
|                       0 |   78.8%   |                          0 | 70.3%     |                       0 |     76.1% |
|                       1 |   73.5%   |                          1 | 61.5%     |                       1 |     17.2% |
|                       2 |   68.9%   |                          2 | 58.9%     |                       2 |     14.6% |
|                       3 |   68.7%   |                          3 | 59.1%     |                       3 |      4.8% |
|                       4 |   74.3%   |                          4 | 66.2%     |                       4 |        0% |
|                       5 |   83.7%   |                          5 | 76.2%     |                       5 |        0% |
|               **Total** | **77.0%** |                  **Total** | **68.8%** |               **Total** | **73.7%** |



### Conclusion and Next Steps

This process did produce a viable model and demonstrated the usefulness of Random Forests. It was not able to highlight a few, key variables. The next steps to improve this model would be:

- Allocate more resources so that the training can be done on the entire training dataset.
- Subset the training dataset and rerun the models to allow for a standard cross validation procedure and allow tools that determine important input variables to be determined.
- Incorporate ordinality information into the classification schema. 
- Incorporate a time series analysis that capitalizes on the time nature of the data.
- Use a recurrent neural network to build a time series model.

The initial overall accuracy of the Random Forest model is 74%. With an additional allocation of time and resources, these models could absolutely reach an accuracy above 80%. This is especially true when the cardinality of drought scores is incorporated into the models and ever more importantly the information contained within the timeseries. Additionally, a recurrent neural network may be able to leverage deep learning available within such a large dataset. Given the changing climate and the inherent integration of economies throughout the present-day world, understanding and accurately predicting drought is an important first step in adapting to the current changing conditions of our environment and maintaining a viable global economy.  Being able to predict drought from simple variables and not overly complex models, would allow them to be applied worldwide.