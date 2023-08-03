---
layout: post
title: "Ukraine Russia Sentiment Analysis"
author: "Greg LeVay"
categories: documentation
tags: [documentation]
image: ukraine-russia-1.jpg
---

## Table of Contents
1. [Introduction](#introduction)
2. [Process](#process)
    1. [Data Overview](#data-overview)
        1. [Subreddit Types](#subreddit-types)
    2. [Methodology](#methods)
3. [Results](#results)

## Introduction

Throughout history Russia and Ukraine have had a contentious relationship.. In the past decade, Russia has taken a more aggressive approach starting with annexing a region of Ukraine that connects to the Black Sea called Crimea on March 18, 2014 ([1](https://www.cnn.com/europe/live-news/ukraine-russia-news-02-24-22-intl/index.html)). This action led to a series of altercations culminating in a Russian invasion of Ukraine on February 24th, 2022 ([2](https://www.nytimes.com/2014/03/19/world/europe/ukraine.html)). Outside of Eastern Europe, the rest of the world has also been reacting to the events in the region. Media portrayals have credited the growing polarization in the West as resulting in seemingly differing responses to these actions in the East. It is important, however, to conduct a study that will allow us to see the reality of the situation and understand if, in regards to the events of the East, sentiment/emotions have actually differed amongst the very polarized political ideologies. Using the Russian invasion on February 24th, 2022, as a landmark, a thorough sentiment analysis was conducted to investigate this question. The social media platform used for this particular study was Reddit. Reddit was chosen because of its pseudo-anonymity; pseudo-anonymity in this case means that often Reddit accounts do not contain personally identifiable information to individuals, the pseudo part is for the fact that some users wish to contain personally identifiable information. The pseudo-anonymity present in Reddit typically leads to people being more honest in the thoughts and opinions that they share online, since they are not worried about public backlash for a potentially controversial opinion. Reddit was the perfect platform to use in studying sentiment analysis in regard to the Russia Ukraine conflict amongst the differing conservative and liberal ideologies.

## Process

### Data Overview

The data which was used in this study consisted of 314k comments from 5.7k threads across 35 mostly political subreddits. The 35 political subreddits were separated into four categories: Conservative, Liberal, General, Location. The Conservative and Liberal labels are intuitive, General refers to subreddits that attempt to stay neutral, such as r/PoliticalDiscussion, Location refers to subreddits that are focused on opinions from a specific region such as r/AskEurope or r/AskAnAmerican. Location and General were categories used to act as controls to the study to not only understand how sentiment/emotions varied across the aisle, but also how it compared to the overall sentiment of the conflict.

### Subreddit Types

1. Liberal
    - r/liberal, r/neoliberal, r/socialism, r/AskaLiberal, r/ToiletPaperUSA, r/democrats, r/ShitLiberalsSay, r/thedavidpakmanshow
2. Conservative
    - r/conservative, r/republican, r/AskThe_Donald, r/GoldandBlack, r/libertarian, r/walkaway, r/tuesday, r/benshapiro, r/jordanpeterson, r/LouderwithCrowder
3. General
    -  r/news, r/politics, r/worldnews, r/Military, r/war, r/anime_titties,  r/history, r/geopolitics, r/PoliticalDiscussion
4. Location
    - r/europe, r/AskEurope, r/ukpolitics, r/ukraine, r/geopolitics, r/askarussian, r/china, r/AskAnAmerican, r/poland

### Methodology

All threads containing the phrase “ukraine” were scraped from the 35 different political subreddits. Note, Reddit’s API limits scraping to at most 250 threads per subreddit following a query. This limit caused some of the subreddits to contain comments going back to 2008, while other subreddits only contain comments that go back a few days before the scraping began. The data was then preprocessed by removing the following:“r/…”, mentions, links, punctuation, html tags and additional non UTF-8 specially encoded characters. In addition to removing parts of comments, some comments were removed if they were posted by a bot. After the text was preprocessed the sentiment was calculated using Syuzhet custom dictionary and the NRC Word-Emotion Association Lexicon was used to evaluate the emotions of each individual comment. After sentiment was calculated per comment, the data was aggregated by day and then the mean sentiment of all comments on a particular day was used. The NRC Word-Emotion Association Lexicon counts the number of words associated with a particular emotion, since comments can be any length on Reddit, there is a potential imbalance where the length of a comment can determine how emotional a particular comment is. To offset the potential imbalance of the number of comments driving emotions, the mean number of emotional words per emotion was then divided by the total number of comments made on that particular day per subreddit to normalize the evaluation metrics. After the emotions and sentiment of each subreddit per day were normalized, another mean was taken to find the overall average sentiment and emotionality of the subreddit type. To  display the findings in an easily digestible way, a shiny app was created.

#### Webscraping using the Reddit API


