
# LSTM-based Weather Forecasting from European Capital City Data

This project was created as part of the Deep Machine Learning course at Óbuda University. Its goal is to implement a deep learning model that, based on meteorological data from several European capitals, can predict the daily maximum temperature.

## Topic selection and objective

The aim of the project is to create a forecasting pipeline using an LSTM-based model with the help of an existing open meteorological dataset. The task includes:
- querying and processing raw data,
- preparing time-based features based on data from multiple cities,
- creating training and validation sets in the form of time-windowed sequences,
- training and optimizing an LSTM model,
- evaluating and visualizing the model.

## Data source

- The data was queried via the public API of [Meteostat](https://dev.meteostat.net/).
- The data has daily resolution and includes the following features:
  - daily average temperature (`tavg`)
  - minimum temperature (`tmin`)
  - maximum temperature (`tmax`)
  - precipitation (`prcp`)
  - wind speed (`wspd`)

Data was only used if it was fully available for the given city and feature throughout the entire examined time interval (2000–2024).

## Model and pipeline

- The implementation is based on an LSTM (Long Short-Term Memory) neural network.
- The input data consists of multiple features from several European capitals, in the form of time-windowed sequences.
- The target variable is the prediction of the `tmax` value for a selected city.

### Model parameters
- `hidden_size`: 16–128         (recommended: 32)
- `batch_size`: 64–4096         (recommended: 1024)
- `learning_rate`: 0.0001–0.003 (recommended: 0.001)
- `num_layers`: 1 or 2          (recommended: 1)
- `window_size`: 7 days         (not tested with other values)

Early stopping and saving of training curves were used during training.

## Evaluation

Models were compared based on several metrics:
- **Mean Absolute Error (MAE)**
- **Mean Squared Error (MSE)**
- training time (in seconds)

The evaluation results are available in `.csv` format in the `training_log.csv` file, and the training curves for each epoch are also logged.

![All_training](https://github.com/alenoi/Weather-prediction-with-LSTM/blob/main/plots/all_training_curves.png)
![Top3_training](https://github.com/alenoi/Weather-prediction-with-LSTM/blob/main/plots/top3_training_curves.png)

## Project structure


```
oe_deep-ml/
├── logs/ # Log files for training curves and metrics
├── models/ # Trained models (.pt)
├── plots/ # Plots of training curves
├── training_log.csv # Hyperparameter tuning results
├── worldcities.csv # City coordinates (SimpleMaps)
├── european_capitals_weather.csv # Merged, processed data
├── weather_data_train.ipynb # Data collection and preparation & model training and logging
├── weather_inference.ipynb # Model loading and inference
├── results_analysis.ipynb # Evaluation of hyperparameter tuning results
```

## Key takeaways

- Optimization of `batch_size` and `learning_rate` has a significant impact on performance.
- Too large hidden layers led to overfitting and poor generalization.
- Standardizing the `tmax` target variable caused biased predictions, so the final model was trained on the original scale.
- Training curves and early stopping helped avoid overfitting.

## Result

- Train Loss:                   4.497498  
- Mean Absolute Error (MAE):    2.054539  
- Mean Squared Error (MSE):     6.802113  
- Training time (in seconds):   30.13 s  

![Result](https://github.com/alenoi/Weather-prediction-with-LSTM/blob/main/Result.png?raw=true)

## Requirements

- Python 3.10+
- numpy
- pandas
- torch
- matplotlib
- scikit-learn
- meteostat
- geopy

## License

MIT License — freely usable for educational and research purposes.
