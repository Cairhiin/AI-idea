# Project Title

iFootbalManager

## Summary

Manage a team on a budget! Find players that are outperforming their market value, maximize player quality within a given budget. Not every team is Manchester City and can afford high profile players like Kevin de Bruijne but every team can purchase the next best thing, or try to!

Building AI course project

## Background

* Teams function under a limited budget but still want to improve and be competitive with the money they have. How do they decide to buy new players? Scouting multiple players across multiple leagues is expensive and requires on the quality of the scout. Developing your own players is also a large investment that requires an expensive infrastructure. 


## How is it used?

The AI will gather data of all players for a given position and in a given league. It then suggests players to buy based on the available budget. Managers of football teams with limited resources can then decide where and with whom to strenghten their team and who to sell to free up budget.

Linear regression can be used to determine the predicted market price. The system can be trained with data from players that are recently traded and their stastics. 

Simple code example using NumPy:

```
def main():
  # example budget
  budget = 1000000
  
  # example number of players to buy
  players = 2
  
  # suppose we have the train data in a text file with the player stats as coefficient in the first n columns 
  # and the player market value in last column
  train_data = np.genfromtxt(StringIO(train_string), skip_header=1)
    
  # split the data into coefficients (x) and market value (y)
  y_train = train_data[:, -1]
  x_train = train_data[:, :-1]

  # fit a linear regression model to the data and get the coefficients
  c = np.linalg.lstsq(x_train, y_train)[0]

  # Similar data format compared to train data
  x_data = np.genfromtxt(StringIO(test_string), skip_header=1)
  x_data = x_test[:, :-1]

  # save the player data and print out the predicted market values for the players in the data set
  player_predicted_values = (x_data @ c)
  print(player_predicted_values)
  
  # optimize the budget and players to buy
  # first create a list of players by market value vs current market value
  
  relative_market_value = []
  for i in range(len(player_predicted_values):
    
main()
```


## Data sources and AI methods
Relevant player data can be gathered from https://www.rotowire.com/soccer/stats.php?UCL=1 
Current market value data can be obtained from https://www.transfermarkt.com/

## Challenges

The AI can predict which player is worth more than their market value but it cannot predict whether the player will actually reach its potential or whether it gets a season ending injury. Though injury proness can be included in the evaluation, a season ending injury can happen to any fit player. 

## What next?

Determine the likelihood of a player injury in each next game based on player load, weather, field quality, average distance per game, etc. Determine best substitutes for a given game depending on the score, player recent performance (ie how is a player trending), weather, etc. Add climate to player evaluation: some players perform better in cold or wet weather than others. Some players perform better in extreme heat.

Required capabilities: Accessing an api to fetch weather data, player data, market data. 

## Acknowledgments

* Football Fantasy League https://fantasy.premierleague.com/my-team