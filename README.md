# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
This dataset holds information from marketing campaigns initiated by a Portuguese marketing institution, detail coming in from phone calls. We seek to predict through classification whether or not the client would subscribe to a bank term deposit

LogisticRegression performed adequately with an accuracy of 91.3%, with AutoML's results (through a VotingEnsemble) being only marginally better (91.5%)

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**
Data is fed in with feature engineering completed to encode non-numerical features. After splitting into testing and training sets, the LogisticRegression classifier is used to fit and train with hyperparameter tuning done by HyperdriveConfig.
See diagram of model architecture pipeline.

**What are the benefits of the parameter sampler you chose?**
The RandomParameter sampler is more flexible in permitting continuous rather than just 'choice' or discrete selections of hyperparameter values. In my evaluation, I ended up using 'choice' to iterate through ranges of C and max iterations any use of a 'continuous' or 'uniform' sampler is enabled by RandomParameter.

**What are the benefits of the early stopping policy you chose?**
BanditPolicy is more geared towards achieving absolute performance through use of a slack factor unlike Truncation Policies or Median Stopping policies, which are focused on achieving good performance relative to other runs 

## AutoML
AutoML selected a VotingEnsemble with hard voting, no penalty, and weights ranging from 0.33 to 0.66. These weights are used to calibrate class occurrences before making a final prediction.
See diagram of model architecture pipeline.

## Pipeline comparison
LogisticRegression performed adequately with an accuracy of 91.3%, with AutoML's results (through a VotingEnsemble) being only marginally better (91.5%)

## Future work
Opportunities to improve modeling include: 
- ordinal encoding in place of one-hot encoding for variables like housing and education which may have a natural order when predicting policy subscriptions
- adding the solver_type to assess 'sag' in its performance for prediction
- Try BayesianParameter search
