---
title: Making Money From Movies - Step 2
date: 2021-09-06 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Machine Learning
tags:
  - Python
  - Data Cleaning
  - standard
toc: true
classes: wide

---

#### Step 2: Preparing and Cleaning The Data

This is the second entry in a series about using Machine Learning to determine which features are correlated with making top profits in the movie industry. To read the first post in the series, click [here](https://mariannbea.github.io/machine%20learning/movie-studio-profits-inspecting-the-data/).

In this series, I am aiming to answer the following questions:

1.	Is there a correlation between genre and profits?
2.	Is there a correlation between content rating and profits?
3.	Are some genres more profitable for specific content ratings?
4.	Does an increase in the number of Facebook likes for directors or actors correlate with increased profits?
5.	Is being in or directing a greater number of movies correlated with more profits?
6.	Are some topics correlated with more profits?

#### Using the Movie Database API to Get Budget Data

First, it was essential to get more accurate profit data.  After searching for a while, it seemed the best place to get this data from was [The Movie Database](https://www.themoviedb.org/?language=en-US).  They have a wide range of information on their site and, unlike IMDb, it was free to access it all via their API. I'd never used an API to get information before. Fortunately, Coding For Entrepreneurs has a [tutorial](https://www.youtube.com/watch?v=Sg5VTTBIhqo) that shows exactly how to use the Movie Database API. You can even access the code used in the tutorial on [GitHub](https://github.com/codingforentrepreneurs/30-Days-of-Python/tree/master/tutorial-reference/Day%2013). The connection kept timing out before the data was downloaded entirely, so I ended up saving the data obtained after each try and collating it together.

```python
    # use if the connection times out
    movie_data = pd.DataFrame(movie_data)
    movie_ids.to_csv("movie_ids2")

    #use if the connection times out to save obtained data
    movies1 = pd.read_csv("movie_profits.csv")
    movie_data.columns = ["title", "budget", "revenue"]
    movies = [movie1, movie_data]
    movie_budget = movies1.append(movie_data)
    movie_budget.to_csv("movie_profits.csv", index = False)
```

After a few tries, I had the data I needed.  The movie database returned ids for every movie with a similar name to the one sent to it. This meant that the results needed to be compared to the original dataset before the data was merged.

```python
    def movie_matching(title: str, _id: str, j: int) -> bool:
        # checks if the movie found matchs the title of the movie in the database
        if (not re.match(title, name_list.iloc[j, 0])):
            print(f'no match: {title}, {name_list.iloc[j, 0]}, {j}')
            if j == (len(name_list) - 1): #stop checking at 2000 to avoid stack overrun
                j = 0
                return False;
            else:
                j += 1
                movie_matching(title, _id, j)
        else: 
            movie_ids.add(_id)
            print(f'match: {title}, {name_list.iloc[j, 0]}, {j}')
            # if found, drop title from list to reduce search time and 
            # also so that remaining titles can be searched for again without the year
            name_list.drop(j, inplace = True) 
            name_list.reset_index(drop=True, inplace=True)
            return True;     
```

#### Adjusting for Inflation

After updating the budget, revenue and profit information, I located information about [worldwide inflation](https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG) from the world bank.  This information was used to adjust the amounts found for inflation.  

```python
	inflation = pd.read_csv("price_index.csv")

	# calculate mean inflation rate for each country.  Use this rate to fill in NaN values    
	
	inflation['mean'] = inflation.mean(axis = 1, numeric_only = True)
	inflation = inflation.set_index('country')

	# fill missing years with 2005, missing countries with USA (most common)
	
	movies_df['title_year'].fillna(2005, inplace = True)
	movies_df['country'].fillna('USA', inplace = True)

	#determine inflation rate for each movie, movies before 1960 given mean inflation rate
	movies_df['title_year'] = movies_df['title_year'].astype(int)

	for index, year, country in movies_df[['title_year', 'country']].itertuples():
    	stryear = str(year)
    	strcountry = str(country)
    	if year >= 1960:
        	movies_df['rate'] = inflation.loc[[strcountry],[stryear]].iloc[0][0]
    	else:
        	movies_df['rate'] = inflation.loc[[strcountry],['mean']].iloc[0][0]

	# find budget, gross and profits adjusted for inflation

	movies_df['budget_infl'] = (movies_df['budget']/movies_df['rate']) * 100
	movies_df['gross_infl'] = (movies_df['revenue']/movies_df['rate']) * 100
	movies_df['profit_infl'] = (movies_df['profit']/movies_df['rate']) * 100

	movies_df.drop_duplicates(inplace = True)
```

Next, the profit amounts were divided into categories to use with the decision tree analysis. I started with having ten categories, but this was eventually changed to three.  This change was made after reading Early Predictions of Movie Success: The Who, What, and When of Profitability[2] which suggested the categories of success, failure and average. This categorization more closely matched the goal of predicting movie success than having ten categories did. The adjusted budget amount was divided into 4 categories. This was done to explore the effects of budgets on profits with a decision tree while still making the results from the decision tree analysis easy to understand. 

```python
	# find the firstand third quartile amounts to use to categorize the values
	Q1 = movies_df['profit_infl'].quantile(0.25)
	Q3 = movies_df['profit_infl'].quantile(0.75) 

	# divide the profits into categories to use when creating decision trees
	movies_df['profit_str'] = None

	movies_df['profit_str'] = np.where(movies_df['profit_infl'] >= Q3, 'Success', movies_df['profit_str'])

	movies_df['profit_str'] = np.where(movies_df['profit_infl'].between(Q1, Q3),
                                              'Some Profits', movies_df['profit_str'])
	movies_df['profit_str'] = np.where(movies_df['profit_infl'].between(0, Q1),
                                              'Low Profits', movies_df['profit_str'])
	movies_df['profit_str'] = np.where(movies_df['profit_infl'] <= 0,
                                              'Failure', movies_df['profit_str'])

	#drop any values that were not filled
	movies_df.dropna(how='any', inplace=True)

	#check to see how many items are in each category
	print(movies_df['profit_str'].value_counts())
```

#### Preparing for Genre and Content Rating Explorations

After the profit and budget data were organized, I prepared the data to explore the effect of genres and content rating on profit. Genre information was split into a list, then made binary by encoding a 1 if a movie was listed as a particular genre and a 0 if not. Because the data was in the form of a list, it was impossible to use one-hot encoding. Instead, I used code from a [blog post](https://towardsdatascience.com/dealing-with-list-values-in-pandas-dataframes-a177e534f173) by Max Hilsdorf written about transforming lists into a data frame to create a genres data frame.  I then merged this data frame with the original one.  The content ratings were combined into fewer categories based on the age and suggested amount of parent supervision. This was done to reduce the feature space and, hopefully, give the machine learning algorithms a better chance of predicting movie success.

#### Accurately Counting Movies to Compare with Profits

My first attempt to see if there was a correlation between the number of movies a director or actor participated in and profits just counted the number of movies each person was in. However, I quickly realized this isn't an accurate representation of reality. A director who directed 43 films didn't direct 43 movies when they were making their first movie. So, I rewrote the code to more accurately reflect the number of movies the person was involved in at the point of time that each one was made. First, the movies were sorted by year. Each time a person was encountered while iterating through the data frame, their count was incremented by one.  This new count was added to the data frame for that movie.

```python
	# sort movies by year so that the earliest movie a director made will have a count of one.
	movies_df = movies_df.sort_values(by = ['title_year']).reset_index(drop = True)

	# dictionary to store the count for each director
	director_count = {}

	# The first time a director is encountered in the dataframe, they will be given a count of one.  
	# Each additional movie will add to the total
	for index, title, director, year in movies_df[['movie_title','director_name', 'title_year']].itertuples():
    	if director in director_count:
        	movies_df.loc[movies_df['movie_title'] == title,'director_count'] = (director_count[director] + 1)
        	director_count[director] += 1
    	else:
        	movies_df.loc[movies_df['movie_title'] == title,'director_count'] = 1
        	director_count[director] = 1
```
#### Text Analysis to Find Most Relevant Key Words
 
Next, the plot keywords field was used with a bag of words model to find words more likely to predict increased movie profits. Other options that were considered for analyzing the keywords were named entity recognition, word embedding and a simple word frequency count.  However, since the goal is to determine what movie executives could do to make movies more likely to succeed, having a list of words correlated to movie success or failure would provide more helpful information. These words would indicate the types of topics that are more likely to result in a successful movie.  The method for preparing the plot list and then analyzing it was shared by Mauro Di Pietro in [this article](https://towardsdatascience.com/text-analysis-feature-engineering-with-nlp-502d6ea9225d). After finding out which keywords were correlated with more or less movie profits, these words were added to the database as binary values using the same method used for the genres.

#### Final Cleaning Steps
 
The last few steps involved dropping columns, filling in missing values and selecting more recent movies. I dropped the following columns: 'color, 'num_voted_users', 'language', 'country', 'num_user_for_reviews', 'num_critic_for_reviews' as they would not be used in the analysis. Missing values in most columns were filled with the median for those columns. Movies with missing profit information were already dropped while adding the newly acquired revenue, budget and profit data. I also quickly selected only movies made after 1999.  Now the data was finally ready for further analysis. The cleaned database was saved to a csv document to be imported into the notebooks used for analysis. 

Next step is to look more carefully at that data and choose featues to use when performing linear regression and decision tree analyses.  Click [here](https://mariannbea.github.io//movie-studio-profits-eda/) to read about it.

Click [here](https://github.com/MariannBea/Movie-Studio-Analysis/blob/e5d2e5f134100b56a835581371772b68c18c172b/Notebooks/Movies%20-%20Cleaning.ipynb) if you would like to see all of the code used in this process.

[Here]( https://github.com/MariannBea/Movie-Studio-Analysis/blob/57931c07b18bc26b34e4d60335b8a4735697ac6b/Notebooks/Get%20Budget%20Info.ipynb) is the code for obtaining movie gross and revenue data from the Movie Database api.

#### Resources

[The Movie Database](https://www.themoviedb.org/?language=en-US)

Coding for Entrepuneurs, 30 Days of Code [You Tube Video](https://www.youtube.com/watch?v=Sg5VTTBIhqo)

Coding for Entrepuneurs, 30 Days of Code[Source Code](https://github.com/codingforentrepreneurs/30-Days-of-Python/tree/master/tutorial-reference/Day%2013)

[World Bank Inflation Indicators](https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG)

Dealing with List Values in Pandas Dataframes by Max Hillsdorf on [Medium](https://towardsdatascience.com/dealing-with-list-values-in-pandas-dataframes-a177e534f173)

Text Analysis & Feature Engineering with NLP by Mauro Di Pietro on [Medium](https://towardsdatascience.com/text-analysis-feature-engineering-with-nlp-502d6ea9225d)
