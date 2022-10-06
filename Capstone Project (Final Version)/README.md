

General Assembly Capstone Project: Drowsiness Detection

Author: Khoo Qi Xiang (DSI31)


This project comprises 3 notebooks:

Part 1 - Deep Learning

Part 2 - Live Demo


## Introduction


One of the world's sleepiest nations is Singapore.
In a recent poll, 43 cities were analyzed, and Singapore came out on top for having the least amount of sleep. 
Lack of sleep or low quality sleep are unacceptable. Whatever the source, a lack of sleep over an extended period of time will be detrimental to your overall wellbeing, productivity, and safety.

If you've ever driven, it's likely that you've dozed off at least once. Although we don't like to admit it, there is a serious problem that must be fixed because it has detrimental impacts. One in four car accidents are the result of drowsy driving, and one in twenty-five adult drivers admit to falling asleep at the wheel in the 30 days prior. The fact that tired driving involves more than just falling asleep behind the wheel is the most alarming element.

## Problem Statement
To develop a prototype drowsiness detection system that can correctly and instantly track whether a driver is drowsy or not based on some of the facial features. 
As attempting to identify signs of drowsiness early on will help reduce the incidence of accidents if the driver is informed of them.


## Dataset 
First, an understanding of the available data should be acquired. UTA already provides some insights in this regard, so that a detailed explorative data analysis can be dispensed with.

Background of the data: 
The UTA dataset consists of 180 RGB videos of 60 unique participants. 
Each video is around 10 minutes long, and is labeled as belonging to one of three classes: alert (labeled as 0), low vigilant (labeled as 5) and drowsy (labeled as 10). 
The labels were provided by the participants themselves, based on their predominant state while recording each video. This type of labeling takes into account and emphasizes the transition from alertness to drowsiness. 
Each set of videos was recorded by a personal cell phone or web camera resulting in various video resolutions and qualities which is in fact a data quality problem. The 60 subjects were randomly divided into five folds of 12 participants, for the purpose of cross validation.

The final Dataset that we are using for the deep learning can be found:
https://github.com/hackenjoe/Advanced_Drowsiness_Detection/tree/main/data_drowsiness/prepared

totalwithmaininfo.csv -- this data contains all of the data for your model. Its data includes every computation made and compilation made from the video frames.


## Predefined Functions

2.1 Eye Aspect Ratio (EAR):
The EAR, as its name suggests, is the proportion of eye length to eye width. Two separate vertical lines are averaged across the eyes to determine their length.

According to our theory, drowsy people's eyes will probably get smaller and will blink more frequently. According to this theory, we anticipated that if an individual's eye aspect ratio decreased over time—that is, if their eyes began to close more or they were blinking more quickly—our model would classify them as being drowsy.

2.2 Mouth Aspect Ratio (MAR):
The MAR, which is computationally comparable to the EAR, measures the proportion of the mouth's length to width. According to our theory, when someone is tired, they are more likely to yawn and lose control of their mouth, which causes their MAR to be greater than usual.

2.3 Pupil Circularity (PUC):
PUC is a measure complementary to EAR, but it places a greater emphasis on the pupil instead of the entire eye. For instance, because of the squared element in the denominator, a person with their eyes only partially open or almost closed will have a significantly lower pupil circularity score than a person with their eyes fully open. 
Similar to the EAR, it was anticipated that drowsiness would cause a person's pupil circularity to decrease.

2.4 Mouth aspect ratio over Eye aspect ratio (MOE):
Finally, we decided to add MOE as another feature. MOE is simply the ratio of the MAR to the EAR.

Adopting this feature has the benefit that EAR and MAR are expected to move in opposite directions if the person's state changes. Because MOE will both detect the minute changes in EAR and MAR and magnify the changes when the denominator and numerator move in the opposite directions, it will be more responsive to these changes than EAR and MAR. 
We hypothesized that because the MOE employs MAR as the numerator and EAR as the denominator, it will increase as a person gets drowsy.








