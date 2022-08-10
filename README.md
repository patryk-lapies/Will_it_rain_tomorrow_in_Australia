
# Will it rain tomorrow in Australia

The goal of this project is to predict whether is it going to rain the next day 
in Australia based on this data: [Rain in Australia](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package).
Its purpose is to learn and practice the usage of the Random Forests Classification algorithm. 

## Technologies

- Python 3.9.12
- Scikit-Learn 1.0.2
- Numpy 1.22.3
- Pandas 1.4.2
- Seaborn 0.11.2
## About the Data

This dataset contains data about 10 years (2007-2017) of daily weather observations
from many locations across Australia with 142193 rows, 23 features, and a target
variable. Some of the features are location, min/max temperature,  wind speed, 
humidity, and pressure. Target variable RainTomorrow indicates whether or not did 
it rain the next day. 
## Data Cleaning
- Transformed Date column into 3 other columns (Year, Month, Day)
- Because of a little amount of data from 2007 and 2008 dropped data from these years 
- Dropped Evaporation, Sunshine, Cloud9pm, Cloud3am columns because of the amount of missing values
- Filled missing values in columns Pressure9am and Pressure3pm with their means
- Dropped RISK_MM column
- Transformed categorical columns using get_dummies

### Standarisation
- Used Standard Scaler from sklearn to standardised all numeric data
## Models created
### Evaluation 
Each created model was evaluated using an accuracy score.
### Basic model
The first Random Forest Classification model was based on all features with listed parameters in the table below.
| n_estimators | criterion | max_depth | random_state | accuracy |
|:------------:|:---------:|:---------:|:------------:|:--------:|
|       5      |    gini   |     5     |      42      |    82 %   |

### Model with better parameters
For the second model to find better parameters RandomizedSearchCV was used with a defined parameters grid. This model achieved better accuracy on the test data.
| n_estimators | criterion | max_depth | random_state | min_samples_leaf | accuracy |
|:------------:|:---------:|:---------:|:------------:|:----------------:|:--------:|
|      100     |  entropy  |    None   |      42      |         2        |  85,6 %  |

Then in order to find the best parameters, GridSearchCV was used for it. It found better parameters but accuracy improved marginally.
| n_estimators | criterion | max_depth | random_state | min_samples_leaf | accuracy |
|:------------:|:---------:|:---------:|:------------:|:----------------:|:--------:|
|      250     |  entropy  |    None   |      42      |         2        |  85,7 %  |

Adjusting the max_features parameter helped in achieving a slightly better score.
| n_estimators | criterion | max_depth | random_state | min_samples_leaf | max_features | accuracy |
|:------------:|:---------:|:---------:|:------------:|:----------------:|:------------:|:--------:|
|      250     |  entropy  |    None   |      42      |         2        |      10      |  85,8 %  |

### Model on a slightly different data
For the next models to previously used data I added Sunshine, Cloud9am, Cloud3pm columns with their missing values filled by their means. The goal was to check if their presence can boost accuracy.

Created model using RandomizedSearchCV produced marginally better accuracy than the previous usage of it.
| n_estimators | criterion | max_depth | random_state | min_samples_leaf | accuracy |
|:------------:|:---------:|:---------:|:------------:|:----------------:|:--------:|
|      150     |  entropy  |    None   |      42      |         4        |  85,7 %  |

### Model not using all features
The last model used only MaxTemp, Sunshine, WindGustSpeed, Humidity9am, Humidity3pm, Pressure9am, Pressure3pm, Rainfall, Cloud9am, Cloud3pm, Temp3pm as its features and had accuracy similar to other models using all features.
| n_estimators | criterion | max_depth | random_state | min_samples_leaf | accuracy |
|:------------:|:---------:|:---------:|:------------:|:----------------:|:--------:|
|      150     |  entropy  |    None   |      42      |         4        |  85,7 %  |

## Conlusion
The last model is the best with 85.7% accuracy because it only uses 11 features to predict the target value instead of all of them.