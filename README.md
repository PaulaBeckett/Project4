# Neural Network Report

## Project Aim

The aim of this project is to explore the relationship between machine telemetry elements and the predictability that the machine might require maintenance in the future.

## Dataset

https://www.kaggle.com/datasets/arnabbiswas1/microsoft-azure-predictive-maintenance

Included 5 csv files that detailed the following for 100 machines over a one-year period:
*	Machine Age
*	Machine Model
*	Hourly averages of Voltage, Rotation, Pressure & Vibration
*	Error codes, if occurred
*	Maintenance undertaken.
*	Failures that occurred.

### Data Cleaning

Data was imported to PgAdmin and all tables merged, joined on a unique MachineID and matching Datetime.

Our target variable was determined to be the 'compfail' columns which identified instances of machine failure & the component impacted.
Assumption was made that all failures were of equal value, therefore 'compfail' column updated to 0 for no failure, and 1 for any failure.

### Data Exploration

Examples:
* Visualisation of telemetry points (volt, rotate, pressure, vibration) of one machine over the 1-year period
* Visualisation of one machines telemetry over a short period of time to see if there was any visual presentation of upcoming failures
* Numbers of failures per machine, errors per machine
* Numbers of each error, and on which components maintenance was conducted
* Seaborn correlation heatmap
* Distribution of machine models and ages

## Machine Learning

### Random Forest

Modelling using the RandomForestClassifier from the Scikit-learn library

High accuracy result from modelling on Machine 99.

High accuracy, but low result on the target variable for Machine 98.

High accuracy and moderate result on the target variable for Machines 90-100.

### Neural Network

Manual parameters set and tested with similar accuracy results to the RandomForest, but lower results on the target variable.

Keras Tuner Hyperband modelling run to determine the best parameters.

Run for Machine 98
* Objective val_accuracy resulted in a very high accuracy but still no predictions of failure.
* Objective val_true_positives resulted in a very low accuracy reading overall
* Multi Objective for val_accuracy & val_true_positives gave high accuracy and high result of true failures

Run for Machine 99
* Multi Objective tuning run with same objectives as machine 98 above, results were almost identical


## Summary

In conclusion it would look like either the RandomForest or keras.tuner model would suffice to acheive a model with accuracy exceeding 98%

As we are looking to determine possible failures, and the RandomForest was less reliable with predicting these failures it would be recommended to 
look deeper into the keras.tuner hyperband optimisation.

Further telemetry data would also be beneficial & personalised for the industry/machine/equipment being monitored.

## Files

Resources
* PdM_errors.csv
* PdM_machines.csv
* PdM_maint.csv
* PdM_failures.csv
* all_tele_main.csv (a reduction of the original PdM_telemetry file which was too large for GitHub)
* machine_98.csv (merged file for Machine 98 only)

Data Exploration
* PredictiveMaintenanceEDA.ipynb

Random Forest Classifier
* PdM_RandomForest_Machine98.ipynb
* PdM_RandomForest_Machine99.ipynb
* PdM_RandomForest_MachinesOver90.ipynb

Neural Network
* PdM_NN_AllMachines_IncDate.ipynb
* PdM_NN_Machine98_Optimisation.ipynb
* PdM_NN_Machine99_Optimisation.ipynb
* PdM_NN_Machine99.ipynb
* PdM_NN_Machine98.ipynb