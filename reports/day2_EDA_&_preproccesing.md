# Day 2 - EDA and Data Visualisation

## David - data examination and explanation

Today I spent some time digging deeper into the dataset and generating a bunch of charts to get a better feel for what’s going on. I’ll walk through each graph and share what I learned.

### Histograms & Boxplots

I started by plotting histograms for all the numerical features. Most features look pretty well distributed, but there are some outliers here and there. Boxplots helped confirm this—especially for grammar errors and burstiness. Most texts have low grammar errors, which is good news for training since AI text is getting better at sounding human.

### Label Distribution

I checked the label distribution and was happy to see it’s balanced between AI and Human. That means our models won’t be biased toward one class, which is always a relief.

### Content Type Distribution

Next up was the content type bar plot. The different types are pretty evenly spread out, so no single type will dominate the model’s decisions. That should help keep things fair.

### Correlation Heatmap

I ran a correlation heatmap to see how the features relate to each other and to the label. Turns out, most features don’t have a strong correlation with the label, but word count, character count, and sentence count are tightly linked to each other. I’m keeping all features for now since the set is small.

### Feature Relationships (Pairplots)

Pairplots were super useful. I picked out key features like word count, sentence count, lexical diversity, flesch reading ease, and burstiness. The clusters are a bit messy, but academic papers really stand out—they have high word and sentence counts, high burstiness, and strong lexical diversity. Product reviews are on the other end, with much lower counts.

### More Insights

Lexical diversity is high for most texts, which means there’s a rich vocabulary in play. Flesch reading ease scores hover around 50, so the texts aren’t too easy or too hard to read. Sentiment scores are pretty uniform, which should help avoid bias. Grammar errors and passive voice ratios don’t show any clear trends—there’s a lot of entropy in the data.

### PCA Visualisation

I wrapped up with a PCA plot. Projecting everything onto two principal components, I saw that it’s basically impossible to separate artificial from human text using just the current features. This matches what the correlation matrix hinted at. Clearly, I’ll need to dig deeper into preprocessing and maybe engineer some new features if I want to boost model performance.

---

Overall, the dataset is clean, balanced, and ready for modeling. There’s no obvious silver bullet feature for distinguishing AI from Human content, but academic papers do stand out. Next up: more advanced text features, embeddings, and prepping for ML and DL