---
title: Making Money From Movies - Step 4, Part 2
date: 2021-09-09 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Machine Learning
tags:
  - Python
  - Linear Regression
---
#### Making Money From Movies - Step 4: Machine Learning Models
This is the fifth entry in a series about using machine learning models to predict movie success.  You can find the first entry [here](https://mariannbea.github.io/machine%20learning/movie-studio-profits-inspecting-the-data/). In previous posts, I discussed how I cleaned the data, did exploratory data analysis and used linear regression to predict movie profits. The aim of this series is to answer the following questions:

1.	Is there a correlation between genre and profits?
2.	Is there a correlation between content rating and profits?
3.	Are some genres more profitable for specific content ratings?
4.	Does an increase in the number of Facebook likes for directors or actors correlate with increased profits?
5.	Is being in or directing a greater number of movies correlated with more profits?
6.	Are some topics correlated with more profits?

##### Decision Trees

The Decision Tree algorithm classifies data instances into different categories. Its accuracy can be measured using both an accuracy score and a confusion matrix.  The accuracy score ranges between 0 - 1 and indicates what percentage of the instances were correctly classified. 0 means that none of the instances were correctly classified, and 1 means 100% of them were classified into the correct category. However, this score can be misleading. A high accuracy score can sometimes be achieved by merely assigning all of the examples under the most common category. This is particularly likely in a dataset where the number of data points in each category is imbalanced. The confusion matrix can be used to get a better idea of how the accuracy score is obtained. This matrix shows how many instances of each category were classified correctly. It also indicates under which category the incorrectly placed data points were categorized. The image below shows why a confusion matrix is necessary. As you can see, the accuracy score is about 52%, but this was achieved by categorizing most instances under "Some Profits." This isn't particularly helpful for determining which features help make a movie more profitable than the norm.

![Confusion Matrix](https://user-images.githubusercontent.com/83561268/133950510-c571724e-1c9b-4150-a9b4-c2360969e98e.PNG)

The true benefit of the decision tree algorithm is it gives valuable information about how the various features related to each other affect the results. Along with the accuracy score and decision matrix, it is possible to print out a visual representation of the tree.  By looking carefully at this representation, it is possible to determine which features are more likely to lead to a specific categorization with more precision. 

![Decision Tree](https://user-images.githubusercontent.com/83561268/133950856-752dd04a-240f-469c-9b74-5911eed7dccc.PNG)

For example, in the image above, you can see that adventure movies that do not contain animation are likely to make some profits. However, those that include animation are likely to succeed. Go further down the tree, and you can see that adventure movies that contain action are likely to be a success whether or not they are also classified as thrillers. Adding more features to the decision tree allows an even better analysis of how these features interact and which conditions make high movie profits more likely.  The linear regression models I ran showed a slight correlation between genre and profits. A decision tree might provide better results and give more information about which combinations of genres, content ratings, and budget allocations result in more profits.

I started by looking at genre.  I first tried all genres rather than just selected ones that looked like they correlated with very successful or unsuccessful movies. I was very excited to see an accuracy score of 53% on the first try, as this was the highest score I had seen for this data set.  However, looking more carefully at the confusion matrix showed that most movies had been classified under "some profits." Unfortunately, the high accuracy did not indicate a model that was strong at predicting movie success.

![pict 1 results without over and under sampling](https://user-images.githubusercontent.com/83561268/132425843-f7765295-e89c-4a8f-bbe6-2cd846a3d676.PNG)

This was most likely due to the imbalance between the categories.  I decided to use SMOTE sampling to try to balance them out and get more predictive results.  While reading more about using SMOTE in python, I came across an [article]( https://machinelearningmastery.com/combine-oversampling-and-undersampling-for-imbalanced-classification/) written by Jason Brownlee on Machine Learning Mastery about using both under and oversampling together.  I had used this method before when analyzing data with Weka and had a lot of success, so I decided to use it here. 

```python
over = SMOTE(sampling_strategy={"Success": 600 ,"Failure": 550})
under = RandomUnderSampler(sampling_strategy = {"Some Profits": 600})
steps = [('o', over), ('u', under)]
pipeline = Pipeline(steps=steps)
```
Using SMOTE and undersampling reduced the accuracy score of the model a bit. However, it predicted more failures and successes correctly. It is probably a more useful model, but there is still room for improvement.

![pict 2 results with over and under sampling](https://user-images.githubusercontent.com/83561268/132425847-2022d537-3776-4180-94d1-ca36f83bfba5.PNG)

Next, I looked at content ratings.  Once again, I used SMOTE and undersampling.  However, this time it was difficult to get good predictive results.  If I weighted the categories evenly, the model predicted most instances as "Some profits" or "Successful". 

![pict3, profits or successful confusion matrix](https://user-images.githubusercontent.com/83561268/132425852-de851f30-93d7-4a7c-9d80-3c08c7823cdc.PNG)

If I tried weighing "Failures" a bit higher, all instances were categorized as either "Failure" or "Successful".  

![failure and successful confusion matrix](https://user-images.githubusercontent.com/83561268/132425859-603fb0b3-b09d-47bb-b11e-402b3edf5d5e.PNG)

After experimenting for quite a while, I decided that it was impossible to get good results using content ratings alone, so I combined them with genre.  This had a reasonable, but not great, accuracy rate. The textual decision tree gave some indications of combinations that predicted either success or failure.

![genre-content rating visualization](https://user-images.githubusercontent.com/83561268/132425867-e756a804-8bfd-4158-b49f-55673b71adeb.PNG)

![genre-content rating confusion matrix](https://user-images.githubusercontent.com/83561268/132425877-10573750-92d7-452a-bd56-12cfb87304d9.PNG)

I also tried a decision tree with the plot keywords selected through the bag of words. Unfortunately, this suffered from the same issue as creating a decision tree model with just the content ratings.  Depending on how the over-sampling and under-sampling were chosen, one or two categories always took precedence over the others.
![plot keywords confusion matrix](https://user-images.githubusercontent.com/83561268/132425917-5021b101-4845-442e-9d78-bd1e440712e4.PNG)

For the final decision tree model, I experimented with changing many of the variables. I started including all genres, content ratings, Facebook likes, number of movies acted/directed in, duration and budget quartile.  I then added and took away various features to see the impact on the results. The best results were obtained using selected genres, content rating, budget quartile and, surprisingly, 'face number in poster'. Looking more carefully at the tree, it indicated many of the same genre-content rating combinations being more likely to be successful.  However, it also gave additional information.  Movies that had a budget that was about the 87th percentile were significantly more likely to be successful. In general, fewer faces in posters correlates with more success as well.  The one exception to this, at least according to the decision tree, was action-fantasy movies. This gave an accuracy score of 52%.

![final decision tree confusion matrix](https://user-images.githubusercontent.com/83561268/132425923-5be786d8-7a78-48bc-a5b2-4ac3fa4033ea.PNG)

This was very similar to the 'bingo accuracy' results found by Mahmud Q, Shuchi N, Tawsif F, et al. in a study about predicting movies using machine learning. [3] Lash M. and Zhao K. achieved much better results by adding extra data such as the movie release date and actor salaries. [2] This might be something to explore in the future. 

[Here](https://github.com/MariannBea/Movie-Studio-Analysis/blob/e5d2e5f134100b56a835581371772b68c18c172b/Notebooks/Movies%20-%20Decision%20Tree.ipynb) is the code I used for the decision tree analysis.

#### Resources

[2]	M. T. Lash and K. Zhao, "Early Predictions of Movie Success: The Who, What, and When of Profitability," Journal of Management Information Systems, vol. 33, no. 3, pp. 874–903, Jul. 2016, doi: 10.1080/07421222.2016.1243969.

[3]	Q. I. Mahmud, N. Z. Shuchi, F. M. Tawsif, A. Mohaimen, and A. Tasnim, "A machine learning approach to predict movie revenue based on pre-released movie metadata," Journal of Computer Science, vol. 16, no. 6, pp. 749–767, 2020, doi: 10.3844/JCSSP.2020.749.767.

How to Combine Oversampling and Undersampling for Imbalanced Classification by Jason Brownlee on [Machine Learning Mastery](https://machinelearningmastery.com/combine-oversampling-and-undersampling-for-imbalanced-classification)
