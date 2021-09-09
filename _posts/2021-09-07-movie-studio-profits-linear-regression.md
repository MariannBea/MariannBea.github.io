---
layout: post
title: Making Money From Movies - Step 3, Part 1
date: 2021-09-06 13:32:20 +0300
description: Exploratory Data Analysis. # Add post description (optional)
img: Genres.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Python, Linear Regression]
categories: [Machine Learning]
---

#### Making Money From Movies - Step 3: Machine Learning Models

##### Linear Regression

This is the third entry in a series about using machine learning models to predict movie success.  You can find the first entry [here](https://mariannbea.github.io//movie-studio-profits-cleaning/).

I chose to use linear regression because it is a quick way to see if a direct correlation can be found between any features and profits. In these analysis, I used the normalized version of earnings because I found easier to interpret the results. 

First, I investigated the relationship between genre and profits. I compared all the genres in the data set. Then I used a smaller set with just those genres that appeared to be more closely linked to a movie either losing money or being very profitable.  The genres that were used were: 'Thriller', 'Fantasy', 'Animation', 'Family', 'Action',' Drama', 'Sci-Fi', 'Crime', 'Adventure' and 'Romance'. The comparison with all of the genres gave slightly better results.

![genre and profits linear regression](https://user-images.githubusercontent.com/83561268/132297158-c792ff6f-baf6-4496-9b82-7a49347b286d.png)

Next, I performed linear regression with the G, PG, PG-13 and R content ratings.
  
![content rating linear reagression](https://user-images.githubusercontent.com/83561268/132297195-788da868-436a-49ab-a4a8-31b86709f16b.PNG) 

Looking at the coefficient of determination, it seems that very little of the variation in profit can be attributed to the content rating.

This is not the case for the number of movies that directors and actors have taken part in before working in a particular film which shows a slightly positive correlation.  However, it is not large enough that it would be the primary recommendation for increasing profits. One reason for this might be that salaries presumably increase with the number of past movies an actor or director has been part of.

![number of movies linear regression](https://user-images.githubusercontent.com/83561268/132297214-99703227-6029-4e23-af29-4dc4b85e7d35.png)
 
Facebook likes were the next feature that I tried.  Facebook has not been around for as long as many of the movies in the database. In addition, its use has varied over time, so I looked at how Facebook likes predicted profits in movies made only after particular dates. 

![Facebook likes linear regression](https://user-images.githubusercontent.com/83561268/132297349-b7b4a722-a932-455b-a5c6-7c0d79a247f6.PNG))

With films made after 2005, shortly after Facebook was founded, the coefficient of determination is only 9%.  However, this increases to 17% with movies made after 2015.  Facebook likes do a much better job of predicting movie success with movies made more recently.  Because the dataset contains movies from a wide range of dates, this feature might not be that useful in creating a model using this particular dataset.  However, it would definitely be worth considering using this feature in a model with a set based off of only more recent movies.
 	 	 
Next, I looked at how well the plot keywords could predict movie profits.  The graph below shows that these keywords have an abysmal predictive ability. I tried a range of words and got very similar results each time.

![keywords linear regression](https://user-images.githubusercontent.com/83561268/132297470-184e69db-bccc-4685-9af0-a5607c43bd84.PNG)
 
Finally, I tried a model with the most predictive features from the previous models.  I tried adding and removing various features. The best model I was able to make used:

•	These content ratings: PG,  G,  R, PG-13
•	These genres: Thriller, Fantasy, Animation, Family, Action, Drama, Sci-Fi, Crime, Adventure, Romance
•	The counts of the number of movies that the director and actors were in
•	These additional features: duration, facenumber_in_poster, genre_count
 
![combined features linear regression](https://user-images.githubusercontent.com/83561268/132297557-2595b64e-45e5-4a1f-b3d5-d90af21f4ddb.PNG)

The combined features produced better results than any of the individual sets that I had tried.  However, the coefficient of determination is pretty low. 

Since the goal is to determine what movie producers can do to make a successful movie, it will be imporant to see exactly which variables are more likely to lead to success. Using linear regression provided some good clues about which features influence movie success. Genre, number of movies a person was in, duration and 'face_number_in_poster' are likely to have some influence on profits. However, it doesn't tell exactly which genres or if there is a connection between particular genres and content ratings. To find that out, I will be using a decision tree algorithm and looking at the textual representation of the tree produced.  You can read about it [here]().

[Here](https://github.com/MariannBea/Movie-Studio-Analysis/blob/43cb71c1faf238a93734623185c424611396ffa3/Notebooks/Movies%20-%20Linear%20Regression.ipynb) is the code I used for the linear regression analysis.
