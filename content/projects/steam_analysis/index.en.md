---
title: "Analyzing Steam Libraries and Reviews"
date: 2025-06-15T18:49:04-06:00
draft: false
---

## Introduction
Steam is a digital video game distribution service and storefront that is developed by the Valve Corporation. It was released in 2003 to distribute only Valve developed games as a means to play their video games on PC, and later updated in 2005 to distribute third-party titles as well. Steam quickly gained market traction and currently is the most popular storefront service for PC gaming, attracting millions of players. As Steam services millions of users in the PC gaming market, data gained from its storefront can be very useful in identifying trends within the video gaming market. This data could be used to understand genres that are gaining traction amongst fans, predict the success of future titles, and better understand consumer behavior. The video game market is a large and growing industry, with larger revenues than many film and TV enterprises. Additionally, there has been a marked shift away from titles developed by large companies and toward independent developers. Some popular indie titles, like Balatro and Stardew Valley, were developed by a single person and have become enormous successes, leading their creators to massive wealth. This highlights the opportunity in analyzing consumer data from a platform like Steam. If we can understand the consumers likes and dislikes, there is a huge economic opportunity to use that data to formulate a successful game. Through data visualization and statistical analysis, we can explore some user behaviors and game trends.

## Analysis Questions 

1. How many games does each user own? How long do they play each title for, on average?
2. How often do users leave reviews? Are they reviewing for each title in their library, or only some titles? 
3. What is the overall distribution of ratings in user reviews? Does the average review skew a certain direction? 
4. When are most games released? Is there a steady release of titles through the year or does one season dominate with releases?
5. What games have the highest play time numbers? Is there commonality between genre or review ratings?

## Data Sourcing and Justification

The data source for this project is the Game Recommendations on Steam dataset on the Kaggle platform. The data was collected using the Steam API, and the user information was anonymized behind user ids to protect privacy. The set itself is comprised of 3 tables, users, games, and recommendations. The games data includes basic identifying information like title and release date, operating systems the game is compatible with, original price and current pricing information, and some aggregated information from the recommendations table. The recommendations table includes information about reviews left on games, the user who made the review and how many hours they've played, the game id, and aggregate votes of whether the review was helpful or funny. The users table contains user id, and counts of the number of products owned and reviews left. 

This data set was selected as Steam is the most used PC storefront. For a better, more encompassing analysis of the entire games market, it would be wise to incorporate data from Sony and Microsoft's console storefronts, as well as mobile storefronts like Google Play and Apple, however this data is proprietary. Steam, which supports open source, makes this data available, and due to its popularity, also makes this set a great option to make conclusions regarding the PC market. The insights gained here will be valuable, but it is important to note they may not extend to the console or mobile markets in the same way.

## Data Cleaning 

Minimal cleaning was needed for this dataset. Each table was imported into a pandas dataframe and inspected for missing values and duplicates, none were found. Numerical features were inspected using Additionally, the data was inspected for outliers in numerical and date columns, dates consistently fell between 1997 and 2023, which are the expected extents of the data, numerical columns found no outliers through inspection with `pd.describe` and distribution plots. Since we are focused on user engagement and acquisition, we will omit users that have accounts but have not left reviews or purchased games, this will be done using inner joins when joining the user and recommendation tables.

## Visualizations and Findings

Many users have signed up for Steam but have not played any games

![Hours Played by user Boxplot](/projects/steam_analysis/images/hours_played_box.png)


Users have mostly played 100s or 1000s of hours, when excluding those who haven't played at all. Some users have played many, many hours

![Hours Played by user Log Distribution](/projects/steam_analysis/images/hours_played_distribution.png)

Reviews skew positive on Steam, but users are not typically leaving reviews on many games

![Distribution of Review Sentiment](/projects/steam_analysis/images/review_dist.png)

Number of releases on Steam and in general have increased steadily with time

![Number of Releases over Time](/projects/steam_analysis/images/release_trend.png)