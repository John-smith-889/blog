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
## 2. Housing Prices Modelling in Python

<span style="color:darkblue"> <em>Python, numpy, pandas, scikit-learn, xgboost, matplotlib, seaborn</em></span>

#### Project description:

The aim of the project is to analyze data and build model to predict housing prices. Project is based on dataset accessible on Kaggle.com [here](https://www.kaggle.com/harlfoxem/housesalesprediction). Dataset contains information on sold houses in King County (including Seattle) between May 2014 and May 2015. Variables include date of sale, price, number of beedrooms, number of beedrooms, floor area, and more.

Project contains Jupyter Notebook file named "housing_case.ipynb" with:
* Data exploration <br>
* Feature engineering <br>
* Data modelling <br>
* Models evaluation <br>
* Choosen model optimization <br>

#### To do:
* Experiment with Artificial Neural Networks <br>
* Modify variables with binning and include date of sale as a explanatory variable <br>
* Experiment with more efficient metaheuristics during hyperparameters optimization <br>


#### Check more:
[Link to Github](https://github.com/John-smith-889/housing-prices-modelling)

<br>

## 3. Exploratory Data Analysis of Movies Data in Python

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


## 4. Credit Scoring in R    

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


## 5. Migrations in Europe Visualization in Shiny App    

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
## 6. Jekyll Blog About Data Science Deployed on GitHub Pages 

<span style="color:darkblue"> <em>Ruby, html, css</em></span>

#### Project description:

The aim of the project is to build blog for posting technical issues associated with data science and software engineering.
Ruby framework Jekyll with its Lanyon theme were used to create this blog. Posts presented on blog incorporate social network analysis, devops and more. A few features had been added to personalize blog, including:
* Archive 
* Categories
* Social media icons
* Code font modificiation
* Code highlighting modification
* Favicon
* Long code snippets rolling
* Footer
* Post layout modification
* Disqus integration
* Google Analytics integration

#### To do:
* Upgrade categories and tags system

#### Check more:

[Link to the blog](https://john-smith-889.github.io/blog/)

[Link to Github](https://github.com/John-smith-889/blog)

<br>


<center>To be continued... </center>

