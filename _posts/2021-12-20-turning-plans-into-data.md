title: "Turning Technology Plans into to Usable Data"
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
You can read the first post [here]<https://mariannbea.github.io/covid-impact-on-education/>.

In my last post, I wrote about finding data to help me answer questions about the use of digital learning platforms in schools. Much of this data led to more general questions about learning and technology use. One of the questions was about the impact that a state's technology plans had on the use of digital platforms. I wanted to investigate if any particular focuses were correlated with more engagement with Edtech. I also wanted to see if there was any correlation between the content of these plans and student achievement. 

For most states, the technology plans I found consisted of documents outlining how they would improve technology use over time. Unfortunately, I could not locate identical information for every state, so I chose to use the most relevant document I could find. When selecting which text to use for each state, I tried to find the most recent one that outlined a plan for improving technology use in the state. If this was not available, I chose the most recent document that included the technology curriculum (as these also tended to talk about what was necessary for students to learn). For Indiana, I used a PowerPoint outlining progress with technology development as this was the only thing that could be found. If this were an official study, I would have contacted each state's education department. However, in this case, I decided to use what I could find.

After I had obtained the documents, I needed to change them from unstructured to structured data. To do this, I decided to create a spreadsheet that recorded which aspects of learning each state focused on in their documents. The assumption was that if something was included in their technology plan or curriculum, it was likely to be seen as important by the state's educators and educational administrators. First, I skimmed each item and wrote down keywords linked to features that seemed like they might have an impact on student achievement.

These were the original key words I found:

flexible  
for_assess  
goals 
home_access   investment  
one_to_one  
professional_development
privacy   problem_solving 
learning_communities
shared_resources  
personalized_learning standards 
student_centered
tech_Leader 
integration tech_lit  
state_wide_goals
as_learning_tool

I also included the year created as it indicated how long the state had been working on those particular goals. I suspected that this could impact student use of digital platforms. 

Then I used a text rank algorithm with bag of words to find other vital words.

Before using the algorithm, I cleaned the text by removing stop words and all entities. I included terms like district, educational and grade as stop words. These were very common and not likely to be specifically related to a concept that would affect online use. I removed all entities to avoid finding keywords that were names of people or states. 

![remove stop words](https://user-images.githubusercontent.com/83561268/160231216-ed76ec31-c41c-46a2-b859-96c8cbc6d9fa.PNG)

Then I ensured that all of the words to be ranked were at least 30 characters and ranked above 0.003.

![phrase selections](https://user-images.githubusercontent.com/83561268/160231221-94b75b4a-0405-4af7-a370-de24bf6c3deb.PNG)

Next, I used topic modeling to look for topics in each text. 

![topic modelling](https://user-images.githubusercontent.com/83561268/160231241-1ccc5bf1-f80d-4adb-817c-c83a20c4492c.PNG)

I chose the most relevant phrases from each topic based on my experience as an educator.

After that, I used Python to check for the keywords in each state's documents. Their presence, or lack of, in a technology document was indicated by using 1 for the term was present, and 0 for it was not.  

![document scanning](https://user-images.githubusercontent.com/83561268/160231253-0bfdf9fd-324f-4114-a49c-ae744688abf6.PNG")

I then condensed some of the key phrases into the following concepts: 
        
* __21st_century:__ talks about preparing students for 21st century/developing 21st century skills 
* __address_gaps:__ specific plan to address gaps in school provision of technology
* __authentic:__ recommends using technology in authentic contexts
* __collaboration:__ one goal of technology use is collaboration  
* __comp_sci_ed:__ specific focus on computer science skills such as programming
* __data_driven:__ specifically talks about using data to drive/plan instruction
* __data_protection:__ mentions protecting student data
* __digital_citizenship:__ mentions digital citizenship or teaching skills that encourage good digital citizenship
* __local_control:__ encourages or requires schools or districts to develop their own technology use plans
* __equity:__ goal of increasing equity related to technology use
* __flexible:__ mentions the need for flexibility in teaching to allow for the use of technology
* __for_assess:__ encourages/requires technology to be used for assessment  
* __goals:__ has specific goals around technology use (including developing infrastructure, pd)
* __home_access:__ goals related to increasing home access to technology
* __integration:__ states use of technology should be integrated into other instruction
* __investment:__ goal of more investment into technology resources or infrastructure 
* __one_to_one:__ goal of one device per student
* __pd:__ goal of providing professional development for technology integration or teaching 
* __personalized_learning:__ one goal of technology use is to provide more personalized learning experiences
* __privacy:__ mentions the importance of protecting student privacy
* __problem_solving:__ encourages/requires technology to be used to promote problem-solving skills
* __learning_communities:__ encourages/provides for the development of professional learning communities
* __shared_resources:__ goal/provision of state-wide shared resources to promote digital learning 
* __standards:__ has or developing technology skills standards
* __student_centered:__ promotes student-centered teaching  
* __tech_Leader:__ provides for a technology leader at the school/state or district level  
* __tech_lit:__ mentions the importance of developing technology literacy skills
* __state_wide_goals:__ has state-wide technology development goals
* __as_learning_tool:__ primary focus is the use of technology as a tool for learning, not a subject to teach
* __year:__ year document used was created

Finally, I carefully read the documents to see if they talked about the concepts while not directly using any keywords. For example, a teacher would understand all of the phrases in the picture below to mean "authentic learning", even though those words are very explicitly stated.

![authentic](https://user-images.githubusercontent.com/83561268/160231259-d4492d33-eb95-4b57-a38a-3a54a1b58916.PNG)

I updated the spreadsheet as appropriate. Now that the data was structured, I would be able to use it to determine if there was a correlation between technology documents and student learning.



