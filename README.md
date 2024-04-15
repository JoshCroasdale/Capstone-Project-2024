# README - Capstone Project

## Predicting NHL Player Performance Using Linear Regression and Neural Networks
##### by Josh Croasdale

## Table of Contents:
 * [Preamble](#Preamble)
 * [Background](#Background)
 * [Goal](#Goal)
 * [Data](#Data)
 * [Modeling Choices](#modeling-choices)
    - [Three Year Weighted Average](#three-year-weighted-average-calculation)
 * [Results](#results)
 * [Conclusions](#conclusions)
    - [Tools Used](#tools-and-resources-used)
    - [Special Thanks](#special-thanks)
 * [About the Author](#about-the-author)
 * [References](#references)
 * [Glossary ](#Glossary)

## Preamble:
Trying to predict (or guess) various different outcomes inside the National Hockey League (NHL) has long been a challenging task. Ice hockey is inherently a random sport. When you have full grown men on skates racing around a sheet of ice holding long sticks and batting around a 3 inch frozen rubber puck, things can get chaotic.<br> The NHL is the best ice hockey league in the world and so to just make it into the league is a huge accomplishment. The subset of all hockey players worldwide that play in the NHL will be considered its own population for the purposes of this analysis. In reality, the NHL population represents most of the top ~0.1% of all players worldwide.<br> With that being said, within the NHL population itself there is a wide variance in player skill level. Every player is unique, and you cannot necessariy compare the career trajectory of a 'superstar' player to that of a '4th line grinder.' You must be careful if you are using league-wide trends to make inferences or predictions about any one single player.

## Background:
#### Why is predicting player performance useful?
##### There are at least three major reasons why we care about predicting player performance:<br>
- `Personal Investment:` professional sports are a huge pasttime for many, and for many others that work in the field (reporters, analysts, commentators, team staff, franchise executives, etc.) their very livihoods are at stake. The ability to to make informed predictions or inferences may give one the upper hand against their friends, colleagues, or rivals. The bottom line here is that a lot of poeple simply care about what happens in professional sports.<br>
- `Sports Gambling:` In Canada and the US, sports gambling is a rapidly growing industry. There are a multitude of online betting companies and physical outlets where people can place bets on all manner of scenarios and outcomes. These scenarios can be at the team level or at the player level. If one can leverage predictive statistics and modelling to possibly gain an upper hand against the betting entities, there is a lot of money to be made. And vice versa, the betting entities themselves are trying to leverage these predictions to maximize their own profits.<br>
- `Fantasy Hockey:` This realm is of the most personal interest to me. In fantasy sports, you are pitted against friends and foes alike in a season-long battle to become the champion of your own fantasy league. The goal is to essentially pick what players you believe to be the 'best' as measured by a set of pre-determined metrics (goals, assists, shots, etc). To put it simply: if your players do better in the real-life games than the players of your opponent, you win. Fantasy sports is also fast becoming a monetarily-involved industry. Fantasy leagues often have a prize pool of cash at stake for the winners. On top of this, there are companies that provide the type of predictive analysis geared towards helping people win their fantasy leagues. One common business model is that a consumer pays a subscription fee (typically to renew at the beginning of each season) to gain access to the predicitve models that a company has built. If you are a company that has built a predictive model that's use is for sale, the incentive is to make your model the most accurate it can be in order to attract more users and sell subscriptions. 

## Goal:
I will be attempting to predict NHL player performance as measured by the number of `goals` that a given player will score. I will primarily be working with rate stats, that is the raw total of a given statistic for a given player divided by the total number of games played for that player. <br>
With this endeavor, I am emulating the useful information that someone trying to win their fantasy hockey league can leverage to gain the upper hand.<br>
In the future, the foundation of work that I have done will be adapted to predict a whole host of statistics, and not just goals.<br>
Additionally, the work can be adapted for use with game-by-game predictions. This approach would have the real-world use case of sports gambling supplementation.


## Data:
All player data was obtained from https://www.hockey-reference.com/$^{1}$. NHL player data for each season (2005-06 to 2023-24 (ongoing season)) was pulled in a .csv format and saved into individual .csv files using a text editor. All .csv files were compiled into one dataframe via python and processed from there. See .ipynb notebook for more detail. 


#### Features and trends that stood out:
 - Career numbers are not necessarily indicitave of recent or future performance!
   - Player performance changes over the course of a player's career. Experience-related improvement and age-related decline are certainties for all players.
 - Per-Game rate stats were implemented in order to "level the playing field" and easily compare players
   - It is difficult to compare a player who has 200 goals over 1000 games played to a player who has 50 goals over 160 games played. Dividing by games played will produce a Goals/Game number that is directly comparable across all players (I calculated these rate stats for every statistic (every feature)).
   - This is essentially a form of scaling. One pitfall I had to be aware of is players that have very few games played. Samples (players) that have very few games played can skew outputs. eg. 1 goal over 1 game equates to 1 Goal/Game, however, this sample is not indicitave of the overall population performance. 
 - Career total rate stats have another glaring issue, and it involves the experience-related improvement and age-related decline that was previously mentioned. If career-long numbers are used in modelling, the model will take it to mean that every season of a player's career should be weighted equally.
 - In reality, the more recent seasons of player's career are most predictive of future performance. The industry standard for approaching this problem is to implement a three year weighted average to feed into the model. The concept was borrowed from Dom Luszczyszyn's work at theathletic.com $^{2}$.
 - This approach takes the most recent three seasons of data for every player - or two seasons or one season if that is all that is available - and assigns weightings to each of the seasons. The most recent season is assigned the highest weight, the second most recent season is assigned the second highest weight, and the third most recent season assigned the least weighting. The resulting number has the same units as the original feature.
   - This method is, in a way, a kind of prediction on its own. It is an amalgamation of recent seasons that aims to provide the model with more responsible data to fit to.


## Modeling Choices:
* Linear regression - Pipeline, PCA feature reduction, StandardScaler
   - Career Totals
   - Career Per Game
   - Three Year Weighted Average
* Neaural Network for regression
   - Career Per Game
   - Three Year Weighted Average
* K Nearest Neighbors regression
   - Three Year Weighted Average
## Results:
#### Final Metrics Table:

Train Set Score	Test Set Score	Adjusted Rsquared	RMSE
Career Totals	0.990	0.990	0.990	7.299
Career Totals w/ manual feature reduction	0.862	0.813	0.812	32.192
Per Game w/ all features	0.998	0.998	0.998	0.004
Per Game w/ Pipeline & GridSearch	0.993	0.993	0.992	0.008
3 Year Weighted Avg w/ Pipeline & GridSearch	0.981	0.969	0.968	0.020
3 Year Weighted Avg w/ Pipeline & 0 G/GP filter	0.979	0.972	0.971	0.020
KNN model w/ StandardScaler (3 yr dataset)	1.000	0.931	0.929	0.029
Neural Network - Per Game Dataset	0.978	0.972	0.972	0.016
Neural Network - 3 Yr Weighted Dataset	0.981	0.943	0.941	0.027

* Model fit on per-game data with no feature reduction overfits the training data
   - High degree of multicollinearity between independent features
* Per-Game data with PCA has strong metrics. However, as I eluded to above, the three year weighted approach is going to be preferred
* Three Year weighted Linear Regression fit with Pipeline (PCA) and GridSearch:
   - Highed adjusted r2 value and low RMSE
   - Model does a nice job on predictions
   - tends to underpredict on above-average players
* KNN regression was overfitting. A training score of 1.0 indicates some irregular performance
* Neural networks have overall strong metrics
   - The three year average NN has a train score that is significantly higher than the test score. This may indicate small sample size or overfitting. 

### Three Year Weighted Average Calculation

The formulas used is the Linearly Weighted Moving Average $^{3}$:
$$\text{LWMA}_n = \frac{{P_n \cdot W_1 + P_{n-1} \cdot W_2 + P_{n-2} \cdot W_3 + \cdots}}{{\sum_{i=1}^{n} W_i}}$$

Where:
- P = The statistic being calculated (eg. Goals/Game)
- W = The assigned weight to each year (eg. 50, 33, 19)
- n = the most recent season, n-1 the second most recent, and n-2 the third most recent (eg. 2023, 2022, 2021)

## Conclusions:

Many model iterations were overfitting on training data. This could be due to a multitude of factors, but the most likely is too small of a sample size.
KNN was almost certainly overfitting. It also struggled to predict above-average players. 
Neural Network needs more tuning. With more precise implementation, there may be a path to fitting a more robust of production-worthy NN model.
#### Model of choice is the Three Year weighted Linear Regression fit with Pipeline (PCA) and GridSearch.
##### The most significant drawback of this model for productizing is its tendency to under-predict on the above-average or 'elite' players.
##### These happen to be the players that are of the highest interest to potential end users.

### Tools and Resources used:  
 - Python
 - sklearn  
 - pandas  
 - matplotlib
 - seaborn
 - plotly express
 - statsmodels
 - tensorflow
 - keras
 - sweetviz
 - streamllit 
 - Hockey-Reference (player data)
 

### Special Thanks:
 * Thanks to Hockey reference for providing their NHL data free of use on their website
 * The instructors and my fellow classmates at Brainstation

### About the Author:  
Josh Croasdale is a Data Science student at BrainStation in Vancouver, BC. 

## References
1. https://www.hockey-reference.com/leagues/NHL_2023_skaters.html
2. https://theathletic.com/1019070/2019/06/14/improving-our-nhl-projection-model-ahead-of-the-2019-20-season/ 
3. https://www.investopedia.com/terms/l/linearlyweightedmovingaverage.asp

## Glossary 

Year -- Year at time of season finale<br>

Age -- Player age at time of finale<br>

Pos -- Player position<br>

GP -- Number of Games Played in season<br>

G -- Goals<br>

A -- Assists <br>

PTS -- Points<br>

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

