
1. # Aim of project 

The data consists of 2 splits *train\_data.csv* and *test\_data.csv.* There are numeric observations labelled either -1 or +1. Labels for the training data are located in *train\_labels.csv*. 

The aim of the project is to predict labels for the testing data.

Desired output:

- Save predictions in *test\_labels.csv*,
- Prepare a report (saved as *report.md*)with the explanations on how you came up with the solution. What obstacles you faced and how did you solve them. Add also information about data quality and so on.

1. # ` `Exploratory Data Analysis and Data Quality


To familiarize with the provided data, a basic check of data quality was performed. “Train\_data” is a dataset containing 10 000 columns and 3750 rows. No duplicated and null data was identified within the dataset. As clearly displayed with the use of the “describe” function, the data is highly varied. 

Secondly, the same analysis was performed for the “Test\_Data” and all the conclusions were almost identical as in the previously analyzed “Train\_Data”. What is most important, both datasets are characterized by the same dimension (number of columns), so no additional tweaks on the data are needed on this point. 

As visualized on the boxplot, the data is unbalanced. The minority

class is almost 10 times smaller than the majority. This problem will need to

be solved in the next steps of the project. 

Subsequently, the “Train\_data” was split with the use of the “test\_train\_split”

function, then standardized and reduced to two dimensions to help visualize the

data. The generated scatterplot shows no correlation between the points. Following, the TSNE plot was generated to display the similarities in the data. The

output was not sufficient to designate the clusters, confirming the previously

stated belief of dealing with unbalanced data. All additional EDA charts

were visualized with the use of the “pandas\_profilling” function.

**Obstacles:** 

- The visualization of the data was the biggest obstacle of the EDA part of the project. The attempts to visualize the raw or split data resulted in either exceeding the possibilities of the used computer or unreadable charts. The PCA was introduced in order to reduce the dimensions and create more friendly input for the data visualization.
1. # ` `Upsampling

We used Upsampling to balance the dataset. The dataset shows inadequate results as many results are close to each other and smaller results can be missed. Initially, we thought the selected method would produce better results, yet in reality, it was only worse. The balanced dataset did not give us expected results. The Upsampling method did not outcome in the balance we wanted. This may be due to the diversity of the dataset, which proved to be too different for the method indicated.

**Obstacles:** 

- For our dataset, the Upsampling method did not work... We decided to check the dataset without using the balancing method and we obtained better results when compared to the Upsampling method.


1. # ` `Grid Search
The method used for scanning the dataset to configure optimal parameters for a given model was GridSearch. It is simply a method to calculate the best parameters to use for any given model. When the dataset is too large this method can be time-consuming, but for our project, GridSearch was very good. It can build a model on each parameter combination and then store a model for each of them. Did it cost us a lot of time? A bit, but we had some trouble understanding the operation of GridSearch itself, which made the task difficult at first. However, over time we realized that our mistake was not understanding the model itself, but the data we were working on. Finally, we decided to test our model for two datasets. For the balanced one after the Upsampling method and the dataset obtained directly after EDA (standardized X and y after train test split). The result surprised us because we thought that the balanced dataset would turn out better. As it turned out later it was completely different.

**Obstacles:** 

- Understanding which dataset we need to use. After consultations, we decided to test a few solutions and choose the best two.
- We also had a problem with the pipeline, but after several attempts and reading some documentation, we found the optimal solution.

1. # ` `Predict labels

The next step in our project is to select the appropriate model for the “Test\_Data” label prediction. Based on the Grid Search described in the previous paragraph, the various fitting to the SVC model was conducted. Firstly, the SVC model was fitted with standardized data. As visualized in the confusion matrix the model was unable to identify the minority class, resulting in 0% accuracy for the value “-1”. Precision and other elements of the classification report couldn’t be calculated.

The next attempt was to indicate the best model parameters calculated with the use of Grid Search. Nevertheless, the parameters did not impact the confusion matrix output. 

As mentioned in the EDA analysis, the dataset is highly unbalanced, so the attempt of upsampling the minority class was performed. However, the results were not sufficient to consider valid, as they revolved around the 50% of proper label identification accuracy. As the third attempt of using the SVC model did not succeed, the new model was picked. 

K-Nearest Neighbours model was picked based on the chart provided with the scikit learn library (https://scikit-learn.org/stable/tutorial/machine\_learning\_map/index.html). The number of neighbors was picked based on the Number of neighbours and score chart. As the SVC Upsampled data was able to identify the minority class labels, the first attempt with the KNN model was used with upsampled values. Yet, the outcome could not be considered as satisfactory. 

Last but not least, the KNN model was based on the data from the original test\_train\_split. The minority class was predicted with 0.82% precision and the majority class with 0.97%. The confusion matrix showed only 46 incorrectly identified labels and was characterized with the highest outcome from all models. The model was considered sufficient and picked as the final model used to predict labels for “Test\_data”.

**Obstacles:** 

- Not predicted minority class was the biggest obstacle in Predict Labels part of the project. The data was too unbalanced, to perform the calculations based on the basic data. The attempt to add “class\_weight = ‘balanced’ “ parameter did not succeed. That is why we decided to create an upsampled dataset, yet as presented it was not effective either.
- We faced the problem of picking the next estimator for our data, however, we followed the suggestion in the Scikit Learn Cheat Sheet chart and succeeded. 
- Additionally, model visualization with the use of a confusion matrix and plotting the charts increased the understanding of the analyzed topic and led to conclusions. The attempt to understand the data without visualization was hindered. 

1. # ` `Summary
There is a possibility that moving forward with the “Choosing the right estimator” chart would probably bring even more positive results when compared to the selected final one. It would be beneficial to discover those options during further self-development. The biggest obstacle of the whole process would be to deal with enormous and unbalanced input data. It is said that almost 80% of the whole Machine Learning process is to prepare data. We believe that this analysis supports this statement. The analysis allows for various and almost unlimited path selection. Dealing with this project allowed us to change the perspective while looking at data and treating it as a whole, rather than individual columns and rows.
