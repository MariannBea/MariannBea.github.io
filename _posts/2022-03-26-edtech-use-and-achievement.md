---
title: "Is There A Correlation Between EdTech and Achievement?"
date: 2021-12-20 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Data Analysis
tags:
  - Python
  - Analysis
  - Natural Language Processing
---
This is part of a series about analyzing how the use of Online Learning Platforms was affected by Covid.
You can read the first post [here](https://mariannbea.github.io/covid-impact-on-education/).

After obtaining additional data, I modified some of the questions that I aimed to answer and added some additional ones. Here are the final questions that I am hoping to answer through analysis:

#### Questions This Project Aims To Answer

* Do states with higher student achievement on the 2019 NAEP reading and math assessments have more online engagement in 2020?

* Is there a correlation between a states' technology plan/curriculum content and online engagement?

* Are any district technology development plan features correlated with achievement on the 2019 NAEP at grades 4, 8?

* Are any features of a school's culture correlated with more or less use of Edtech platforms?

* Which products are used most in states with higher achievement rates on the 2019 NAEP reading and math assessments?

* Which programs had the most engagement in each state?

* Is there an increase or a decrease in online product activity during online learning?

* What is the correlation between each demographic factor and engagement with online platforms?

Follow-up for later:  Are high levels of engagement with any particular programs correlated with high levels of achievement on the 2021 NAEP reading and maths assessments? 

This post will look at what I learned about whether states with higher student achievement in 2019 have more online engagement in 2020. Ideally, I would have looked at how students achieved at the end of the 19-20 or 20-21 school years. However, due to the difficult school situation, no nationwide standardized tests were given to public school students at the end of these years. There will be a new NAEP assessment at the end of this year, so this might be something to investigate in the future.

Before I could investigate if there was any correlation between test scores and online engagement, I needed to see how the students in each state performed on the national assessment. To better understand this, I created bar graphs showing achievement in each state against the national average.

![bar graph](https://user-images.githubusercontent.com/83561268/160241745-624cb91e-5ef4-4971-874a-c8cfc0711eeb.PNG)

The graph made it easy to see that Massachusetts outperforms all other states in the study in all four assessments. Massachusetts, Indiana, Utah, Connecticut and Ohio were at or above the national average in all examinations. California was the only state below the national average in all four areas. However, New York did not perform that much better. It is also apparent that there are no vast differences in achievement between any states, except for Massachusetts.

I used linear regression to see if there was a correlation between test scores and online engagement. I compared test scores to the average engagement index for each state. I was surprised to see a slight negative correlation between digital platform engagement and student achievement. However, there was a considerable error rate, which indicates that the amount of online engagement does not have much influence on student achievement.

![corr](https://user-images.githubusercontent.com/83561268/160242130-6fcec481-09ed-479f-94f7-f91045e5c434.PNG)

I have read a lot about best practices in technology use and how it supports student achievement. So, these results raised many questions for me. Is there a positive correlation between some platforms and a negative correlation between others? Does the manner how technology is used? For example, is there a difference if students mainly use technology to create and research vs doing rote practice or playing learning games. Were these results due to the minimal number of examples? Only 10 states were being considered, after all. Maybe the results would be different with a broader sample. 

So I decided to look closer at the data. I plotted the achievement scores against the average engagement index for each state. Looking at this visual, it was apparent that states that used more digital resources were not always the ones with higher achievement scores.

![segment plot](https://user-images.githubusercontent.com/83561268/160243031-9139a399-3012-49d6-8b6b-51837b4ae1f3.PNG)

I was so intrigued by these results I started reading more research to see if others had found similar results. Based on what other researchers have found, my first inclination was correct. Some types of technology and some ways of using them have been correlated with increased student achievement. In contrast, others have been associated with decreased achievement.

What I learned through reading research inspired me to look a bit deeper at the data. First, I looked at the correlation between each subject and online engagement. This showed a positive correlation between fourth-grade reading scores and engagement in digital resources. There was a negative correlation between the other assessments and digital resources. 

![subject correlations](https://user-images.githubusercontent.com/83561268/160243007-21817321-75a9-49fb-9e15-329329fc1f60.PNG)

Then I looked for a correlation between any particular digital platforms. It turns out that there was a positive correlation between some EdTech tools and assessment scores and a negative correlation between other tools and assessment scores. 

![ed tech correlations](https://user-images.githubusercontent.com/83561268/160279277-4b2a0483-d78d-46a5-aab8-d608d455e0f0.PNG)

I looked over the different platforms in each category to see if I could distinguish factors that might differentiate between the two. I was not familiar with all of the platforms, so I probably missed some insights. However, I noticed that many of the programs positively correlated with achievement had one of these characteristics:

* used for research
* used for teacher professional development
* used to share or improve writing
* used for collaboration
* make math interactive or relate it to real-contexts
* websites for educational publishing companies
* make whole class lessons more interactive by playing games that formatively assess understanding during the lesson

Many of those that were negatively associated with achievement shared these characteristics:

* aimed towards elementary students
* replicated worksheets in game form (rote learning, but gamified)
* used for remediation when students were struggling
* involved reading books digitally
* used for behavior management
* provided worksheets for teachers to print and use with students

However, it should not be assumed that correlation implies causation. For example, schools with limited resources might use digital books more often to expand their students' access to different types of books. Teachers might use worksheet websites because their school lacks an explicit curriculum or materials for students to practice what they learn. Both indicate a lack of resources, which could mean the teachers don't have everything they need to provide the best quality education for students. This might be the actual cause for lower achievement. If this were the case, simply using those resources correlated with positive achievement in this analysis would likely not impact student achievement.

Several research studies have been done about the impact of technology use in on student achievement. This analysis supports what many have found: some types of Edtech support student achievement better than others. However, the lists created by this analysis should not form the basis of decisions on which digital media to use in a classroom. On the other hand, this analysis could provide a reason to look more carefully at how technology is used in education.

#### References

Bryant, J., Child, F., Dorn, E., & Hall, S. (2020). New global data reveal education technology’s impact on learning.


Comi, S. L., Argentin, G., Gui, M., Origo, F., & Pagani, L. (2017). Is it the way they use it? Teachers, ICT and student achievement. Economics of Education Review, 56, 24–39. https://doi.org/10.1016/j.econedurev.2016.11.007


Han, I., Byun, S. yong, & Shin, W. S. (2018). A comparative study of factors associated with technology-enabled learning between the United States and South Korea. Educational Technology Research and Development, 66(5), 1303–1320. https://doi.org/10.1007/s11423-018-9612-z


Lee, D., Huh, Y., Lin, C. Y., Reigeluth, C. M., & Lee, E. (2021). Differences in personalized learning practice and technology use in high- and low-performing learner-centered schools in the United States. Educational Technology Research and Development, 69(2), 1221–1245. https://doi.org/10.1007/s11423-021-09937-y


Walker, S. K. (2019). ‘It Depends’: Technology Use by Parent and Family Educators in the United States. Education Sciences, 9(4). https://doi.org/10.3390/educsci9040293
 


