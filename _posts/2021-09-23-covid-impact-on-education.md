
#### Covid's Impact on Education

I was in Beijing getting ready to enjoy a Chinese New Year holiday when I first heard of Covid.  As the parents of the students in my class came to pick their children, they told me to be careful. They said I shouldn't travel during the break because there was a new disease in China and to stay inside as much as possible. At first, I thought they were overreacting. It turns out they weren't. I watched in horror as the Covid numbers went from a little over 800 to over 10000 in a week. I continued to watch in the following weeks as the numbers rose exponentially.  More and more people seemed to be going into the hospital, but no one was coming out. More and more people seemed to be dying, though. I started to get nervous.

Soon our school was closed indefinitely, and we began online learning. By the end of the next month, there were 100,000 cases, and Covid was detected in other countries. I have continued to follow the effect that Covid has had around the world, regularly reading about how different societies have reacted to it and how it is has affected the people living there. As a teacher, I have also been particularly interested in its effect on students and teachers. 

In August of 2020, my school began in-person learning again. For most of the students, it was the first time they had been in a class with their peers in 8 months. The students I teach come from well-off families, and most had many hours of additional tutoring during online learning. As a result, we didn't notice a negative impact on most students' academic achievement. However, many teachers noticed a difference in the students' ability to interact socially with others. It wasn't until the very end of the school year that I started noticing my students making significant progress in their ability to deal with conflicts in social situations. I can only imagine how online learning, and the experience of living in a pandemic, affected students much less fortunate than the ones at the school where I teach.

Because of my intense interest in this topic, when I was ready to work on my second independent project, I looked for something related to Covid and learning.  I soon found a [competition](https://www.kaggle.com/c/learnplatform-covid19-impact-on-digital-learning/code) on Kaggle that involved analyzing how Covid affected digital learning. I discovered this project far too late to enter it, but because it looked so interesting, I decided to use the data to see what I could find out.

#### Initial Observations

The data on the Kaggle website consisted of three main types of information:
*    A csv file of some basic demographic information about the districts where the data was collected. 
*    A csv file containing information about the various programs used by the school 
*    A set of 233 engagement files, each showing information about programs used each day for 2020.

After downloading the data, the first thing that I did was open the district and program information files and look at them. I also opened a random selection of the district files. My first impression of the data was that it was very well structured, and there seemed to be very little missing data.  

The district file contained the most missing data. Quite a few of the districts had no demographic information at all. My first inclination was to disregard these districts. However, sometimes the pattern in which data is missing can also give valuable information. For example, perhaps most of the communities that are missing demographic information use the most online resources. That might be a clue that the most affluent districts removed their demographic information before it was shared.  I decided to keep the data and analyze these districts as a separate group in some analyses.
Looking next at the program data, I noticed that a few of the programs in the program data were missing information about what sector they served and their function. Most of the programs that were missing this data were general programs like Youtube and Adobe that are used by most people. It didn't seem like this missing information would affect the results as much as the missing demographics information. 

Finally, I opened a random selection of the engagement data. Based on the files I opened, it appeared that there was information from every day of the year.  Each of the files had complete data for days, program id and percent access, and all had left the engagement index field blank when the percent access was zero for the day.  There were vast differences in the program use between the different files I opened. 

From just this quick glance at the data, here are some questions that I would like to investigate:
*  How does engagement change during online and offline learning?
*  Does engagement have an effect on student achievement levels?
*  How were student achievement levels affected by periods of online learning?
*  Is there are correlation between any of the demographic factors and engagement with online platforms?
*  Which programs had the most engagement?
*  Is there are correlation between extensive use of any of the programs and student achievement?

I will likely develop more questions as I explore the data further. Based on my questions, I will need to obtain more data about when different states had online and in-person learning. I will also need to see if I can find achievement data.  However, since it is not possible to identify which districts are indicated by the numbers given, I am not sure that I will be able to answer some of the questions about achievement.  I will have to see what information is publicly available.  Hopefully, the information I find will help me to answer at least some of the questions about achievement.
