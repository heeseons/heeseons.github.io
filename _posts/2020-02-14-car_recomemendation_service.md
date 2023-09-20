---
title: '[Prj] Car Recommendation Service using Filtered Review Data'
categories: [Data Science, Machine Learning]
tags: [nlp, text analysis, svm]
math: 'True'
img_path: "/assets/img/posting"
pin: true
---

<div align=left>
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/PyCharm-000000?logo=pycharm&logoColor=white">
  <img src="https://img.shields.io/badge/Windows-000000?logo=windows&logoColor=white">
</div>

[![Semantria](https://img.shields.io/badge/Semantria_Web-Lexaltics-green)](https://api5.semantria.com)

Received an Honorable Mention at `the 15th Korean University Student Industrial Engineering Project Competition`(2019, [KIIE](https://kiie.org))


---

# Introduction

Given the substantial upfront costs and extended usage lifecycle associated with automobile ownership, the demand for comprehensive information services in the domain of car acquisition is significant. However, challenges like intricate technical jargon and the potential propagation of misinformation underscore the necessity for data mining-driven solutions, which can provide reliable and steadfast services.
<br><br>
To address these challenges, an Analytic Hierarchy Process (AHP) analysis is employed. This analysis evaluates the pivotal criteria deemed essential by users in their quest for personalized vehicle information. The resulting weights assigned to each criterion are then seamlessly integrated, culminating in a strategic implementation blueprint for the final service. This systematic approach effectively addresses the prevailing issues and concerns.

[![GitHub](https://img.shields.io/badge/-GitHub-black?logo=github&link=https://github.com/heeseons/CarRecomSvc)](https://github.com/heeseons/CarRecomSvc/)

<br>

# Experiment

## 1. Data Collection
### 1.1. Setting the Scope of Data Collection

#### Data Type
* Qualitative Data: Review from experts and users
* Quantitative Data: Car specifications

#### Review Data Source
[Auto Portal](https://autoportal.com/), [Edmunds](https://www.edmunds.com/), LeftLane News, etc.
#### Car Type
C/D segment vehicles launched between 2016 and 2019, excluding sports cars.

### 1.2. Web Crawling
(1) Develop an automated data collection program utilizing *Selenium* and *BeautifulSoup*.\
(2) Build a database by extracting solely meaningful data.

![crawling data](2020-02-14-crawling_data.png){: width="70%" heignt="70%"}

* 358 types of car
* 1,098 reviews from experts
* 44,817 reviews from users

<br>

## 2. Filtering Data
### 2.1. Generating Embeddings with Doc2Vec (Doc-to-Vector)
To quantify qualitative review data, a preliminary step of data preprocessing is indispensable.\
Subsequently, the text data underwent a conversion process, being mapped into a **10-dimensional vector space** with the aid of the **Doc2Vec** algorithm.

![d2v result](2020-02-14-d2v_result.png){: width="70%" height="70%"}

### 2.2. Performing Classification with SVM (Support Vector Machine)
In the present experiment, we deploy an SVM classification model trained on hotel review data sourced from Kaggle.\
The model demonstrates an **accuracy of 74.33%**, effectively identifying and isolating **4,215 erroneous reviews**.

![svm result](2020-02-14-svm_result.png){: width="70%" height="70%"}

### 2.3. Characteristics of Filtered Data Identified as Inconsequential Synthetic Data

#### Filtered Data
It presents only objective facts without subjective judgments such as positive or negative biases.
> * ProPilot Assist is not exactly a self-driving feature. The system does require you to keep your hands on the steering wheel, and it will sound an alarm if you do not.
> * To enhance the interior ambiance of the 2016 Mitsubishi Outlander, the company’s product planning team specified a redesigned steering wheel as well as a new navigation and display audio system.

#### Truthful Data
It provides subjective assessments alongside objective facts, including advantages related to the vehicle's technology.
> * Mitsubishi has gotten <span style='background-color: #f1f8ff'>more aggressive</span> with the 2019 Outlander’s new look. There’s much <span style='background-color: #f1f8ff'>more visual appeal than before</span>, and the new panels work well with the Outlander’s sleek profile and crisp lines.
> * Infiniti has one of the <span style='background-color: #f1f8ff'>best-handling</span> crossovers on the road, the QX70, so the QX30 has <span style='background-color: #f1f8ff'>a high bar to jump</span>.


## 3. Conducting Sentiment Analysis using Semantria Web

### 3.1. Process
(1) Segmenting review data using commas as delimiters

(2) Configuring the predominant feature within each category for each car

|Design|Performance|...|Technology|
|:--:|:--:|--|:--:|
|Color|Drive||Display|
|Inside|Noise||Screen|
|Dashboard|Handle||Sound system|
|Height|Control||Camera|
|Style|Power||Interface|
|...|...||...|

(3) Calculating sentiment score for car features using Semantria

### 3.2. Result
There is a review of Audi A3.

> I was considering trading my 2014 S4 for a 2017 A4, but the annoying center <span style='background-color: #fff5b1'>display</span> and contradictory options packages eliminated the A4. ... As one expects of Audi, the fit and finish, <span style='background-color: #fff5b1'>inside</span> is excellent.\
Given its smaller <span style='background-color: #fff5b1'>size</span>, it may not suit those who have to carry a lot of cargo, or those who have to carry more than one passenger. It may also not be the best car for those who <span style='background-color: #fff5b1'>drive</span> a lot of highway miles, due to its short wheelbase. Overall, however, I recommend it highly to those people <span style='background-color: #fff5b1'>look</span>ing for a sporty, high quality smaller car.

|review_num|feature|sentence|
|:--:|:--:|--|
|3|display|i was considering trading my 2014 s4 ...|
|3|inside|as one expects of audi, the fit and finish ...|
|3|size|given its smaller size, it may not suit those ...|
|3|drive|it may also not be the best car for those ...|
|3|look|overall, howeber, i recommend it highly ...|

|brand|model|year|review_num|category|feature|document sentiment|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|audi|a3|2016|3|technology|display|<span style='color: red'>-0.773</span>|
|audi|a3|2016|3|design|inside|<span style='color: blue'>0.600</span>|
|audi|a3|2016|3|design|size|0|
|audi|a3|2016|3|performance|drive|<span style='color: red'>-0.620</span>|
|audi|a3|2016|3|design|look|<span style='color: blue'>0.863</span>|

<br>

## 4. Implementing Recommendation Service
### 4.1. Impementing Prototype
Create a design prototype using PyQT and then compile it into an .exe file.

![pyqt_input](2020-02-14-pyqt_input.png){: width="70%" height="70%"}
<br>

### 4.2. User Journey
(1) Input User Information\
User select their current car and 6 preference priorities(i.e. improve, same, irrelevant).

* User Input

|Model|Design|Performance|Fuel|Technology|Price|Comfort|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|OPTIMA|imporve|same|irrelevant|improve|irrelevant|improve|

* Informatin from Database

|Model|Design|Performance|Fuel|Technology|Price|Comfort|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|OPTIMA|3.1|3|3.2|3.3|3.3|2.9|

(2) Score User Requirements\
System translates user's requirements into a score value by combining input information and car information from the database.

||Design|Performance|Fuel|Technology|Price|Comfort|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|$X$|$X>3.1$|$X>=3$|$X>=0$|$X>3.3$|$X>=0$|$X>2.9$|

(3) Search for Cars that Meet the Condition\
System searches for cars that meet the requirement score condition.

|Model|Design|Performance|Fuel|Technology|Price|Comfort|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|Trax|3.2|3.2|3.4|3.3|3.4|2.9|
|CX-3|3.1|3.2|3.3|3.4|3.4|3.2|
|Sentra|3.2|3.1|3.2|3.7|3.3|3.1|

(4) Display Recommended Cars\
System recommends 3 cars and displays their characteristics intuitively using a word cloud.
![pyqt_result](2020-02-14-pyqt_result.png)
<br>

(5) Evaluate Service Satisfaction\
User select the most preferred option among the cars recommended by the system.
<br>

# Contribution
(1) Enhance the reliability of the recommendation serviceby implementing a filtering process that eliminates irrelevant data.
<br>

(2) Integrate qualitative data, such as reviews that directly assist users in their vehicle procurement decisions, with quantitative data encompassing car specifications.

<br>

---

# References
* Conroy, N. J., Rubin, V. L., & Chen, Y. (2015). Automatic deception detection: Methods for - finding fake news. Proceedings of the Association for
Information Science and Technology, 52(1), 1-4.
* Shu, K., Sliva, A., Wang, S., Tang, J., & Liu, H. (2017). Fake news detection on social media: A data mining perspective. ACM SIGKDD Explorations
Newsletter, 19(1), 22-36.
* Rubin, V., Conroy, N., Chen, Y., & Cornwell, S. (2016). Fake news or truth? using satirical cues to detect potentially misleading news. In Proceedings of
the second workshop on computational approaches to deception detection (pp. 7-17).
* Jindal, N., & Liu, B. (2007, May). Review spam detection. In Proceedings of the 16th international conference on World Wide Web (pp. 1189-1190). ACM.
* Guzella, T. S., & Caminhas, W. M. (2009). A review of machine learning approaches to spam filtering. Expert Systems with Applications, 36(7), 10206-
10222.
* Tretyakov, K. (2004, May). Machine learning techniques in spam filtering. In Data Mining Problem-oriented Seminar, MTAT (Vol. 3, No. 177, pp. 60-79).
Citeseer.
* Sculley, D., & Wachman, G. M. (2007, July). Relaxed online SVMs for spam filtering. In Proceedings of the 30th annual international ACM SIGIR
conference on Research and development in information retrieval (pp. 415-422). ACM.
* Drucker, H., Wu, D., & Vapnik, V. N. (1999). Support vector machines for spam categorization. IEEE Transactions on Neural networks, 10(5), 1048-1054.
* Hallinan, B., & Striphas, T. (2016). Recommended for you: The Netflix Prize and the production of algorithmic culture. New media &
society, 18(1), 117-137.
* [Amazon recommendation service](https://aws.amazon.com/ko/personalize/)
