# Predict Stock Prices with RNN models  

### Overview  

RNN models were developed to predict stock prices for the S&P 500 Index over a 5-year span. Daily adjusted closing prices from 2015 – 2019 were sourced from Yahoo! Finance, yielding 1257 days of closing price values. To implement best practices for time series modeling, the data split assigned earlier periods (2015 – 2018) for training and validation, with 2019 used as the test set. The RNN models were also built with using the prices from the previous 5 days to train the model. 5 days was used as the lookback window to reflect the 5-day week of the financial markets, since the NYSE is open Monday - Friday and closed on the weekends.  

### Exploratory Data Analysis  

The graph of the closing stock prices shows a slight dip between at the end of 2015 and in early 2019. Closing prices have seen an increase over the past 5 years otherwise. Prices from 2018 have a high degree of volatility and will be used in the validation set. This volatility will affect model fitting.  

![EDA graph closing prices 2015 - 2019](https://user-images.githubusercontent.com/49419673/156899874-8179c262-97e0-450f-90bf-afd7515d9505.png)  

### Model Exploration  

A baseline linear regression model was built with Keras to compare to three RNN models. The three RNN models are outlined below:
* Deep RNN: 2  layers, 20 neurons, 10 epochs
* LSTM Model 1: 2 layers, 20 neurons, 10 epochs
* LSTM Model 2: 2 layers, 20 neurons, and hyperparameters tuned  
** Modeling with batches incorporated and epochs increased to 50  
** Training included monitoring loss on the valdation set  

Root mean squared error was used as the performance metric for model fit to compare the average distance between the predicted and actual price values.   

The Deep RNN model achieved the best performance on the Test set with RMSE of $23.65, however, LSTM Model 2 achieved lower RMSE for the Train and Validation set and a slight increase in RMSE for the Test set at $26.46. Tuning the hyperparameters on LSTM Model 2 helped to mitigate overfitting over LSTM Model 1. As suspected from the EDA, RMSE on the Validation set was the highest in all models, due to the price volatility during that period.  

| Model                      | Train RMSE | Validation RMSE | Test RMSE |
| -------------------------- | ---------- | --------------- | --------- |
| Baseline Linear Regression | $36.75     | $72.40          | $50.24    |
| Deep RNN                   | $17.30     | $31.42          | $23.65    | 
| LSTM Model 1               | $22.63     | $43.30          | $30.54    |
| LSTM Model 2               | $17.02     | $29.73          | $26.46    |

When looking at the graphs of Predicted vs. Actual prices from the Test set, all models consistently exhibited higher predicted prices when the actual prices were on a downward trend and exhibited lower predicted prices when actual prices were on an upward trend. The graphs display the least error in the Deep RNN and LSTM Model 2 models, whereas the LSTM Model 1 graph, shows the greatest gaps between predicted and actual price values.  

![DeepRNN testpredict](https://user-images.githubusercontent.com/49419673/156901561-7ca8e4e3-ba05-415d-8502-1e6a0b82b0c5.png)  

![LSTM mod1 test predict](https://user-images.githubusercontent.com/49419673/156901566-fdce8fe3-0e9d-49ee-935b-83276349d9fd.png)  

![LSTM Mod5 -USE for LSTM2](https://user-images.githubusercontent.com/49419673/156901570-74846703-2d41-43e1-adb3-6858aaaaf04e.png)


