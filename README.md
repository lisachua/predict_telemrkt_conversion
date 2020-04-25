## msds699_sal
Shane Buchanan |
Al A Latif |
Lisa Chua 
### Overview:
The goal of this project was to find a way to predict whether a prospect would sign up for a term deposit after going through a telephone conversation with the bank. We used machine learning algortitms and tools to get the best prediction for this binary classsification problem. Our data comes from the [UCI machine learning repository](https://archive.ics.uci.edu/ml/datasets/bank+marketing "UCI machine learning repository"). 

### Challenges:
1. Imbalanced Data - Only 12% of the data were successful conversions by the bank. Due to this fact we needed to upsample the data use techniques like SMOTE. This also impacted our model evalutation metric, since accuracy is a poor criterion for imbalanced data sets. 
2. Some Strongly Correlated Features - Around a quarter of the features were economic indicators, which were correlated so we needed to be careful when training and testing on a linear model. 

### Feature Processing and Importance:
1. We one-hot encoded our categorical variables, imputing missing data by taking the mode and creating a separate variable to flag the record as “unknown”.  We also excluded the duration variable since it was only recorded post-call. Prospects that had not been called and therefore not converted would have a missing duration. Therefore including duration would be a form of data leakage.
2. Since our domain is business intelligence for improving tele-marketing strategy, we focused heavily on feature importance to understand which factors have a bigger impact on conversion. We used RFPimp’s implementation for feature importance because we have a few codependent features and this allows us to consider multiple features together. The results show that most importance features are all economic indicators: national employment, consumer confidence index and Eurobor.

### Model Selection:
As mentioned above we needed a different evaluation metric so we choose Weighted F1-score since it gives us a good balance between precision and recall. However we list the accuracy scores for the two best models just as a comparison for other groups. 
- Linear Model - F1=.87, Accuracy=.89, Variance(n=100)=2.3e-5
- Random Forest - F1=.88, Accuracy=.90, Variance(n=100)=1.8e-5
The random forest gave us the best model based on our F1 metric so that is the final model we choose.

### Business Insight:
One of the key insights we learned from working with this data is that it is better to change the decision threshold for the random forest. Since our business goal is to be able to hand over a list of prospects most likely to sign up for a deposit, it is better to have a higher recall at the expense of the False Positive rate. This allows us to capture more people who may potentially convert in our filtering. Since marketing campaigns have always had a very low conversion rate, taking on more false positives and doing a few more calls is fine if it means bringing in more money.

### Takeaways:
Feature importance found that most of our variables are not predictive of conversion. When we compared our best f1 score to benchmarks and high scores on Kaggle, we hit a ceiling of 0.88, which may further indicate that there are missing features. Another limitation is that naïve and SMOTE upsampling to address our imbalanced data problem did not improve our model metrics. Some potential next steps would be to rerun models after feature selection and collect more economic features.

