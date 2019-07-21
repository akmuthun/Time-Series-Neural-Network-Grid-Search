# Time-Series-Neural-Network-Grid-Search
Grid search for multilayer perceptron neural network for modelling time series data

Special Thanks to Jason Brownlee

Time series data often arise when monitoring industrial processes or tracking corporate business metrics.
Tuning hyperparameters is always a difficult task when building neural networks.

This program is for grid (window size, nodes, epochs, batch, difference) searching for univarate time series data for modelling with a multilayer perceptron neural network. 
The MLP network which has been considered contains only one layer but can be adjusted for any number of layers easily. This will grid find for any forecasting steps which depends on the size of test dataset and export the best combination of parameters for each forecasting steps. 

## 10 functions in the program in detail:
<b>train_test_split</b> will take in the univariate dataset and the splitting size(n_test) and split in to train and test. The maximum number of steps to forecast depend on the number of elements in the test datset.

<b>series_to_supervised</b> will take in the training dataset, window size(n_in) and the number of forecasting steps(n_out) and arrange the dataset in to supervised learning. The table below shows how data will be arranged in the case n_in = 3, n_out = 2.
<table style="width:100%">
  <tr>
    <th>Input</th>
    <th>Target</th> 
  </tr>
  <tr>
    <td>[10, 20, 30]</td>
    <td>[40, 50]</td>
  </tr>
  <tr>
    <td>[20, 30, 40]</td>
    <td>[50, 60]</td>
  </tr>
  <tr>
    <td>[30, 40, 50]</td>
    <td>[60, 70]</td>
  </tr>
</table>

<b>measure_rmse</b> is for calculating the root mean squared eroor of predictions and actuals.

<b>difference</b> will take off seasonality of the data. You can specify the order to make the difference. 

<b>model_fit</b> will input train dataset, configuration list which is the collection of hyperparameters you want to check and num_step forecasting. Then it will call to the series_to_supervised function with the data inhand and defined the neural network. Finally feed data to the network and return the model.

<b>model_predict</b> and <b>walk_forward_validation</b> will take the trained model, train dataset and make the first prediction based on the last n_input number of elements of the train dataset called history. After the first element of the test dataset will be added to the history and second prediction will be done by taking last n_input number of elements from the updated history. Also, the mean of the error will be calculated. 
  
<b>repeat_evaluate</b> the above process will be repeated number of n_repeats since the stochastic behavior of nueral networks and take the mean error. 

<b>grid_search</b> will called the repeat_evaluate function for each configuration provided by the <b>model_configs</b>.

Finally best configurtation combination for each forecasting step and the corresponding error will be stored in the list called collection and will be exported in to a csv file as showns in the following table.

<table style="width:100%">
  <tr>
    <th>Predict Step</th>
    <th>Error</th> 
    <th>window width</th>
    <th>Nodes</th>
    <th>Epochs</th>
    <th>batch size</th>
    <th>difference</th>
  </tr>
  <tr>
    <td>1</td>
    <td>29753.24</td>
    <td>5</td>
    <td>70</td>
    <td>160</td>
    <td>10</td>
     <td>0<//td>
  </tr>
  <tr>
    <td>2</td>
    <td>33361.81</td>
    <td>4</td>
    <td>70</td>
    <td>150</td>
    <td>10</td>
     <td>0</td>
  </tr>
  <tr>
    <td>3</td>
    <td>34804.54</td>
    <td>3</td>
    <td>70</td>
    <td>140</td>
    <td>10</td>
     <td>0<//td>
  </tr>
   <tr>
    <td>4</td>
    <td>32095.55</td>
    <td>2</td>
    <td>40</td>
    <td>160</td>
    <td>10</td>
     <td>0</td>
  </tr>
</table>