## Model used:
Models/Classifiers:
- Naive Bayes 
- Logistic Regression
- Decision Tree Classifier
- Random Forests Classifier
- XG Boost
- K-Nearest Neighbors (KNN)
- Multi-layer Perceptron classifier (MLP)
- Convolutional Neural Network (CNN)

Metrics:
- F1 score , Accuracy

## Summary of the Five models:

|Model|Accuracy|F1 Score|ROC|
|---|---|---|---|
|Logistic Regression|0.888|0.904|0.933|
|Naive Bayes|0.865|0.886|0.930|
|KNN|0.877|0.892|0.936|
|MLP|0.881|0.895|0.941|
|Decision Tree|0.900|0.913|0.938|
|Random Forest|0.890|0.902|0.959|
|CNN|0.879|0.894|0.50|
|XGBoost|0.940|0.948|0.975|


Our primary metric will be recall since correctly predicting the positive class (a sleeping driver) is more crucial to us than correctly predicting the negative class (an awake driver) (sensitivity). The model incorrectly anticipates fewer sleeping drivers to be awake the greater the recall (false negatives). The main issue here is that our negative class outnumbers our positive class by a large margin. Due to this, it is preferable to utilize the F1 score or Precision-Recall AUC score because they also account for the instances when we mistakenly believe a driver to be asleep when they are actually awake (precision). If not, our model will always assume that we are asleep and will be useless. We did not use image augmentation as a solution for coping with unbalanced image data.

The key of the final model decision is down to the primary metric that we choose to focus. Our primary metric will be recall since correctly guessing the positive class (a sleeping driver) is more crucial to us than correctly predicting the negative class (an awake driver) (sensitivity). The higher the recall, the smaller amount of sleeping drivers the model mistakenly predicts are awake (false negatives). We also utilize F1 scores, which also account for the instances when we assume a driver is asleep but is actually awake (precision).If not, our model will always assume that we are asleep and will be useless.

Logistic Regression and Naive Bayes although they yield good result they are basic models. We rule out random forest, decision tree and xg boost since we think they might be overfitting. Because the present data videos only show people sitting down in a generalized environment. This is could be the cause of why models like random forest, xgb boost, and decision tree are showing very good performance and could be deem as overfitting. But thanks to that finding, we can see that we would need more different video data. (Next slide):

We then chose to use MLP as the final model based on the best ROC and reasonable recall rate which we re-emphasis that we want to be able to predict the positive class( a sleepy user ) than correctly predicting the negative class (an awake user).


The final model selected for final evaluation were:

|Model|Accuracy|F1 Score|ROC|
|---|---|---|---|
|MLP|0.881|0.895|0.941|


Our primary metric will be recall since correctly guessing the positive class (a sleeping driver) is more crucial to us than correctly predicting the negative class (an awake driver) (sensitivity). The algorithm incorrectly anticipates fewer sleeping drivers to be awake the greater the recall (false negatives).

The main issue here is that our negative class outnumbers our positive class by a large margin. Due to this, it is preferable to utilize the F1 score or Precision-Recall AUC score because they also account for the instances when we mistakenly believe a driver to be asleep when they are actually awake (precision). If not, our model will always assume that we are asleep and will be useless.


## Conclusion
Through the final model, we are able to conclude :
- Everyone's baseline for the eye and mouth aspect ratios is different which was why normalization was crucial to our performance.
- When performing tasks, less complicated models can be just as effective as more complex ones.But ultimately, it is better to employ the more sophisticated model with a lower false-negative rate than a simpler model.
- Flexibility of the system. Finally, the simplicity of the system allows us to explore more models. The model’s output appears useful, and applying it to a device appears feasible. This system might be applied in real-world settings and possibly save lives but of course with a few additional adjustments and export to a different device.

## Suggestion for further enhancement:
- For the models, more diverse images taken in a range of seating arrangements and lighting conditions would have been desirable.
- How the false-negative rate for MLP and other straightforward models can be reduced.
- Incorporate behavior feature like sudden head movements, hand motions, head tilting (posture), or even monitoring eye movements, these are new, distinct signs of tiredness.