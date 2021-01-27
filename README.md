# _Lords of War: A Global Arms Trade Analysis_

![A dense, highly interconnected graph visualization showing thousands of relations between 250 odd entities representing state and non-state actors supplying with arms](./images/initialneo4jload.png)

# Introduction: Motivation & Goals

- This project uses data from [SIPRI's Arms Trade Database](https://www.sipri.org/databases/armstransfers) and is a work in progress currently focusing on network analysis using Neo4j and Python of the highly interconnected relationships and flow of goods between actors in the arms trade, focusing on a binary classification task of whether the United States is the Supplier in an arms trade or not.
- I chose this dataset after working on regime change data previously and world unrest, seeing the arms trade as a natural evolution of what to study. I hope to incorporate these projects together(the other mentioned -- [located here](https://github.com/MichaelBurak/regime_changes) -- being a stock analysis of defense stock compared to world unrest towards authoriatarianism and the fragility of states undergoing it.)

# Contents

- [The Data Set](#the-data-set)
- [Process Overview](#process-overview)
- [Project Status](#project-status)
- [Future Work](#future-work)
- [Follow Me On](#follow-me-on)

# The Data Set

![Chart depicting up and downs for trades per year in arms trade](./images/trades_per_yr.png)

- The dataset contains over 25k transactions between over 250 actors(_nation state and non both_) from 1940 to 2019 in the global arms trade.
- The data is wonderfully dense and I am still exploring it and finding new things to study.
- Issues include the rich text format that the data originally was in making it difficult to import and requiring extensive data wrangling as the columns would not align and NaN predominated the dataset(so much of the notebook is data wrangling), as well as a format not suited for traditional analysis in Python's data science ecosystem.

![Chart depicting top 10 suppliers in the arms trade dataset, first being the US](./images/top_10_suppliers.png)

# Process Overview

- The data was gathered from SIPRI's site in the form of a rich text file, which resisted attempts to load cleanly into _Pandas_. Data cleaning was the next step.
- Columns were shifted to fix formatting issues, rows filled based off of previous values and their place in the data, null values and columns were dropped.
- Special characters were removed from column values to render them numeric.
- Plotting of top Suppliers, Recipients, and trade partners was done.
- A final dataframe with the _target of a boolean value of 1/0 or United States/other Supplier in the Supplier column_ was created for analysis.
- Data on Suppliers, Recipients and who had supplied who was transferred via. _Py2Neo library_ to the graph database _Neo4j_ in a local installation for further and future analysis.
- A brief NLP exploration of the Comments column indicating notes on the trades was embarked upon using _t-SNE and UMAP_ visualization along with a wordcloud.
- _Another library for Neo4j, nxneo4j,_ was used to visualize and analyze the stored graph data from the Jupyter Notebook development took place in, _utilizing algorithms of centrality such as PageRank to identify important nodes and communities of interacting nodes_, experimented with as important features(currently not being used for scaling concerns.)
- Several columns, including Comments, were dropped and numeric columns created by earlier experimenting with _iteratively increasing how many values of each categorical variable would be one hot encoded_ for best performance, including _1000 dummy variables in high cardinality columns._, experimented with as feat
- Modeling utilizing _SMOTE_ for the imbalanced classification task's target to be resampled, at one point _Principal Component Analysis for dimensionality reduction_ in high-dimensional space, scaling, primarily the model used was _Complement Naive Bayes as a fast, effective binary classifier_ which was employed with _cross validation_ and _grid searching_, reaching a **weighted F1 score of .91**.
- _SHAP_ was used to examine the final model for interpretability, showing the importance of numeric columns engineered from text representing comments including "second-hand", "aid" and "combat" or "aircraft" as important.

![A plot showing the direction and amount of importance of model features, prominently around the above text features](./images/shap.png)

# Project Status

- This project is still in process, keep tuned for more and pardon the mess! So far I have gained a greater appreciation for my data cleaning skills, a willingness to tackle the most arcane of datasets, and a deep interest rekindled in this sort of socio-political data.
- Currently working on using catboost given the predominance of categorical values in the dataset.

# Future Work

- Additional data I'd like to add in is data on the countries themselves, possibly financial data as well, along with the unrest and state fragility datasets I have worked with in the above project.
- Next steps include geospatial work involving similar countries as determined by graph algorithm, clustering, outlier detection, further NLP on the text columns, and more including iterating on the modeling aspect of this project.

# Follow Me On

[LinkedIn](https://www.linkedin.com/in/michael-burak/) for **pretty pictures**

![More minimal representation of the top graph of Actors and trades](./images/nxdrawtrades.png)
