---
layout: page
title: Projects
---

<div style="line-height:20%;"> <br> </div>
## 1. Difpy - Python Package for Information Diffusion Investigation in Social Networks

<span style="color:darkblue"> <em>Python, numpy, networkx, matplotlib </em></span>

<div align="center" style="width:auto; margin: 0px 0px 0px 0px; auto;" >
  <img src="assets/difpy_logo.png" width="30%" height="30%">
</div>
#### Project description:

The aim of the project is to build python package useful to investigate information diffusion in social networks.
DifPy is in early development stage. MIT licence.

Project contains modules with following features:

**initiatialize.py**

* Create random graph ready to simulation performance <br>
* Adjust existing graph <br>
* Add manually features to graph nodes <br>
* Visualize graph with information spread view <br>
* Extract graph statistics <br>

**simulate.py**
* perform one simulation step 
* perform whole simulation  
* perform simulation sequence with statistics computation  

**optimize.py**
* compute centrality for all nodes and return n nodes with best scores <br>
* perform simulation for given nodes set size with random search method and return n nodes' sets with best diffusion capability <br>


**feature_importance.py**
* Compute importance of nodes' features due to nodes information diffusion capability <br>
 
Basic information about functions usage you may read in functions docstrings.

#### Requirements:
DifPy is based mostly on NumPy, NetworkX, Matplotlib libraries. Also contemporary version of Python 3.7 + is needed. It works well in 2019.03 Anaconda environment.

#### Installation:
DifPy is available directly from the Github repository. To install DifPy, git installed on your local machine is needed. 

You may install DifPy on your local machine with the line below:

```sh
$ pip install git+git://github.com/John-smith-889/difpy.git
```
And import with the line below:
```python
import difpy as dp
```

#### To do:
* Additional optimization metaheuristics functions <br>
* Additional methods of computing diffusion speed <br>
* Implement paralell computing for better performance <br>
* Extend unit tests fot better code coverage <br>
* Test big size networks 1 million + nodes <br>
* Examples of code usage <br>
* Extended documentation <br>


