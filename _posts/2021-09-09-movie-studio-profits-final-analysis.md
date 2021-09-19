---
title: Making Money From Movies - Analysis
date: 2021-09-12 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Machine Learning
tags:
  - Python
  - Analysis
  - standard
---

For now, let's look at the questions we started with and see if what we have learned.

1.	Is there a correlation between genre and profits?

    Some genres seem to be correlated with higher profits. However, there are some subtleties involved. Adventure appears to be linked to a greater likelihood of movie success. However, this is always the case. Combined with some genres, such as romance or animation, it is more likely to lose money.  Animation and Action Movies are also more likely to be linked to greater profits but, just like with Adventure movies, it depends on the exact combinations.

2.	Is there a correlation between content rating and profits?

   	Looking at the information from the exploratory data analysis, it appears that there is some connection. Content ratings combined with genre did seem to have some predictive ability. However, content ratings alone were not overly predictive in either of the machine learning algorithsm tried. 

3.   Are some genres more profitable for specific content ratings?

    Based on the decision tree model, it appears some genres are more profitable only when linked with particular content ratings. For example, action movies that are rated PG-13 and adventure movies not rated R.

4.	Does an increase in the number of Facebook likes for directors or actors correlate with increased profits?

    There is a slight correlation between these two variables, which has become stronger over time.  It would be something to look more closely at with a greater range of more recent movies.

5.	Is being in or directing a greater number of movies correlated with more profits? 

    There seems to be a correlation between participation in more movies and profits. However, being in more movies appears to make a difference only up to a point.

6.	Are some topics correlated with more profits?

    I had predicted that there would be a correlation between plot keywords and profits. The bag-of-words analysis was able to make a prediction that linked keywords to different profit categories. It found different words each time it ran; however, some words matched with success or failure fairly consistently. I was surprised to see that even using only these words had no impact on any models I tried.

Based on my observations, if I was going to recommend a strategy for producing a successful movie based on the results of the this analysis, I would suggest an action movie appropriate for children. A high budget and making sure there were only a few faces in the movie posters would help as well.  Based on the linear regression models and exploratory data analysis, it couldn't hurt to look for at least some participants that have been in a few movies and are popular on Facebook. It probably wouldn't hurt to make it an epic and, just to be safe, leave out the drugs.
