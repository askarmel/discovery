# Discovery
add interpretability to clustering 

## Context
Segmentation through clustering with limited number of features, for example Recency-Frequency-Monetary marketing segmentation or Memory-CPU-GPU consumption on production monitoring

## Objectives
Enable human interpretation / extrapolation of the clusters by adding much more features (demographics, online / offline behaviours, transactional data, etc.) and identifying what features matter the most and how.

## Impact
Understand why given groups of people are similar (share the same cluster); Help to build deep dive profiles and patterns

## Approach

### Step 1: Clustering
Train and tune a clustering algorithm based on a minimal set of features, typically metrics that marketing follows (RFM)

### Step 2: Classifier
Build and online train a classifier where the input data is the initial dataset augemented with demographics, behavioural, transactional data. 
//
The new training dataset doesn't include the marketing metrics.
//
The classifier labels are the cluster numbers (hence it needs to be trained online)
//
Tuning the classifier (typically Boosting trees) can be done through HyperOpt with Spark / MongoDB for better scalability.

### Step 3: Add explainability to the classifier
Implement SHAP on top of the classifier results in order to obtain the most important features
//
Identify not only the features but also the values and the correlations that matter

### Step 4 (optional): Build an optimized classifier
Use only key features in the new classifier and tune it with hyperopt.
//
This step matters if the number of demographics, behavioural, transctional features is significatively bigger than the final number of important features.
This may allow faster inference at scale

### Step 5: Use the classifier to project marketing segments on potential users
As the classifier doesn't need marketing metrics as input data, it can infer marketing segment for potential users (as long as the demographics, behavioural and transactionnal data required for the classifier is available)

