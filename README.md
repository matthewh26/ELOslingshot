# ELOslingshot

Application to recommend your champ selection based on yours + enemies' team comp

Data Used: https://www.kaggle.com/datasets/paololol/league-of-legends-ranked-matches
(currently)

## FILES

- data_create.py: This uses some of the files (located above) to create a dataset I can use for modelling purposes
- win_predict.py: The file containing the neural net framework (not currently used)
- main.py: The file you need to run to actually get your custom champion recommendations! (not currently used)

### App - folder for web app (development)

This folder contains files needed to run a localhost web app where you can interactively submit imformation about your lobby and the
app will return the recommended champ you should play along with a prediction of the win probability. It uses the naive method of taking the winrates of every 
possible champ with every other champ in the game and averaging these. Still a WIP, so far styling is very basic and you can only input allied champs.

- static: contains styling for the pages and also winrates.py, containing a function for calculating winrates from the dataset used by the app.
- app.py: the file that runs the app.
- templates: contains the html templates for the pages.

To use: 
1. Download app folder from here, along with data_create.py.
2. Also download the data from the kaggle link above.
3. Run data_create.py to create the dataset used by the app.
4. Install flask on your environment: **pip install flask**
5. Navigate to app directory.
6. Run the following: **flask run**
7. Put the URL given into your browser, and have a go with the app!(try and select champs in the role that they are conventionally played, otherwise there may not be enough data to give a result)

## PLAN (as a reminder to myself so that I don't forget)

The kaggle dataset used is old but is large and contains a lot of information so is useful to build up a method that works well as a proof of concept.
First I would like to build 2 different models and test these to see how well they work before looking for potential improvements:
  1. 'Naive' model, checks the win rates of every champ in your team with all of the possible champs you can play, then averages this.
      (And the same for every champ in enemy team's win rates vs. every champ you can play). Champ with the highest win rate is what you pick.
  2.  Create/optimise a neural net that will predict based on game stats (gold earned, kills, etc) if the match was won or lost. Then, from the dataset,
      for every champ, find an average of these stats across all games played with you team's champs (and enemy champs) and insert into the model. The sigmoid
      activation output can be treated as a 'win probability' for this champ combination. Across all champs, the win prob is averaged and the champ with the highest
      average win prob is what you pick.

These are my initial ideas, and also it will be quite hard to test how effective they are. I can see if the approach of averaging is any good by holding out some data and finding the average euclidean distance between averaged match stats and actual (i.e. if the averaged stats are averaging <2 kills away from actual this is pretty good).Can then research more/ increase complexity of this if it is good with heuristics etc.

Naive model I can test by using it??? To play a lot of games, and see what the win rate is like with/without it but that is quite time consuming. This model is probably more meant as a baseline anyway.

Would also be extremely beneficial to add in heuristics regarding the individual player, such as champion proficiency (so for example me if I am using it)
However for testing, I can just play the highest 'rated' champ that is in my champ pool (of like 7 champs lol)

End goal is to get Riot approval and create a functioning web application that I can use to get me to diamond ;) 
