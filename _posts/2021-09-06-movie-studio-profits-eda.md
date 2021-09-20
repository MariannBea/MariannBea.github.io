---
title: Making Money From Movies - Step 3
date: 2021-09-06 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Machine Learning
tags:
  - Python
  - Data Cleaning
classes: wide
---
#### Step 3: Exploratory Data Analysis

This is the third post in a series about using data analysis to look for features that make movies more likely to be successful.  The first post can be seen [here](https://mariannbea.github.io/machine%20learning/movie-studio-profits-inspecting-the-data/). In previous posts, I discussed my initial analysis and how I cleaned the data. The aim of this series is to answer the following questions:

1.	Is there a correlation between genre and profits?
2.	Is there a correlation between content rating and profits?
3.	Are some genres more profitable for specific content ratings?
4.	Does an increase in the number of Facebook likes for directors or actors correlate with increased profits?
5.	Is being in or directing a greater number of movies correlated with more profits?
6.	Are some topics correlated with more profits?

I will use linear regression and decision trees to help answer these questions. However, before using any machine learning models on the data, I took a closer look at the relationship between each of the features I thought might affect profits.  I did this by graphing each variable separately against the inflation-adjusted profits to see what patterns could be observed.  The type of graph I used varied according to the data.

First, I looked more carefully at the association between genre and profits.  I did this in several ways.  One was looking for a correlation between the number of genres that a movie was labelled and profits using a scatter plot. 

![picture of genre scatter plot](https://user-images.githubusercontent.com/83561268/132159013-59baaaf7-76e1-4515-b23c-bfe260ecd922.png)

From the graph, it appears that there might be some benefit to creating movies that can be associated with more than one genre. However, having an association with too many types of genres seems to be detrimental.  This makes sense because a movie that could be classified with more than one genre might increase the potential audience. For example, a 'Mystery - Western' movie might attract both fans of mysteries and westerns.  However, increasing the number of genres beyond three dilutes each type too much to attract fans of any particular genre. A 'Western-Space-Horror-Comedy-Musical" would be a unique type of movie that might not really attract customers who might have been attracted to any one of those genres individually. 

I also looked at each type of genre separately against profits. I initially tried stacking the genres on top of each other.  However, there was so much overlap that it was easier to understand each genre graphed separately.

![picture 1 of genre histograms](https://user-images.githubusercontent.com/83561268/132159082-fcbd4f72-905b-4d8b-8b5b-53b5f6a080fc.png)

![picture 2 of genre histograms](https://user-images.githubusercontent.com/83561268/132159094-96b61f2c-8147-4008-bc95-5af41b8025db.png)

![picture 3 of genre histograms](https://user-images.githubusercontent.com/83561268/132159103-2da3f7d8-7cc0-4edc-b597-6fadaae14415.PNG)

Looking at the histograms, it is easy to see some trends.  Few genres never lose any money. War movies, Crime movies, Thrillers and Biographies are more likely to lose money than make high profits. Documentaries are unlikely either to lose money or to produce very high profits. Animated movies and Family movies seem more likely to be successful than to lose money.  However, there are no guarantees when it comes to a particular genre making or losing money.

To make it easier to see how different genres compare with the number of unprofitable and successful movies they made, I also created a graph comparing movies that lost money to those in the top 25th percentile.  Looking at this graph, it is easy to see that Family, Adventure and Fantasy movies are all much more likely to be a hit than a flop – at least based on the films in this particular data set.

![genre htits and flops graphs](https://user-images.githubusercontent.com/83561268/132214710-80904120-8f41-4e92-89ad-24877dab5a90.png)

From this analysis, it is clear that genre should be included in the machine learning models.

Next, I looked at how content rating compared to profits.  To look at this, I created stacked [histograms](https://medium.com/analytics-vidhya/tutorial-exploratory-data-analysis-eda-with-categorical-variables-6a569a3aea55) after reading this blog post. One graph had ratings for adults and children over 12, and the other had those appropriate for children under 13. Unrated and NC-17 ratings had so few movies that these needed to be graphed separately.

![content rating histographs](https://user-images.githubusercontent.com/83561268/132214841-0c821f53-9028-47b4-9c2c-a0cbbaa8eb9e.PNG)

The graphs above show that NC-17 and Unrated Movies are unlikely to affect predictions made using a machine learning algorithm. There were very few of either type of these movies in the dataset. The other ratings are in line with what can be seen in the genre graphs. PG and G rated films are more likely to be a success than to lose money. These ratings are well-matched with the Family, Adventure, Animation and Fantasy genres.

![ratings hits and flops](https://user-images.githubusercontent.com/83561268/132215091-ef16ba81-cc62-449b-a7c7-19520c1fd4be.png))

The graph above makes it even more apparent that a greater proportion of movies made for children and young adults are likely to make profits than lose money.

Next, I looked at the relationship between keywords and profits.  A box plot was used to show the range of profits made by movies linked to each keyword. Based on the keywords below, it seems that films that can be described as 'epic' are very likely to be successful. The same is true for movies that feature princesses and secrets. I was surprised to see that fish is also a keyword that appears to be linked to movies that are more likely to make a significant profit. I was also amazed to see that, contrary to a well-known saying, it seems that movies with drugs or sex as main features are more likely to lose money than to make lots of profit. 

![keyword box plot](https://user-images.githubusercontent.com/83561268/132215226-0d2c353f-814a-4aa7-b95e-2f3ba3dcf05f.png)

Looking at the graphs below, it appears that the number of movies an actor or director in does not necessarily indicate that a film will make more profits.  In fact, many of the movies that made in the top 25% of profits had directors or actors who took part in fewer movies than those who made less profit. One reason for this could be that actors and directors who work on more movies demand larger salaries, affecting profits.

![Number of Movies Scatter Plots](https://user-images.githubusercontent.com/83561268/132224342-c8ce39a8-f721-4937-95af-d033cafba7a1.png)

There isn't an obvious correlation between the number of Facebook likes directors or actors had and movie profits.  Because Facebook is recent, it seemed like this feature might only be relevant to movies made after Facebook became popular. When creating these graphs, I created a separate data frame with movies made only after a particular year.  I tried various cut-off years from 2004 to 2015; however, no obvious correlation was visible in any graphs produced.  The scatterplots shown above were created with movies made after 2010.

![Facebook Likes and Profits](https://user-images.githubusercontent.com/83561268/132225918-af096b22-8753-4c4c-8346-48c32b4a50b9.PNG)

The relationship between budget, posters' faces and movie duration is not part of the original questions posed. However, as these variables are under the control of movie studios and might affect profits, I created scatterplots to look more carefully at their relation to earnings to decide whether to include them as extra features in any machine learning models tried. 

![other features scatter plot](https://user-images.githubusercontent.com/83561268/132224496-de0d8286-0f89-44dc-aee7-d6bbbb51eb1b.PNG)

Looking at the scatter plots, it appears there might be some weak correlation between budget and profits.  The number of faces in posters seems to have a slight negative correlation with earnings, while movie duration looks positive.

Having looked more carefully at the data, it is now time to use what I found out to start training machine learning models. You can read about it [here]().

If you would like to see the code that I used in this exploratory data analysis, click [here]().

#### Resources

Tutorial: Exploratory Data Analysis (EDA) with Categorical Variablesby Erin Hoffman on [Medium](https://medium.com/analytics-vidhya/tutorial-exploratory-data-analysis-eda-with-categorical-variables-6a569a3aea55)
