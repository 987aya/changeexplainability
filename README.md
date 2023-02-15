# Explainability of change
A framework for explaining changes in data stream classification
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

# Definition

Streaming Data: A continuous source of data. Example: Twitter data, stock data, weather data.

Data Space: All possible values for a set of data samples.
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

Learning Model: A machine learning model is a program that can find patterns or make decisions from a previously unseen dataset
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

Data Distribution: A collection of data samples that are mapped to a hyper space.
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

Concept Drift: A change in the underlying data distribution that affect the performance of the current learning model.

# Interpreting Impact of Change on Existing Model
SVM classify data points by separating the two classes of data using a linear function in hyperspace. Ideally, on each side of the linear function should contain only one data class. Furthermore, there should be little data points that fall between the two support vectors, such that the classification confidence of the SVM model is high. When changes occur in a data stream, look for data distribution change that either (a) increase number of data points on the wrong side of the classification model or (b) increase number of data points within the support margin of the SVM. 
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

Above Figure demonstrated a case where the visualization explains how concept drift impact performance of learning models. Initial in “chunk 6”, the model before concept drift was able to separate the brown and blue classes of data well. The majority of data instances from either class fall on their respective side of the SVM class boundary (solid line). Although the classification confidence is low, as many data points fall between the support vector margin (dotted line). In “chunk 11”, changes in data distribution is clearly seen as the majority of data points from both classes now reside on the same side of the SVM classification boundary. This means that most of the blue class and brown class instances will be classified with the same class label. Thus, one can conclude that the change in data distribution severely affect the performance of the current model, and a concept drift detection is justified.

# Interpreting Updated Model Trained Using Data After Concept Drift
The increase performance of the updated model after concept drift can be shown through the rebalancing of data points on each side of the classification boundary.   In this interpretation, look for SVM boundary once again being able to split the two classes of data well, compared to previous model in the same chunk of data. Ideally, the number of data points between the support vector margin should also decrease, showing a increase in classification confidence.
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

 Above Figure illustrates the difference of model performance when concept drift is detected in “chunk 11”, which is a continuation of Figure 5. As mentioned earlier, the outdated model can no longer separated the blue and brown data points well, as shown in the visualization on the left. The updated model, shown in the visualization on the right, have different support vectors and class boundary that conform to the shape of the data distribution much better. In this new model, the blue samples and brown samples are once again rebalanced on each side of the classification boundary. This shows clear improvement of classification performance, even though classification confidence is low, as many data points are within the support vector margin. 
 
# Interpreting Cases When No Concept Drift Detected
Data distribution changes don’t always result in an need for updating learning model. In such case, concept drift will not be detected because the change does not affect the performance of the current learning model. This occurs when the change doesn’t result in data samples of either class labels appearing on the wrong side of the SVM boundary. 
<p align="center">
  <img src="https://en.wikipedia.org/wiki/Iris_flower_data_set#/media/File:Iris_dataset_scatterplot.svg" width="800" />
</p>

Above Figure shows two chunks of data with distribution change, but no concept drift is detected. The contour shape of both the brown and blue data points changed between “chunk 2” and “chunk 3”. However, the existing model still separates the majority of the two classes on their own respective side of the class boundary. Although some misclassification occurred in both “chunk 2” and “chunk 3”, there is no significant change in how many data points are misclassified. Furthermore, the classification confidence, shown as non-support data points in support vector margin, remains mostly unchanged. Thus, one can conclude that the change does not warrant training of a new updated model. 

