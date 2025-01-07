# What makes a Pokémon popular amongst viewers?

## 1. Introduction

To increase viewer retention we need to know the factors that contribute the most to a Pokémon's popularity, because **Pokémon popularity and viewer retention are directly proportional**.
If we somehow figure out the factors that contribute the most we could work on them for other Pokémon's as well and get better viewer retention, **increasing overall revenue**.
In this project we'll dive deep into analyzing and figuring out those factors. Also, we'll figure out **what makes a Pokémon legendary** as that's a big deal amongst Pokémon fanbase.

### What factors contribute the most to a Pokémon's popularity amongst viewers?

This is a list of all the factors related to a Pokémon that we'll be looking at while figuring out the most important one.

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

##### Let's start by looking at how many Pokémon's belong to a perticular type

Looking at the distribution of types along with their legendary status we mainly notice 2 things. First - most type has the highest number of Pokémon's in it followed by normal and grass, second - there are bunch of types that don't have any legendary Pokémon's in them eg. bug, grass.

<categorical vairable exploration>

##### Now we should analyse the spread of all the different features by looking at a density plot

We can see that in the case of features like attack and speed there are larger number of Pokémon's that have average scores whereas features like capture rate and weight show that larger number of Pokémon's are not captured often and are lighter.

<Density histogram>

##### To visualize the correlation between all the features that we are looking at and their popularity score we'll do a complete bivariate analysis

Here we can explore the relationship between popularity score and other features to identify trends and correlations.
If we take a look at the graph it seems like sp_attack and sp_defense have a significant impact on the popularity score wherease speed and attack have a moderate positive correlation.

<scatter plot bivariate analysis>

##### Let's look at the popularity spread for each type of Pokémon

We can clearly see that people tend to like dragon type more compared to all the other types. As we have the box-plot here we can also take a look at the outliers.

#####
