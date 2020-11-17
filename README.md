# iFootballManager

Building AI course project

## Summary

Manage a team on a budget! Find players that are outperforming their market value, maximize player quality within a given budget. Not every team is Manchester City and can afford high profile players.

## Background

* Teams function under a limited budget but still want to improve and be competitive with the money they have. How do they decide to buy new players? 
* Scouting multiple players across multiple leagues is expensive and relies on the quality of the scout. 
* Developing your own players is also a large investment that requires an expensive infrastructure. 

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
  
  # suppose we have the data in a text file with the player stats where first column is the player name, 
  # and the last column is their real market price (based on recent transfer), and the columns in between are player statistics 
  like pass% shot% minutes played, etc, and the player market value in last column
  train_data = np.genfromtxt(StringIO(train_string), skip_header=1)
    
  # split the data into coefficients (x) and market value (y) 
  player_train_value = train_data[:, -1]
  player_train_coefficents = train_data[:, 1:-1]
  player_name = train_data[1]
  
  # fit a linear regression model to the data and get the coefficients
  c = np.linalg.lstsq(player_train_coefficents, player_train_value)[0]

  # Test data has similar data format compared to train data
  player_data = np.genfromtxt(StringIO(test_string), skip_header=1)
  player_coef_data = player_data[:, 1:-1]

  # save the player data and print out the predicted market values for the players in the data set
  player_predicted_values = (player_coef_data @ c)
  print(player_predicted_values)
  
  # optimize the budget and players to buy
  # first create a list of players by market value vs current market value 
  relative_market_value = []
  for i in range(len(player_predicted_values):
    current_player = { name: player_name[i], value_gain: y_train[i] - player_predicted_values[i] }
    relative_market_value.append(current_player)
  
  print(relative_market_value)
  # algorythm to maximize the budget and amount of players to be implemented
    
main()
```


## Data sources and AI methods
Relevant player data can be gathered from https://www.rotowire.com/soccer/stats.php?UCL=1 
Current market value data can be obtained from https://www.transfermarkt.com/

## Challenges

The AI can predict which player is worth more than their market value but it cannot predict whether the player will actually reach its potential or whether it gets a season ending injury. Though injury proness can be included in the evaluation, a season ending injury can happen to any fit player. 

## What next?

* Determine the likelihood of a player injury in each next game based on player load, weather, field quality, average distance per game, etc. 
* Determine best substitutes for a given game depending on the score, player recent performance (ie how is a player trending), weather, etc. Add climate to player evaluation: some players perform better in cold or wet weather than others. Some players perform better in extreme heat.
* Determine whether investments into own youth players is worth the cost of the investment. Prediction based on player progress vs money spent. 
* Player qualification system using logistic regression; player categories can be: prospect, value player, star, sale potential

Required capabilities: Accessing an api to fetch weather data, player data, market data. Developing a neural network to map players to categories. 

## Acknowledgments

* Football Fantasy League https://fantasy.premierleague.com/my-team
