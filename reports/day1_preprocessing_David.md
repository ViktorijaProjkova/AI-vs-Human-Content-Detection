# Day 1 report - David

On day 1 of preprocessing, I used my time to analyze the dataset and look through what Viki had already done. I also thought about what plan we should devise and what routes we should take in the following days while doing EDA and preprocessing, in order to get the maximum value from the data we downloaded from Kaggle.

## Data visualization

We've noticed that the data isn't that large and it is a single file containing 1,367 rows and 17 columns (features). Therefore, analyzing it wouldn't be a difficult task. The low amount of data, as well as the nature of the data itself (most columns contain numerical values), aids in the preservation of the original values of the dataset. This means that encoding wouldn be an issue and the data itself would be applicable for different AI models without much tampering. 

Viki has already dropped all null values in the dataset, with which i agree that is the correct course of action because of the low quantities of null values in each column rendering them inafective when missing from the dataset while training and testing models. I just made a minor adjustment to the code. 

Viki suggested we should do a data visualisation before scalling the data or doing any kind of encoding, with which i agree to the fullest.

## Suggestions for further work

I do have some notes though. Perhaps it would be better if the project is devided in different notebooks: one for the data visualisation and EDA, and two others for ML and DL both simulating a pipeline with different approaches for data preproccessing and model training and testing.

I already reorganised the workspace and have strated to do EDA, but it has some work to do, so i will continue tommorow...