---
title: "Data, Data Everywhere: How to Make Sense of It All?"
date: 2021-11-25 13:32:20 +0300
excerpt_separator: "<!--more-->"
categories:
  - Data Analysis
tags:
  - Python
  - Analysis
  - SQL
---
This is part of a series about analyzing how the use of Online Learning Platforms was affected by Covid.
You can read the first post [here](https://mariannbea.github.io/covid-impact-on-education/).

I chose to work on a project related to Covid and Learning because of my experience working as a teacher during the pandemic. This project was inspired by a Kaggle Competition sponsored by Learn Platform, and much of the data used came from that competition.

After quickly looking through the data, these were the initial questions I thought I might be able to answer:

*  How does engagement change during online and offline learning?
*  Does engagement have an effect on student achievement levels?
*  How were student achievement levels affected by periods of online learning?
*  Is there are correlation between any demographic factors and engagement with online platforms?
*  Which programs had the most engagement?
*  Is there are correlation between extensive use of any of the programs and student achievement?

However, before I could answer these questions, I needed to better understand the data I had and find additional data that would help answer the questions.

Looking at the data, the first thing that became apparent was that it was more data than I had ever worked with before. Two smaller files contained information about the school districts and programs present in the data. One had basic demographic information about the communities where the data was collected. The other included information about the names and purposes of the programs. These were similar to the types of data I had previously used. However, the engagement data was not. It was a set of 233 files, and each file contained information about the programs used every day in 2020 for each school in the district. 

At first, I was unsure where to even begin with cleaning the data. Obviously, I wouldn’t be able to look at every single file and check for errors, and I wasn’t sure how to go about it at first. So I started with the district and program data.

The district file contained the most missing data. Quite a few of the districts had no demographic information at all. My first inclination was to disregard these districts. However, sometimes the pattern in which data is missing can also give valuable information. For example, perhaps most of the absent demographic information came from communities that used the most online resources. That might be a clue that a particular type of district removed their demographic information before it was shared.  I decided to keep the data and analyze these districts as a separate group.

Looking next at the program data, I noticed that a few of the programs in the program data were missing information about what sector they served and their function. Most of the programs that were missing this data were general programs like Youtube and Adobe used by most people. It didn’t seem like this missing information would affect the results as much as the missing demographics information. However, I was familiar with almost all of the programs and not many were missing, so I decided to add this data manually.

Finally, I opened a random selection of the engagement data. Based on the files I opened, it appeared there was information from every day of the year.  Each of the files had complete data for days, program id and percent access, and all had left the engagement index field blank when the percent access was zero for the day.  There were vast differences in the program use between the different files I opened. I decided that cleaning this data would have to be done after I had a better way to process it. This meant that I would need to create an SQL database to store it. However, before I got started on that, I decided to see what other data I could find that might help answer some of my questions. 

One of the questions I was most interested in answering was if there was a correlation between using Digital Platforms and student achievement. So, I decided to start by looking for student assessment data. From my own personal experience, I saw how students’ educational experience in one state can vary significantly from district to district. So, I would have liked to compare outcomes by school district. This would have given the most accurate picture of how the use of online platforms was influenced by school closures and district-level decisions. It would have also allowed for a more precise analysis of the correlation between the use of EdTech and student achievement. However, the data providers had purposefully removed data to anonymize the districts. It was decided not to attempt to determine which data were linked to which actual communities for ethical reasons. Instead, outcomes would be compared on a state-by-state basis.
 
I created a quick pivot table in Excel to determine which states to include. I had initially intended to include states with over 10 districts. This would be more likely to include a broader range of demographics and types of schools. ![picture of pivot table](https://user-images.githubusercontent.com/83561268/160224449-76f87a72-6bbe-4153-9d85-e410b6e16037.PNG) However, there were only 7 states with information for more than 10 districts in the data. This didn’t seem enough, so I included states with more than 5 districts. This was not ideal, but it was the best I would be able to do with the data I had. I had also intended to investigate whether there were any differences between districts in rural areas, suburban areas, or towns. However, creating a new pivot table made it apparent that this was not a viable option for this dataset. ![picture of pivot table with city type](https://user-images.githubusercontent.com/83561268/160224476-1a060ece-2ea9-420c-aff1-c9ff052c11b6.PNG)

Finding data was much more manageable after I knew which states I would include in the analysis. In fact, I found a lot more data than it made sense to include. In the end, I decided to use data about:

* each state’s school technology plans
*  student assessment scores
*  school culture
*  school calendars showing holidays 
* data about how the method of instruction changed after Covid arrived in America. 

Most of the data was quick and easy to clean and transform. The one exception to this was the school’s technology plans. That took a lot more time and effort, which is what the focus of the next post will be about. 

Once I had the data prepared, I designed an SQL database to store it. This had the advantage of helping to ensure the data was in the appropriate format as it was added to the database. This was one of the ways that I caught some errors in the engagement data. It also allowed me to easily combine the data from different sources to analyze through creating queries for data as I needed it. With the data cleaned and ready to use, it was time to analyze it.

![sqlModelpict](https://user-images.githubusercontent.com/83561268/160225717-f6b4b08d-4c73-45ce-bca6-27da98a98a45.png)

Data Sources used in this project:

[Kaggle Data]( https://www.kaggle.com/c/learnplatform-covid19-impact-on-digital-learning) 
[School Culture Data](https://nces.ed.gov/)
[School Assessment Data]( https://www.nationsreportcard.gov/ndecore/landing)
[Data About School Delivery Models](https://www.covidschooldatahub.com/states/illinois)

The school technology plans that were analyzed can be found in![this]() folder.
diff --git a/_posts/2021-12-20-turning-plans-into-data.md b/_posts/2021-12-20-turning-plans-into-data.md
