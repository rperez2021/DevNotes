---
id: z64ad3krycpz76064gvbscz
title: Model Evaluation
desc: ''
updated: 1649136450032
created: 1649136450032
---
## Model Eval Metrics

### For Clustering Models

- **Average Distance to Other Center**: This indicates how close, on average, each point in the cluster is to the centroids of all other clusters.
- **Average Distance to Cluster Center**: This indicates how close, on average, each point in the cluster is to the centroid of the cluster.
- **Number of Points**: The number of points assigned to the cluster.
- **Maximal Distance to Cluster Center**: The maximum of the distances between each point and the centroid of that point’s cluster. If this number is high, the cluster may be widely dispersed. This statistic in combination with the Average Distance to Cluster Center helps you determine the cluster’s spread.

### For Classification Models

- **Accuracy**: The ratio of correct predictions (true positives + true negatives) to the total number of predictions. In other words, what proportion of diabetes predictions did the model get right?
- **Precision**: The fraction of positive cases correctly identified (the number of true positives divided by the number of true positives plus false positives). In other words, out of all the patients that the model predicted as having diabetes, how many are actually diabetic?
- **Recall**: The fraction of the cases classified as positive that are actually positive (the number of true positives divided by the number of true positives plus false negatives). In other words, out of all the patients who actually have diabetes, how many did the model identify?
- **F1 Score**: An overall metric that essentially combines precision and recall.
- **AUC**:

Of these metric, accuracy is the most intuitive. However, you need to be careful about using simple accuracy as a measurement of how well a model works. Suppose that only 3% of the population is diabetic. You could create a model that always predicts 0 and it would be 97% accurate - just not very useful! For this reason, most data scientists use other metrics like precision and recall to assess classification model performance.

Above the list of metrics, note that there's a Threshold slider. Remember that what a classification model predicts is the probability for each possible class. In the case of this binary classification model, the predicted probability for a positive (that is, diabetic) prediction is a value between 0 and 1. By default, a predicted probability for diabetes including or above 0.5 results in a class prediction of 1, while a prediction below this threshold means that there's a greater probability of the patient not having diabetes (remember that the probabilities for all classes add up to 1), so the predicted class would be 0. Try moving the threshold slider and observe the effect on the confusion matrix. If you move it all the way to the left (0), the Recall metric becomes 1, and if you move it all the way to the right (1), the Recall metric becomes 0.

Look above the Threshold slider at the ROC curve (ROC stands for receiver operating characteristic, but most data scientists just call it a ROC curve). Another term for recall is True positive rate, and it has a corresponding metric named False positive rate, which measures the number of negative cases incorrectly identified as positive compared the number of actual negative cases. Plotting these metrics against each other for every possible threshold value between 0 and 1 results in a curve. In an ideal model, the curve would go all the way up the left side and across the top, so that it covers the full area of the chart. The larger the area under the curve (which can be any value from 0 to 1), the better the model is performing - this is the AUC metric listed with the other metrics below. To get an idea of how this area represents the performance of the model, imagine a straight diagonal line from the bottom left to the top right of the ROC chart. This represents the expected performance if you just guessed or flipped a coin for each patient - you could expect to get around half of them right, and half of them wrong, so the area under the diagonal line represents an AUC of 0.5. If the AUC for your model is higher than this for a binary classification model, then the model performs better than a random guess.
