# Netflix_Data_Assignment

## Project Overview

This project focuses on analyzing and visualizing a Netflix dataset containing information about movies and TV shows. The objective is to extract meaningful insights through data cleaning, exploration, and visualization using Python and R.

The project was completed as part of a data analytics assignment and demonstrates the integration of multiple tools for effective data analysis.

## Assignment Objectives

The following requirements were successfully completed:

* Data preparation (unzipping and organizing dataset)
* Data cleaning (handling missing values)
* Data exploration (descriptive and statistical analysis)
* Data visualization using Python (Matplotlib & Seaborn)
* Integration of R for visualization
* Proper documentation and project structuring

## Dataset Description

The dataset contains information about Netflix content, including:

* Title
* Director
* Cast
* Country
* Release year
* Rating
* Duration
* Genre (listed_in)

## Tools & Libraries Used
### Python Libraries

* pandas
* matplotlib
* seaborn
* zipfile
* os

### R Libraries

* ggplot2

## Data Preparation

The dataset was initially provided in a compressed (ZIP) format. It was extracted and organized into a working directory.

*Python Code:* 

import zipfile
import os

with zipfile.ZipFile('netflix_data.csv.zip', 'r') as zip_ref:
    zip_ref.extractall('Netflix_shows_movies')

os.listdir('Netflix_shows_movies')

## Data Cleaning

Missing values were identified and handled appropriately to ensure data consistency.

Approach:

* Filled categorical null values with "Unknown"
* Dropped rows with critical missing fields

*Python Code:* 

import pandas as pd

df = pd.read_csv('Netflix_shows_movies/netflix_data.csv')

df['director'] = df['director'].fillna('Unknown')
df['cast'] = df['cast'].fillna('Unknown')
df['country'] = df['country'].fillna('Unknown')

df.dropna(subset=['date_added', 'rating'], inplace=True)

## Data Exploration

Basic data understanding and statistical summaries were performed.

*Python Code:* 

df.info()
df.describe()

df['type'].value_counts()
df['rating'].value_counts()

*Key Insights:*

* The dataset contains both Movies and TV Shows
* Some ratings appear more frequently than others
* Missing values were present in key descriptive fields

## Data Visualization (Python)
*A. Most Watched Genres* 

To analyze popular genres, the listed_in column was split and expanded.

import matplotlib.pyplot as plt
import seaborn as sns

df['listed_in'] = df['listed_in'].str.split(',')
df_genre = df.explode('listed_in')
df_genre['listed_in'] = df_genre['listed_in'].str.strip()

genre_counts = df_genre['listed_in'].value_counts().head(10)

plt.figure()
sns.barplot(x=genre_counts.values, y=genre_counts.index)
plt.title('Top 10 Genres on Netflix')
plt.xlabel('Count')
plt.ylabel('Genre')
plt.show()

*B. Ratings Distribution* 

plt.figure()
sns.countplot(data=df, x='rating')
plt.title('Distribution of Ratings')
plt.xticks(rotation=45)
plt.show()

*Insights:* 

* Certain genres dominate Netflix content
* Ratings are unevenly distributed across titles

Data Visualization (R Integration)

One of the visualizations was recreated in R using ggplot2.

## R Code

library(ggplot2)

df <- read.csv("netflix_titles.csv")

ggplot(df, aes(x=rating)) +
  geom_bar() +
  theme(axis.text.x = element_text(angle=45, hjust=1)) +
  ggtitle("Distribution of Ratings")

## Conclusion

This project demonstrates how raw data can be transformed into actionable insights through:

* Effective data cleaning
* Structured exploration
* Clear visual storytelling

It also highlights the integration of Python and R in a single analytics workflow.
