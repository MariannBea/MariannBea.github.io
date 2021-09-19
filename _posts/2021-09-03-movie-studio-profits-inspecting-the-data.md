---
title: Making Money From Movies - Step 1
date: 2021-09-03 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Machine Learning
tags:
  - Python
  - Data Analysis
  - standard
classes: wide
---

#### Making Money from Movies - Step 1: Inspecting the Data Set

25% of the movies in the [IMDb-5000-movie-dataset](https://www.kaggle.com/carolzhangdc/imdb-5000-movie-dataset) lost money.  While this might seem high, according to many online resources, that figure is actually low. [Stephen Fellows](https://stephenfollows.com/hollywood-movies-make-a-profit/) found that about 50% of films actually lose money. It is even said that 80% of movies lose money, although this is likely a trick of [shady practices](https://priceonomics.com/why-do-all-hollywood-movies-lose-money/) and creative bookkeeping. However, some movies do make extraordinary profits. Is it possible to predict which ones will make the most? To find out, I used the IMDB dataset found on the Kaggle website along with a bit of Machine Learning. My goal was to see if I could predict if a film will be in the top 25% of profitability for the year, using factors that movie studios could consider when planning a movie project.   

After loading the data into a pandas Dataframe, I used a report created using the [pandas-profiling package](https://pandas-profiling.github.io/pandas-profiling/docs/master/index.html). [1] This report makes it very easy to do a quick visual analysis of what each attribute contains. The report provides information about the range of each variable and the percentage of values that are missing or distinct. It also creates a bar graph and warnings for properties of the attribute that might cause issues during analysis. In addition, it provides several different correlation matrices showing the amount of correlation between various variables.  It is a very efficient way to get a quick, visual overview of the data. 

Understanding what type of information a dataset holds is the first step in any data anlysis project. It is important to get an idea of what information is available and how this information is organized. This means looking at what fields are present as well as the composition of the data in each field. Categorical and numeric data must be processed and analyzed in different ways. In addition the variety of different categories and the distrubition of the data can have an affect on the analysis. All of this information must be taken into considerating when planning how to best use data to gain new insights. Thinking about what data is missing that might add additional values is often useful as well.

#### This is what I observed on my first look at the profile report:

*	About half of the variables contained information that studios had direct control over in planning future productions.
*	The other half of the information was about things that studios would have little or no control over, such as the number of Facebook likes or reviews on IMDb. However, some of this information could possibly be used when choosing actors or directors for a movie.
*	Some of the variables, like director and actor, had a lot of different possible values. These could be more difficult to use with Machine Learning algorithms, as their results can become less accurate with too many features. One option might be to include only movies by directors who have made at least 5 movies. Another is to disregard this information.
*	The first movie in the database was from 1916. Movies from far in the past might not be as good at helping to predict future movie sales as it is likely that people's tastes in movies have changed over time. Perhaps looking at films only in the more recent past might give better results.
*	Data was heavily skewed towards color movies, the English language and movies made in the US. As most movies are made in color now, this variable could probably be dropped. Language and country data will either need some pre-processing before use to reduce the imbalance, or they will also need to be dropped.
*	Most of the data did not have many missing fields. Unfortunately, budget and gross, two of the more important ones for this analysis, had a high percentage of missing data. In addition, many of the values were referring to different information. Some values referred to total gross US and Canada sales, while others referred only to the opening weekend. Reobtaining this information and ensuring it all refers to the same type of information would give more valid results.
*	Very few of the values had a normal distribution. Some of this was likely due to the changes in technology over time and inflation.
*	Many of the values had high correlations between them. This was also likely due to changes over time in many cases. 
*	Both budget and gross had an extremely wide distribution. Part of this was probably due to inflation. Adjusting amounts for inflation might help with this to some extent. This would also make the results more accurate.

After this quick look over the data, these were the questions I decided to investigate further. 

##### Questions to Investigate

1.	Is there a correlation between genre and profits?
2.	Is there a correlation between content rating and profits?
3.	Are some genres more profitable for specific content ratings?
4.	Does an increase in the number of Facebook likes for directors or actors correlate with increased profits?
5.	Is being in or directing a greater number of movies correlated with more profits?
6.	Are some topics correlated with more profits?

Before beginning the investigation; however, the data will need to be cleaned and organized.

#### Resources

[1]	S. Roy, “Accelerate Your Exploratory Data Analysis With Pandas-Profiling,” Apr. 20, 2020. https://towardsdatascience.com/accelerate-your-exploratory-data-analysis-with-pandas-profiling-4eca0cb770d1 (accessed Jun. 08, 2021).

[2]	M. T. Lash and K. Zhao, “Early Predictions of Movie Success: The Who, What, and When of Profitability,” Journal of Management Information Systems, vol. 33, no. 3, pp. 874–903, Jul. 2016, doi: 10.1080/07421222.2016.1243969.

[Kaggle Dataset](https://www.kaggle.com/carolzhangdc/imdb-5000-movie-dataset)

Hollywood Movies Make a Profit by [Stephen Follows](https://stephenfollows.com/hollywood-movies-make-a-profit/)

Why Do All Hollywood Movies Lose Money? by Alex Mayyasi[Priconomics.com](https://priceonomics.com/why-do-all-hollywood-movies-lose-money/)

[Pandas Profiling](https://pandas-profiling.github.io/pandas-profiling/docs/master/index.html)
