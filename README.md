## README - Capstone Project

### Predicting NHL Player Performance Using Linear Regression and ML models
 

### Table of Contents:
 * [Preamble](#Preamble)
 * [Background](#Background)
 * [Goal](#Goal)
 * [Data](#Data)
 * [Model](#Model)
    - [Modeling Choices](#modeling-choices)
 * [Conclusions](#conclusions)
    - [Important Features](#permutation-importance)
    - [Results](#results)
    - [Tools used](#tools-and-resources-used)
    - [Special Thanks](#special-thanks)
 * [About the Author](#about-the-author)
 * [Glossary ](#Glossary)

## Preamble:
Trying to predict (or guess) various different outcomes inside the National Hockey League (NHL) has long been a challenging task. Ice hockey is inherently a random sport. When you have full grown men on skates racing around a sheet of ice holding long sticks and batting around a 3 inch frozen rubber puck, things can get chaotic.<br> The NHL is the best ice hockey league in the world and so to just make it into the league is a huge accomplishment. The subset of all hockey players worldwide that play in the NHL will be considered its own population for the purposes of this analysis. In reality, the NHL population represents most of the top ~0.1% of all players worldwide.<br> With that being said, within the NHL population itself there is a wide variance in player skill level. Every player is unique, and you cannot necessariy compare the career trajectory of a 'superstar' player to that of a '4th line grinder.' You must be careful if you are using league-wide trends to make inferences or predictions about any one single player.

## Background:
#### Why is predicting player performance useful?
##### There are at least three major reasons why we care about predicting player performance:<br>
	- `personal investment:` professional sports are a huge pasttime for many, and for many others that work in the field (reporters, analysts, commentators, team staff, franchise executives, etc.) their very livihoods are at stake. The ability to to make informed predictions or inferences may give one the upper hand against their friends, colleagues, or rivals. The bottom line here is that a lot of poeple simply care about what happens in professional sports.<br>
	- `gambling:` In Canada and the US, sports gambling is a rapidly growing industry. There are a multitude of online betting companies and physical outlets where people can place bets on all manner of scenarios and outcomes. These scenarios can be at the team level or at the player level. If one can leverage predictive statistics and modelling to possibly gain an upper hand against the betting entities, there is a lot of money to be made. And vice versa, the betting entities themselves are trying to leverage these predictions to maximize their own profits.<br>
	- `fantasy hockey:` This realm is of the most personal interest to me. In fantasy sports, you are pitted against friends and foes alike in a season-long battle to become the champion of your own fantasy league. The goal is to essentially pick what players you believe to be the 'best' as measured by a set of pre-determined metrics (goals, assists, shots, etc). To put it simply: if your players do better in the real-life games than the players of your opponent, you win. Fantasy sports is also fast becoming a monetarily-involved industry. Fantasy leagues often have a prize pool of cash at stake for the winners. On top of this, there are companies that provide the type of predictive analysis geared towards helping people win their fantasy leagues. One common business model is that a consumer pays a subscription fee (typically to renew at the beginning of each season) to gain access to the predicitve models that a company has built. If you are a company that has built a predictive model that's use is for sale, the incentive is to make your model the most accurate it can be in order to attract more users and sell subscriptions. 

## Goal:
I will be attempting to predict NHL player performance as measured by the number of `goals` and `assists` that a given player will produce, averaged over the length of an entire NHL season (82 games). With this endeavor, I am emulating the useful information that someone trying to win their fantasy hockey league can leverage to gain the upper hand. 


## Data:
All player data was obtained from https://www.hockey-reference.com/. NHL player data for each NHL season (2005-06 to 2023-24 (ongoing season)) was pulled in a .csv format and saved into individual .csv files using a text editor. All .csv files were compiled into one dataframe via python and processed from there. See .ipynb notebook for more detail. 



#### Features and trends that stood out:
 - 
 - 
 - 
 - 
 - 
 - 
 - 


## Model:

### Modeling Choices:
* Linear regression - 
* KNN regression?
* 
* 
* 




## Conclusions:



### Results:


### Tools and Resources used:  
 - Python
 - sklearn  
 - pandas  
 - matplotlib
 - seaborn
 - Tableau
 - SQL
 - Hockey-Reference (player data)
 

### Special Thanks:
 * Thanks to Hockey reference for providing their NHL data for free use on their website
 * The instructors and my fellow classmates at Brainstation

### About the Author:  
Joshua Croasdale is a Data Science student at BrainStation in Vancouver, BC. 

## Glossary 

Year -- Year at time of season finale<br>
Age -- Player age at time of finale<br>

Pos -- Player position<br>

GP -- Number of Games Played in season<br>

G -- Goals<br>

A -- Assists <br>

PTS` -- Points<br>

PTS/g -- Points per Game<br>

PS -- Point Shares; an estimate of the number of points contributed by a player<br>

PPG -- Power Play Goals<br>

PPA -- Power Play Assists<br>

Shots -- Shots on Goal<br>

S% -- Shooting Percentage (total goals / total shots on goal)<br>

TOI -- Total Time on Ice (in minutes)<br>

TOI/GP -- Average Time on Ice per game<br>

G/60 -- Number of goals averaged per 60 minutes of icetime<br>

A/60 -- Number of assists averaged per 60 minutes of icetime<br>



ToREAD: https://medium.com/codex/trying-to-predict-nhl-game-outcomes-with-ml-and-why-its-difficult-aaac4d2a690b

