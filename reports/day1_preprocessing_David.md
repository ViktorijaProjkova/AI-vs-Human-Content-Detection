# Day 1 report - David

On day 1 of preprocessing, I used my time to analyze the dataset and look through what Viki had already done. I also thought about what plan we should devise and what routes we should take in the following days while doing EDA and preprocessing, in order to get the maximum value from the data we downloaded from Kaggle.

## Data visualization

We've noticed that the data isn't that large and it is a single file containing 1,367 rows and 17 columns (features). Therefore, analyzing it wouldn't be a difficult task. The low amount of data, as well as the nature of the data itself (most columns contain numerical values), aids in the preservation of the original values of the dataset. This means that encoding wouldn be an issue and the data itself would be applicable for different AI models without much tampering. 

Viki has already dropped all null values in the dataset, with which i agree that is the correct course of action because of the low quantities of null values in each column rendering them inafective when missing from the dataset while training and testing models. I just made a minor adjustment to the code. 

Viki suggested we should do a data visualisation before scalling the data or doing any kind of encoding, with which i agree to the fullest.

## Suggestions for further work

I do have some notes though. Perhaps it would be better if the project is devided in different notebooks: one for the data visualisation and EDA, and two others for ML and DL both simulating a pipeline with different approaches for data preproccessing and model training and testing.

I already reorganised the workspace and have strated to do EDA, but it has some work to do, so i will continue tommorow...

## Viki report - preprocessing (ML)

I focused on preparing the dataset so that it can be directly used for model training. My main goal was to transform the raw text column into numerical features, combine them with the existing numerical metrics, and then split the data into training and testing sets in a clean and reproducible way.

# Text preprocessing

The core of the dataset is the text_content column, which contains human or AI written text. Since models cannot work directly with strings, I applied TF-IDF vectorization. This approach converts words and bigrams into numbers, giving higher weights to terms that are more informative and reducing the influence of extremely common words. I set the vectorizer to include unigrams and bigrams, with min_df=2, max_df=0.9, and a vocabulary limit of 10,000 tokens. The reasoning here is that rare words do not add much value, and overly frequent words behave like noise. Bigrams are useful because they capture stylistic signals such as “in conclusion” or “as a result,” which might help distinguish AI from human writing.

The TF-IDF output is a sparse matrix that works very well with linear classifiers such as Logistic Regression or Linear SVM, which are both strong baselines for text classification tasks.

# Numerical features

Apart from the raw text, the dataset contains several numerical metrics such as word count, character count, lexical diversity, grammar errors, and others. I standardized these features using StandardScaler to ensure they are on the same scale. This prevents the model from being biased toward features with larger ranges.

Additionally, if categorical columns (like content type) were already one hot encoded, I passed them through the pipeline without changes. This way we can keep them for potential later experiments without breaking the transformation process.

# Train/test split and saving

After preprocessing, I split the dataset into 80% training (943 rows) and 20% testing (236 rows), making sure the distribution of the label (0 = human, 1 = AI) was preserved with stratified sampling. The final feature space contained around 9,165 columns, combining TF-IDF tokens and the numeric features.

Finally, I saved the pipeline itself together with X_train, X_test, y_train, and y_test. This ensures we can reuse the same transformation consistently when training different models or evaluating new data.


## Viki report - preprocessing (DL)

I worked on preparing the dataset for deep learning models. Unlike the machine learning pipeline where we used TF-IDF, for deep learning I created separate inputs for the text, numeric features, and the encoded categorical features. The goal was to have a clean dataset ready for multi input neural networks.

# Text preprocessing

The main feature of the dataset is the text_content column. Deep learning models cannot read raw text, so I used the Tokenizer from Keras to convert words into integer indices. I fit the tokenizer only on the training data to avoid leakage. After that, I transformed all texts into sequences of word indices and used padding to make sure they all had the same length of 300 tokens. This way, every text is represented as a numeric sequence of equal size, ready to be fed into an embedding layer in Keras.

# Numeric features

The dataset also contains several numeric features that describe the text, such as word count, lexical diversity, readability indexes, grammar errors, and sentiment score. I selected these columns and applied StandardScaler to them, but again only fitting on the training data. This step ensures that all numeric values are standardized to the same scale, which makes it easier for the model to learn patterns without being biased by large value ranges.

# Encoded categorical features

We also had a set of one-hot encoded columns representing the type of text. These columns were already in numeric [0,1] format, so I simply selected them as a separate input. This allows the deep learning model to also consider the type of the text as an additional feature alongside the raw text and numeric metrics.

# Train/test split

I split the dataset into 80% training and 20% testing using stratified sampling to preserve the balance between AI and human texts. Importantly, I split the raw features first, and then applied tokenization and scaling only on the training subset. This avoids information leakage from the test set. After the split, I ended up with three aligned sets of inputs: X_text (padded sequences), X_num (scaled numeric features), and X_encoded (one-hot encoded categories), together with the target labels y.

The visualization you prepared looks excellent, and the folder organization makes the workflow much clearer. I think it already gives a good overview of the data, and I’ll leave it to you if you want to add additional plots (EDA). From my side, the preprocessing is now in place and ready for model training.