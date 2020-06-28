# Predicting high school performance with Naive Bayes and Random Forests

## Background

## Dataset
The dataset was taken from the UCI Machine Learning Repository. It contains information about students and their academic performance, collected at two secondary schools in Portugal through student surveys and performance records. More specificaly, it contians the following records:

* General information about the students:
    * Student's school (binary: 'GP' - Gabriel Pereira or 'MS' - Mousinho da Silveira)
    * Student's sex (binary: 'F' - female or 'M' - male)
    * Student's age (numeric)
    * Student's home address type (binary: 'U' - urban or 'R' - rural)
    * Number of past class failures (numeric: n if 1<=n<3, else 4)
    * Number of school absences (numeric: from 0 to 93)
* Family information:
    * Family size (binary: 'LE3' - less or equal to 3 or 'GT3' - greater than 3)
    * Parent's cohabitation status (binary: 'T' - living together or 'A' - apart)
    * Mother's education (numeric: 0 - none, 1 - primary education (4th grade), 2 - 5th to 9th grade, 3 - secondary education or 4 - higher education)
    * Father's education (numeric: 0 - none, 1 - primary education (4th grade), 2 - 5th to 9th grade, 3 - secondary education or 4 - higher education)
    * Mother's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g. administrative or police), 'at_home' or 'other')
    * Father's job (nominal: 'teacher', 'health' care related, civil 'services' (e.g. administrative or police), 'at_home' or 'other')
    * Student's guardian (nominal: 'mother', 'father' or 'other')
* Student's academic and personal life
    * Whether the student wants to take higher education (binary: yes or no)
    * Whether the student is in a a romantic relationship (binary: yes or no)
    * Quality of family relationships (numeric: from 1 - very bad to 5 - excellent)
    * Free time after school (numeric: from 1 - very low to 5 - very high)
    * Going out with friends (numeric: from 1 - very low to 5 - very high)
    * Workday alcohol consumption (numeric: from 1 - very low to 5 - very high)
    * Weekend alcohol consumption (numeric: from 1 - very low to 5 - very high)
    * Weekly study time (numeric: 1 - <2 hours, 2 - 2 to 5 hours, 3 - 5 to 10 hours, or 4 - >10 hours)
    * Extra educational support (binary: yes or no)
    * Family educational support (binary: yes or no)
    * Extra paid classes within the course subject (binary: yes or no)
    * Engaging in extra-curricular activities (binary: yes or no)
* Miscellaneous:
    * Current health status (numeric: from 1 - very bad to 5 - very good)
    * Internet access at home (binary: yes or no)
    * Wheter the student attended nursery school (binary: yes or no)
    * Reason to choose this school (nominal: close to 'home', school 'reputation', 'course' preference or 'other')
    * Home to school travel time (numeric: 1 - <15 min., 2 - 15 to 30 min., 3 - 30 min. to 1 hour, or 4 - >1 hour)
* Grades (Maths and Portugese):
    * G1 - First period grade (numeric: from 0 to 20)
    * G2 - Second period grade (numeric: from 0 to 20)
    * G3 - Final grade (numeric: from 0 to 20)
 
### Outcome variable
We are interested in predicting G3 - the student's final year grade. An immediate thing to realise is that using the student's previous grades (G1 and G2) would make it a lot easier to predict the final grade (e.g. a student who did very well in the first two terms is likely to do similarly well in the final term). However, variations of such a model would still be useful. For example, after the first one would be interested to know how well will this student perform overall given the current performance and personal factors.

Based on this, the best course of action is to use two version of the dataset:
* All attributes including G1 but not G2
* All attributes apart form the grades (excluding bioth G1 and G2); this is a more exciting problem, although we expect it to be harder to classify

## Models
This is one of the lesser-known UCI ML datasets, and most of the existing projects treated this as a regression problem (prediciting exact grades) or a binary classification problem (will the student pass of fail?). 

A couple of notes about this:
* We are not particularly fussed about predicting the actual grade. It would be useful enough to predict more generally how well the student is likely to do. This was done in previous studies by converting G3 to a discrete range according to the Portugese grading classification:
    * 20 - Excellent with distinction and honors
    * 18 to 19.99 - Excellent
    * 16 to 17.99 - Very good
    * 14 to 15.99 - Good
    * 10 to 13.99 - Sufficient	
    * 7 to 9.99 Poor
    * 0 to 6.99 Very poor
An immediate problem with thisapproach is the high class imbalance:

!!!!!!!!!!!!!!!!!!!!!!!!!!!!IMAGES HERE!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

Clearly, the more "extreme" cases will be lost and the classifiers may not be able to learn to distinguish between them. We could balance the classes by undersampling to match the least prevalent class but that would leave a realtively small training set.

* Converting G3 to a pass/fail scale would leave
We will treat this as a multi-label classification problem, splitting the grade into three categories according to the above classification:
* 0 to 9.99 - "Very poor to poor"
* 10 to 15.99 - "Sufficient to good"
* 16 to 20 - "Very good to excellent"

This approach is good for two 
Knowing the exact grade does not 

When this dataset was used in a research paper by Cortez and Silva

## Setup and functions

## References
Portugal Secondary and Higher Education Grading: https://www.portugaleducation.info/education-system/grading-system-academic-year-and-language-of-instruction.html

P. Cortez and A. Silva. Using Data Mining to Predict Secondary School Student Performance. In A. Brito and J. Teixeira Eds., Proceedings of 5th FUture BUsiness TEChnology Conference (FUBUTEC 2008) pp. 5-12, Porto, Portugal, April, 2008.
