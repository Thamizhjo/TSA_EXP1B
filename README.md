# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

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

data = pd.read_csv('asiacup.csv')
df = data.groupby("Year")["Avg Bat Strike Rate"].mean().reset_index()

df['Year'] = pd.to_datetime(df['Year'], format='%Y')
df.set_index('Year', inplace=True)

df['strike_diff'] = df['Avg Bat Strike Rate'] - df['Avg Bat Strike Rate'].shift(1)

result = seasonal_decompose(df['Avg Bat Strike Rate'], model='additive', period=1)
df['strike_sea_diff'] = result.resid

df['strike_log'] = np.log(df['Avg Bat Strike Rate'])
df['strike_log_diff'] = df['strike_log'] - df['strike_log'].shift(1)

result_log = seasonal_decompose(df['strike_log_diff'].dropna(), model='additive', period=1)
df['strike_log_seasonal_diff'] = result_log.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(df['Avg Bat Strike Rate'], label='Original')
plt.legend(loc='best')
plt.title('Original Avg Bat Strike Rate')

plt.subplot(6, 1, 2)
plt.plot(df['strike_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(df['strike_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')

plt.subplot(6, 1, 4)
plt.plot(df['strike_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')

plt.subplot(6, 1, 5)
plt.plot(df['strike_log_diff'], label='Log Transformation + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing')

plt.subplot(6, 1, 6)
plt.plot(df['strike_log_seasonal_diff'], label='Log Transformation + Differencing + Seasonal Adj.')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing + Seasonal Adj.')

plt.tight_layout()
plt.show()

```

### OUTPUT:


ORIGINAL AVG BAT STRIKE RATE:
<img width="1019" height="171" alt="image" src="https://github.com/user-attachments/assets/5d470bf2-0cbf-45c3-9a2e-541c1e8d5403" />
REGULAR DIFFERENCING:
<img width="1005" height="168" alt="image" src="https://github.com/user-attachments/assets/17cc4661-17a5-4759-a3a9-cfe54575cc5f" />
SEASONAL ADJUSTMENT:
<img width="1019" height="177" alt="image" src="https://github.com/user-attachments/assets/0e4dfd1a-3e8d-4b3c-8370-4f229dfd4519" />
LOG TRANSFORMATION:
<img width="1021" height="169" alt="image" src="https://github.com/user-attachments/assets/a2cbe88d-b615-4b9d-9fa1-df02bec3092a" />
LOG TRANSFORMATION + REGULAR DIFFERENCING:
<img width="1005" height="168" alt="image" src="https://github.com/user-attachments/assets/f98b7b4f-8860-4ecd-a31f-794b06ded6de" />
LOG TRANSFORMATION + DIFFERENCING + SEASONAL ADJ.:
<img width="1020" height="173" alt="image" src="https://github.com/user-attachments/assets/73b21ff8-42b3-46f2-b64c-a4d03901d810" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
