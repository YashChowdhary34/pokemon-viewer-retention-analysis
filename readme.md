# What Makes a Pokémon Popular Amongst Viewers?

## Introduction
To increase viewer retention, we need to identify the factors that contribute most to a Pokémon's popularity because **Pokémon popularity and viewer retention are directly proportional**. 

By uncovering these factors, we can focus on enhancing them for other Pokémon, thereby improving viewer retention and **increasing overall revenue**. In this project, we will analyze these factors in depth. Additionally, we’ll explore **what makes a Pokémon legendary**, a highly significant topic among Pokémon enthusiasts.

---

## Dataset Information
The dataset used in this project is `pokemon_dataset.csv`, which contains detailed statistics and attributes of Pokémon, including:

- **Basic stats**: `height_m`, `weight_kg`, `attack`, `defense`, etc.
- **Attributes**: `type`, `generation`, and `legendary status`.
- **Additional metrics**: `capture_rate`, `pokedex_number`, and `popularity_score`.

This dataset forms the basis for identifying popularity trends and determining legendary status predictors.

---

## Table of Contents

1. [Factors Contributing to Pokémon Popularity](#factors-contributing-to-pokémon-popularity)
   - [Variable Exploration](#variable-exploration)
   - [Handling Outliers](#handling-outliers)
   - [Train/Test Split](#traintest-split)
   - [Model Fitting (Random Forest)](#model-fitting-random-forest)
   - [Model Performance Analysis](#model-performance-analysis)
   - [Feature Importance Analysis](#feature-importance-analysis)
2. [What Makes a Pokémon Legendary?](#what-makes-a-pokémon-legendary)
   - [Variable Exploration](#legendary-variable-exploration)
   - [Train/Test Split](#legendary-traintest-split)
   - [Decision Tree Fitting](#decision-tree-fitting)
   - [Random Forest Fitting](#random-forest-fitting)
   - [Model Fit Assessment](#model-fit-assessment)
   - [Feature Importance Analysis](#legendary-feature-importance-analysis)
3. [Answering Business Problems](#answering-business-problems)
   - [Popularity](#popularity)
   - [Legendary Status](#legendary-status)
4. [Conclusion](#conclusion)

---

## Factors Contributing to Pokémon Popularity

### Variable Exploration

#### 1. Which types have the most Pokémon?
The distribution of types and their legendary status reveals that:

- **Water type** has the highest number of Pokémon, followed by Normal and Grass.
- Several types (e.g., Bug, Grass, Poison) do not have any legendary Pokémon.

<div align="center">
<img src="https://github.com/user-attachments/assets/cad74064-5124-4f33-a9a7-91b9ca805000" alt="Distribution of Types" width="600">
</div>

#### 2. Spread of Features: Density Plot
- **Attack** and **Speed** show a large number of average Pokémon.
- **HP**, **Height**, and **Weight** show most Pokémon as shorter, lighter, and having lower HP.

<div align="center">
<img src="https://github.com/user-attachments/assets/25762ddb-0916-47ef-91d1-a54eac9919a3" alt="Density Histogram" width="600">
</div>

#### 3. Feature Correlation with Popularity Score
Features like **Special Defense (Sp_Defense)**, **HP**, and **Special Attack (Sp_Attack)** have significant correlations, while **Speed** and **Attack** have moderate positive correlations.

<div align="center">
<img src="https://github.com/user-attachments/assets/8266ca64-5de2-4949-8948-bedb4ec99ca5" alt="Correlation Analysis" width="600">
</div>

#### 4. Popular Pokémon Types
**Dragon types** are generally more popular compared to others, with clear outliers visible in the box plot.

<div align="center">
<img src="https://github.com/user-attachments/assets/6b6379b0-2d08-4b17-9019-4751a72b9ee0" alt="Box Plot of Types" width="600">
</div>

### Handling Outliers

#### Identifying Outliers
<div align="center">
<img src="https://github.com/user-attachments/assets/b000e34c-7194-44e3-9c2c-0a31a74140a1" alt="Outlier Identification" width="600">
</div>

#### Removing Outliers
<div align="center">
<img src="https://github.com/user-attachments/assets/378ce851-0524-494d-b337-d8e627a3dc33" alt="Outlier Handling" width="600">
</div>

### Train/Test Split
To ensure robust testing, we split the dataset:

```r
train_index <- createDataPartition(pokemon$popularity_score, p = 0.8, list = FALSE)
train_data <- pokemon[train_index, ]
test_data <- pokemon[-train_index, ]
```

### Model Fitting (Random Forest)
We use a **Random Forest model** for its robustness and ability to handle non-linear interactions:

```r
rf_model <- randomForest(popularity_score ~ ., data = train_data, importance = TRUE, ntree = 500)
```

### Model Performance Analysis
**Mean Squared Error (Random Forest):** 7.13

### Feature Importance Analysis
Key predictors include:

- **Pokedex Number** and **Generation** (earlier Pokémon have more screen time).
- **Height** and **Sp_Defense** (desirable features).
- **Gender** and **Name** are less important.

<div align="center">
<img src="https://github.com/user-attachments/assets/7504096a-b894-4cda-976a-dee359ae25ba" alt="Feature Importance" width="600">
</div>

---

## What Makes a Pokémon Legendary?

### Legendary Variable Exploration

#### 1. How many Pokémon are legendary?
- 70 Pokémon (9%) are legendary.

#### 2. Legendary Pokémon by Height and Weight
Legendary Pokémon are generally heavier and taller, but there are exceptions.

<div align="center">
<img src="https://github.com/user-attachments/assets/db30e396-33ea-44d6-82bb-861873e8651e" alt="Height and Weight Analysis" width="600">
</div>

#### 3. Legendary Pokémon by Type
Certain types (e.g., Flying, Psychic) have a higher proportion of legendary Pokémon.

<div align="center">
<img src="https://github.com/user-attachments/assets/09cb5ec7-819a-45f0-8fdc-9f849efc0208" alt="Type Analysis" width="600">
</div>

### Legendary Train/Test Split

```r
n <- nrow(pokemon)
sample_rows <- sample(n, 0.7 * n)

pokemon_train <- pokemon %>% filter(row_number() %in% sample_rows)
pokemon_test <- pokemon %>% filter(!row_number() %in% sample_rows)
```

### Decision Tree Fitting
Used for baseline comparison:

<div align="center">
<img src="https://github.com/user-attachments/assets/dec9bf19-f11d-45b4-b141-5a9e01ef48ff" alt="Decision Tree" width="600">
</div>

### Random Forest Fitting
- **OOB Error Rate:** 6.41%

### Model Fit Assessment
The ROC curve shows Random Forest outperforms the Decision Tree:

<div align="center">
<img src="https://github.com/user-attachments/assets/212870d3-4b91-4508-8a18-ca1819ebd405" alt="ROC Curve" width="600">
</div>

### Legendary Feature Importance Analysis

<div align="center">
<img src="https://github.com/user-attachments/assets/18415ed2-bd84-4a3d-ab59-f8a9ed7fc340" alt="Feature Importance" width="600">
</div>

---

## Answering Business Problems

### Popularity

1. **Which Pokémon type correlates most with popularity?**  
   **Answer:** Dragon.

2. **Does generation impact popularity?**  
   **Answer:** Yes, earlier generations are more popular.

3. **Is height or weight more important for popularity?**  
   **Answer:** Height.

4. **Does Sp_Attack or Sp_Defense have a higher impact?**  
   **Answer:** Sp_Defense.

5. **What feature is least significant for popularity?**  
   **Answer:** Gender.

### Legendary Status

1. **Is `attack` or `defense` more important?**  
   **Answer:** Attack.

2. **Is `weight_kg` or `height_m` more important?**  
   **Answer:** Weight.

---

## Conclusion
This analysis highlights the factors driving Pokémon popularity and legendary status. Strategic use of these insights can improve viewer retention and foster a more engaged fanbase.

---

*Project by [Yash Chowdhary](https://github.com/YashChowdhary34/pokemon-viewer-retention-analysis).*
