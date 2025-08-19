# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
## Date: 18/08/2025
## Register No: 212223240128

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from statsmodels.tsa.seasonal import seasonal_decompose

data=pd.read_csv('dc (2).csv')
data.head()

data['date']=pd.to_datetime(data['date'])
data.set_index('date',inplace=True)

data['volume_diff']=data['volume']-data['volume'].shift(1)
result = seasonal_decompose(data['volume'], model='additive', period=12)
data['volume_sea_diff']=result.resid
data['volume_log'] = np.log(data['volume'])
data['volume_log_diff']=data['volume_log']-data['volume_log'].shift(1)
result = seasonal_decompose(data['volume_log_diff'].dropna(), model='additive', period=12)
data['volume_log_seasonal_diff']=result.resid

plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(data['volume'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('date')
plt.ylabel('volume')

plt.subplot(6, 1, 2)
plt.plot(data['volume_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('date')
plt.ylabel('volume')

plt.subplot(6, 1, 3)
plt.plot(data['volume_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('date')
plt.ylabel('volume')

plt.subplot(6, 1, 4)
plt.plot(data['volume_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('date')
plt.ylabel('volume')

plt.subplot(6, 1, 5)
plt.plot(data['volume_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('date')
plt.ylabel('volume')

plt.subplot(6, 1, 6)
plt.plot(data['volume_log_seasonal_diff'], label='Log Transformation and regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('date')
plt.ylabel('volume')

plt.tight_layout()
plt.show()
data.plot(kind='line')
```
### OUTPUT:


REGULAR DIFFERENCING:
<img width="1236" height="179" alt="image" src="https://github.com/user-attachments/assets/80b7cba4-005d-4e4a-8a33-5bd70581411c" />


SEASONAL ADJUSTMENT:

<img width="1167" height="181" alt="image" src="https://github.com/user-attachments/assets/ac9ce313-89a7-40b7-b970-6d5204e53153" />

LOG TRANSFORMATION:
<img width="1028" height="165" alt="image" src="https://github.com/user-attachments/assets/97e10fd0-38e4-4584-89cd-d013349b2672" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
