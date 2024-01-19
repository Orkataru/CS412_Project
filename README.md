Table of contents

1. Introduction

1. Extracting and Storing Data

1. Preprocessing

1. Feature Engineering

1. Finalizing the Data

1. Applying Upsampling and Running the Model

**CS412 Group Project: Predicting Homework Scores with ChatGPT**

This project consists of a ML model that tries to predict the homework scores of a student based on the ChatGPT history which they used while doing the homework. By analyzing the interactions between students and ChatGPT, we explore the potential correlation between the assistance interactions and homework grades.

**Extracting and Storing Data**

- The code firstly processes the ChatGPT histories stored as HTML files and puts them in a dictionary. The dictionary stores them with the students’ ids as keys and the prompts and answers as values.
- The code then creates a separate disctionary to store just the user prompts, for easier integration into functions.
- It also stores the document names on a list for easy access later on. 
- We then create a separate list with the document names of students who got perfect scores.
- Using the stored document names, we extract text from the GPT responses, seperately storing those the belong to students with a perfect score.
- Finally, the code extracts our main labels, the student scores.


**Preprocessing**

- Preprocessing is applied to both the questions and user prompts to clean the data consisting of words. Tabs, newlines, non-ASCII words, words that only have numbers, data paths and multiple spaces are removed.
- The words that only occur once are also removed.
- The words then have Stemming and Lemitization applied to them.
- A word frequency matrix is then formed by using TF-IDF vectorizer.
- We then identify the student chats where the student score is outside of mean ± standart deviation. This is done to get rid of outliers that might harm the data. We also remove values directly equal to 100, as we use those values as the “golden standart” of one our features.

**Feature Engineering**

- Code similarity: Calculated by finding the similarity between all students and those who got perfect scores. 
- Question similarity: Calculated by finding the similarity of each student’s prompt with the questions of the assignment. This is given as a separate feature for each question.
- Average characters per prompt/response: Calculated by counting the total number of characters in a prompt/response and then at the end divided by the number of prompts/responses.
- Keyword Occurrence: Calculated by counting the number of times each keyword is found. The list of keywords is given below:

  ![Aspose Words 92108f4f-65b0-468b-8f6e-6114b7f94085 001](https://github.com/Orkataru/CS412_Project/assets/91630525/61016bce-651f-47c4-a6b2-a842149ef83e)


- Joy and Anger: Obtained by implementing a sentiment analysis tool.
- Intelligence Scored: An abstract value that represents the overall intelligence of the student, as best as possible given just the text data, uses the following metrics to get close to an objective rating:
  - Vocabulary Complexity
  - Curiosity and Inquiry
  - Engagement with Diverse Topics
  - Logical Consistency
  - Problem-Solving Skills
  - Learning and Adaptation

**Finalizing the data.**

- The code inserts all the data into the DataFrame
- The code then filters out the students that were marked to be filtered out. (Outliers and perfect scorers)
- DataFrame is then finalized and is merged with the rest of the featured.

**Applying Upsampling and running the model.**

- The code applies Manual Upsampling to the DataFrame to prevent certain small classes from being underrepresented.
- The code then uses stratified K fold to obtain a more accurate test result. Hyperparameter tuning is used alongside the K fold to get the best parameters for all the folds.
- The model is then run for all the folds, using a variety of Regression models, and is compared to the accuracies of the model initially given to us also ran with the same models. 
- The table of the results can be found below.  


Authors

Bilgehan Bilgin

Sadiq Qara

Zeynep Özgür Gün

Beste Bayhan
