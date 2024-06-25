# scam92_assignment1
created a basic lstm model to predict stock prices of chosen company
Making a stock prediction model using lstm 
Steps:
1) Trained the model using the stock data of aapl , for the data collection I used tiingo api 
2) Extracted the past data for around 3.5 years which contained data for 854 days , now used 
(854-30)=824 days data for training and last 30 days for testing
3) Plotted the data for all 854 days
4) I was interested in predicting the closing price for the stock
5) I separated ‘close’ and made a list containing only close price.
6) Now to apply lstm I need timestep and for my case it is 100 
7) So my train size came to be 100+30+1=131and test size became 854-train size
8) Collected train and test data I n train_data, test_data respectively
9) Created a function which take a dataset as parameter and to apply lstm on days close price I 
need the entries close price of the all the 100(timestep) following that day , so the function 
serves this purpose it returns datay list which have the close price entry used as a label in 
this case and list datax which have the following 100 days close price entries and are used as 
input features for that label existing in datay.
10) Used this function on both train and test dataset and collected y_train (a day’s close price in 
training set) , x_train(the corresponding 100 past entries for that dayy_train (corresponding 
label ) and x_test, y_test.
11) Applied minmax scalar to scale the entries in range (0 to 1)
12) Created a lstm model with these specifications :
model=Sequential()
model.add(LSTM(50,return_sequences=True,input_shape=(100,1)))
model.add(LSTM(50,return_sequences=True))
model.add(LSTM(50))
model.add(Dense(1))
model.compile(loss= 'mean_squared_error', optimizer='adam')
13) Trained the model with the data x_train and y_train 
14) Did the inverse of minmax scaler to get to original scale
15) Did the prediction for both train and test data and found mean squared error for them. for 
train data it came t o be 163.77209919768555 and for test it came as 197.09241484647967
16) Made the plot blue line for all the original data, orange for prediction in train data green for 
prediction for last 30 days
