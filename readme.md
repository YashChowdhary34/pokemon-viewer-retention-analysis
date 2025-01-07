# What makes a Pokémon popular amongst viewers?

## Introduction

To increase viewer retention we need to know the factors that contribute the most to a Pokémon's popularity, because **Pokémon popularity and viewer retention are directly proportional**.

If we somehow figure out the factors that contribute the most we could work on them for other Pokémon's as well and get better viewer retention, **increasing overall revenue**.

In this project we'll dive deep into analyzing and figuring out those factors. Also, we'll figure out **what makes a Pokémon legendary** as that's a big deal amongst Pokémon fanbase.

---

## Table of Contents

- [What factors that contribute the most to a Pokémon's popularity?](#What-are-the-Factors-that-Contribute-the-most-to-a-Pokémon's-Popularity-amongst-Viewers?)
  - [Variable Exploration](#Variable-Exploration)
  - [Handling Outliers](#Handling-Outliers)
  - [Create Train/Test Split](#Create-Train/Test-Split)
  - [Fitting Model (randomForest)](#Fitting-Model)
  - [Analysing Model Performance](#Analysing-Model-Performance)
  - [Analysing Feature Importance](#Analysing-Feature-Importance)
- [What makes a Pokémon legendary?](#What-Makes-a-Pokémon-Legendary?)
  - [Variable Exploration](#Variable-Exploration)
  - [Create Train/Test Split](#Create-a-training/test-split)
  - [Fitting Decision Tree](#Fit-a-decision-tree)
  - [Fitting Random Forest](#Fit-a-random-forest)
  - [Assess Model Fit](#Assess-model-fit)
  - [Analysing Feature Importance](#Analyze-variable-importance)
- [Answering Business Problems](#Answering-Business-Problems)
- [Conclusion](#Conclusion)

---

### What are the Factors that Contribute the most to a Pokémon's Popularity amongst Viewers?

To find the factors that contribute the most we need to look at the individual features of each Pokémon. There must be certain features or type that people find more desirable and if we successfully in finding those features we can predict and increase viewer retention by using those particular Pokémon's that have those desirable features in them, also we could tweak features for other Pokémon's in the feature.

This is a list of all the features that we'll be looking at while figuring out the most important ones.

- height_m
- weight_kg
- attack
- defense
- s_attack
- s_defense
- type
- generation
- capture_rate
- pokedex_number
- legendary status
- hp
- speed
- percentage_male

These factors should be enough for our use case as these describe all the important features of a given Pokémon.

#### Variable Exploration

##### 1. Which types have the most number of Pokémon's?

Looking at the distribution of types along with their legendary status we mainly notice 2 things. First - water type has the highest number of Pokémon's in it followed by normal and grass, Second - there are a bunch of types that don't have any legendary Pokémon's in them eg. water, bug, grass, poison.

<categorical vairable exploration>

##### 2. Now we should Analyse the Spread of all the different Features by looking at a Density Plot

We can see that in the case of features like attack and speed there are larger number of Pokémon's that are average whereas features like hp, height, weight show that larger number of Pokémon's are shorter, lighter and have low hp.

<Density histogram>

##### 3. How are the features correlated to Popularity Score?

Here we can explore the relationship between popularity score and other features to identify trends and correlations.
If we take a look at the graph it seems like sp_defense, hp, sp_attack have a significant impact on the popularity score wherease speed and attack have a moderate positive correlation.

<scatter plot bivariate analysis>

##### 4. Which Pokémon types are generally more popular?

We can clearly see that people tend to like dragon type more compared to all the other types. As we have the box-plot here we can also take a look at the outliers.

<boxplot>

#### Handling Outliers

There are some outliers that we need to handle so that we get a more accurate prediction.

**Identifying Outliers**

**Handling Outliers**

#### Create Train/Test Split

We have now explored all of the predictor variables we will use to explain what makes a Pokémon popular. Before fitting our model, we will split the dataset into a training set and a test set. This will allow us to test the model on unseen data.

```r
  train_index <- createDataPartition(pokemon$popularity_score, p = 0.8, list = FALSE)
  train_data <- pokemon[train_index, ]
  test_data <- pokemon[-train_index, ]
```

#### Fitting Model

We'll fit a random forest – an ensemble method that averages over several decision trees all at once. It provides a robust measure of feature importance, including non-linear interactions.

```r
  rf_model <- randomForest(popularity_score ~ ., data = train_data, importance = TRUE, ntree = 500)
```

#### Analysing Model Performance

Let's take a look at the MSE score to assess our model's performance on unseen data. Note that lower score is better.

**Mean Squared Error (Random Forest): 7.129137**

#### Analysing Feature Importance

##### Most important predictors for Pokémon Popularity

Pokedex Number seems to be the hightest predicter as Pokémon with lower Pokedex numbers were among the first to be discovered within the lore of the Pokémon universe or introduced in the games. Same goes for the generation, so it naturally makes sense as Pokémon's that are discovered first will have more screen on time therefore more popularity.

It's interesting to see height and sp_defense as the features that people find the most desirable.

On the contrary people don't really care about a Pokémon's name or gender which is an important thing to note.

<feature importance plot>

##### What are the Features that Contribute the most in a Pokémon's Popularity?

Here is a pie chart visualising the relative contribution of features in Pokémon popularity.

<attach pie chart>

---

### What Makes a Pokémon Legendary?

After browsing the dataset, we can see several variables that could feasibly explain what makes a Pokémon legendary. We have a series of numerical fighter stats – attack, defense, speed and so on – as well as a categorization of Pokemon type. is_legendary is the binary classification variable we will eventually be predicting, tagged 1 if a Pokémon is legendary and 0 if it is not.

### Variable Exploration

##### 1. How many Pokémon are legendary?

We now know that there are 70 legendary Pokémon – a sizable minority at 9% of the population! Let's start to explore some of their distinguishing characteristics.

<insert table>

##### 2. Legendary Pokémon by height and weight

We'll add conditional labels to the plot, which will only print a Pokémon's name if it is taller than 7.5m or heavier than 600kg.

It seems that legendary Pokémon are generally heavier and taller, but with many exceptions. For example, Onix (Gen 1), Steelix (Gen 2) and Wailord (Gen 3) are all extremely tall, but none of them have legendary status. There must be other factors at play.

<add scatter plot>

##### 3. Legendary Pokémon by type

There are clear differences between Pokémon types in their relation to legendary status. While more than 30% of flying and psychic Pokémon are legendary, there is no such thing as a legendary poison or fighting Pokémon!

<add type bar plot>

##### 4. Legendary Pokémon by fighter stats

As we might expect, legendary Pokémon outshine their ordinary counterparts in all fighter stats. Although we haven't formally tested a difference in means, the boxplots suggest a significant difference with respect to all six variables. Nonetheless, there are a number of outliers in each case, meaning that some legendary Pokémon are anomalously weak.

<box plot>

#### Create a training/test split

We have now explored all of the predictor variables we will use to explain what makes a Pokémon legendary. Before fitting our model, we will split the pokedex into a training set and a test set. This will allow us to test the model on unseen data.

```r
  n <- nrow(pokemon)
  sample_rows <- sample(n, 0.7 * n)

  pokemon_train <- pokemon %>%
    filter(row_number() %in% sample_rows)
  pokemon_test <- pokemon %>%
    filter(!row_number() %in% sample_rows)
```

#### Fit a decision tree

Before we fit a random forest, we will fit a simple classification decision tree. This will give us a baseline fit against which to compare the results of the random forest, as well as an informative graphical representation of the model.

Here, and also in the random forest, we will omit incomplete observations by setting the na.action argument to na.omit. This will remove a few Pokémon with missing values for height_m and weight_kg from the training set. Remember the warning messages when we made our height/weight plot in Task 3? These are the Pokémon to blame!

<add decision tree graph>

#### Fit a random forest

Decision trees are unstable and sensitive to small variations in the data. It therefore makes sense to fit a random forest – an ensemble method that averages over several decision trees all at once. This should give us a more robust model that classifies Pokémon with greater accuracy.

```
  Type of random forest: classification
    Number of trees: 500
    No. of variables tried at each split: 3

  OOB estimate of  error rate: 6.41%
  Confusion matrix:
      0  1 class.error
  0 488  7  0.01414141
  1  28 23  0.54901961

```

#### Assess model fit

In order to allow direct comparison with the decision tree, we will plot the ROC curves for both models using the ROCR package, which will visualize their true positive rate (TPR) and false positive rate (FPR) respectively. The closer the curve is to the top left of the plot, the higher the area under the curve (AUC) and the better the model.

It's clear from the ROC curves that the random forest is a substantially better model, boasting an AUC (not calculated above) of 91% versus the decision tree's 78%. When calculating variable importance, it makes sense to do so with the best model available, so we'll use the random forest for the final part of our analysis.

<add the curve>

#### Analyze variable importance

Note that a random forest returns two measures of variable importance:

- MeanDecreaseAccuracy – how much the model accuracy suffers if you leave out a particular variable
- MeanDecreaseGini – the degree to which a variable improves the probability of an observation being classified one way or another (i.e. 'node purity').
  Together, these two measures will allow us to answer our original research question – what makes a Pokémon legendary?

<add the graph>

---

#### Answering Business Problems

##### Popularity

##### Legendary Status

1. Is the `attack` or `defense` variable more important?
   answer <- "attack"

2. Is the `weight_kg` or `height_m` variable more important?
   answer <- "weight_kg"

3. Is the `attack` or `defense` variable more important?
   answer <- "defense"

4. Is the `weight_kg` or `height_m` variable more important?
   answer <- "weight_kg"

---

#### Conclusion