#### Check more:
[Link to Github](https://github.com/John-smith-889/difpy)













<br>
## 2. Numbers' images classification

<span style="color:darkblue"> <em>Python, numpy, tensorflow, keras, scikit-learn, matplotlib </em></span>

#### Project description:

The aim of the project is to predict if number on an image is prime or composite.  
The model used in the project is Multilayer Perceptron (MLP), a kind of Artificial Neural Network. 
The model of the network was created with Tensorflow 2.0 and Keras as high level API, 
and was tuned with Scikit-learn library.
The project is based on MNIST dataset accessible [here](http://yann.lecun.com/exdb/mnist/). 
Dataset contains pictures of images which represent numbers from 0 to 9, and labels of those numbers.
There are 4 files, which divide data on 
images taining set, labels training set, images test set, and labels test set as follows:  

* train-images.idx3-ubyte <br>    
* train-labels.idx1-ubyte <br>
* t10k-images.idx3-ubyte <br>
* t10k-labels.idx1-ubyte <br>

Modified MNIST dataset has been used to build the model. '0' and '1' numbers' pictures has been deleted. 
Labels has been encoded into 0 and 1, where 0 is a prime number (2, 3, 5 or 7) and 1 is a composite number (4, 6, 8, or 9).

Project contains Jupyter Notebook file named "MNIST_binary_cls_tf.ipynb" with:

* Data exploration <br>
* Data preparation <br>
* Data modelling <br>
* Model assessment (1) <br>
* Hyperparameters tuning <br>
* Model assessment (2) <br>

#### To do:

* experiments with model's hyperparameters tuning <br>
* improve model architecture <br>
* implement Convolutional Neural Networks <br>

#### Check more:
[Link to Github](https://github.com/John-smith-889/numbers-images-recognition)












<br>
## 3. Housing Prices Modelling in Python

<span style="color:darkblue"> <em>Python, numpy, pandas, scikit-learn, xgboost, matplotlib, seaborn</em></span>

#### Project description:

The aim of the project is to analyze data and build model to predict housing prices. 
Project is based on dataset accessible on Kaggle.com [here](https://www.kaggle.com/harlfoxem/housesalesprediction). 
Dataset contains information on sold houses in King County (including Seattle) between May 2014 and May 2015. 
Variables include date of sale, price, number of beedrooms, number of beedrooms, floor area, and more.

Project contains a few Jupyter notebooks files, and each is based on following sections: 
* Data exploration <br>
* Data preparation <br>
* Data modelling <br>
* Models evaluation <br>
* Choosen model optimization <br>


Notebook named "housing_case.ipynb" is a first version of the notebook in which regression problem
of prediction each house price is solved. Results of a few algorithms are juxtaposed, where the best performance has XGBoost.

In further notebooks we operate on modified dataset. Variable 'price_bin' is constructed with values 0 and 1. 
Value of 0 means certain house is <= \$1 mln worth, value 1 means it is > \$1 mln worth. 
The rest of variables stay the same.

Notebook housing_case_2_reg.ipynb is the improved version of previous one. 
It has more expanded explanation of taking steps and results analysis, 
although the same algorithms are used. 

In the notebook housing_case_2_cls.ipynb problem of classification is approached. 
Variable 'price_bin' with values 0 and 1 is treated as target variable, and 
other variables (excluding 'price' variable - prices of houses) are treated as explanatory variables. 
Classificator version of XGBoost algorithm is used to perform binary classification.

In notebook housing_case_2_reg_MLP.ipynb the problem of regression is considered. 
Solution is prepared with Scikit-learn Multilayer Perceptron (MLP) implementation, a genre of Artificial Neural Network.


#### To do:
* \/ Experiment with Artificial Neural Networks <br>
* \/ Modify variables with binning and include date of sale as a explanatory variable <br>
* Experiment with more efficient metaheuristics during hyperparameters optimization <br>


#### Check more:
[Link to Github](https://github.com/John-smith-889/housing-prices-modelling)












<br>
## 4. Spatial Data Analysis of Taxi Vehicles' Movements in Python

<span style="color:darkblue"> <em>Python, SQL, numpy, pandas, geopandas, shapely, matplotlib </em></span>

#### Project description:

The aim of the project is to analyze spatial data of taxi fleet movements. 
Analysis include Big Query standard SQL queries, Python code for matching points with polygons, and data visualisation.
Project is based on dataset accessible on BigQuery [here](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=new_york_taxi_trips&page=dataset). 
Dataset contains information of taxi vehicles activity in New York in 2014. 

Key research questions are as following: in which day of the week there is highest transits rate, 
what were the trends of payments during the year if we take under consideration cash and a card,
what is the most popular customer's pick up place?

To acquire data a few SQL queries were performed on tlc_green_trips_2014, and taxi_zone_geom BigQuery tables. 
Queries are saved in "queries.sql" in the project repository.
Variables include pick-up datatime, pick-up longitude, pick-up latitude, payment type and more.
Polygons data of New York area was downloaded from taxi_zone_geom table.

Project contains also Python script file named "spatial_case_solution.py" with following tasks:

* Import and transform polygons data and points data <br>
* Match points to polygons with Python's shapely package <br>
* Check data consistency <br>
* Compose charts and map chart <br>


#### To do:
* More map charts in the division into particular months  <br>
* Chart with juxtaposition of all payment profiles
* Apply code optimization for Python to enable better efficiency (e.g. numba)

#### Check more:
[Link to Github](https://github.com/John-smith-889/taxi-spatial-data-analysis)












<br>
## 5. Exploratory Data Analysis of Movies Data in Python

<span style="color:darkblue"> <em>Python, numpy, pandas, matplotlib</em></span>

#### Project description:

The aim of the project is to explore data and build model to predict rating of particular movies. Project is based on Movies Dataset accessible on Kaggle.com [here](https://www.kaggle.com/rounakbanik/the-movies-dataset). Used file movies_metadata.csv contains information on 45_000 movies released on or before July 2017. Movies belong to the Full MovieLens Dataset. Variables include budget, revenue, release dates, languages, and more. Ratings are on a scale of 1-10.

Project contains Jupyter Notebook file named "movies_case_eda.ipynb" with:
* Data collection <br>
* General overview <br>
* Data exploration of choosen variables <br>

#### To do:
* Explore relations between variables <br>
* Create movies_case_feat_eng.ipynb where features will be prepared for data modelling <br>
* Create movies_case_model.ipynb for data modelling <br>
* Deploy model in Flask web app <br>

#### Check more:
[Link to Github](https://github.com/John-smith-889/movies_data_analysis)










<br>
## 6. Credit Scoring in R    

<span style="color:darkblue"> <em> R, MXNetR, dplyr, scorecard, corrplot, fastDummies </em></span>

#### Project description:

The aim of the project is to predict defaults of bank customers. Project contains two files: "feature-engineering.R" and "credit-scoring.R".

In feature engineering part there are used techniques like:
* IV (Information Value) calculating
* dummy variables
* merging correlated variables with PCA

In credit scoring part following activities were done:
* setting up Multi Layer Perceptron
* creating custom callback function for training process monitoring
* model evaluation with gini coefficient
<br>

#### Check more:

[Link to Github](https://github.com/John-smith-889/Credit-scoring-case-study-2019)













<br>
## 7. Migrations in Europe Visualization in Shiny App    

<span style="color:darkblue"> <em> R, Shiny, googleCharts, magrittr, devtools </em></span>

#### Project description:

The aim of the project is to build simple web application to visualize migrations across Europe over the years.
Application frontend consists an interactive chart showing changes in migrants and refugees levels in European countries. Small button below the chart may be used to animate changes over the years. 
In the chart it is possible to discover:
* particular country names in the map represented as bubbles
* population of particular country at the choosen moment in time represented as a bubble size
* migrants and refugees level at the choosen moment in time represented as a position in 2-dimensional space
* color division on northern, southern, eastern and western countries

#### Check more:

[Link to deployed app](https://james-smith-889.shinyapps.io/shiny-migrations-europe-bubblechart/)

[Link to Github](https://github.com/John-smith-889/Shiny-migrations-europe-bubblechart)














<br>

Last but not least...
## 8. Jekyll Blog About Data Science Deployed on GitHub Pages 

<span style="color:darkblue"> <em>Ruby, html, css, javascript </em></span>

#### Project description:

The aim of the project is to build blog for posting technical issues associated with data science and software engineering.
Posts presented on blog include topics associated with Python, social network analysis, devops, space industry and more. 

Ruby framework Jekyll with its Lanyon theme were used to create this blog. 
A few features have been added to personalize blog, including:

* Logo
* Social media icons
* Code font modificiation
* Code highlighting modification
* Favicon
* Long code snippets rolling
* Footer
* Post layout modification
* Archive 
* Categories
* Disqus integration
* Google Analytics integration

#### To do:
* Upgrade categories and tags system

#### Check more:

[Link to the blog](https://john-smith-889.github.io/blog/)

[Link to Github](https://github.com/John-smith-889/blog)

<br>


<center> To be continued... </center>
