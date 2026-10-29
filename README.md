# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 29.10.26

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
ALGORITHM:

1. Import the necessary libraries and upload the car dataset.
2. Extract the price data and calculate its mean and variance.
3. Normalize the data by subtracting the mean.
4. Compute the autocorrelation values for the first 35 lags and store them in an array.
5. Plot the ACF graph and display the autocorrelation values.
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files
from io import BytesIO

# Upload dataset
uploaded = files.upload()

# Read dataset
file_name = next(iter(uploaded))
data = pd.read_csv(BytesIO(uploaded[file_name]))

# Extract car prices
data['price'] = pd.to_numeric(data['price'], errors='coerce')
data = data.dropna(subset=['price'])

data = data['price'].to_numpy()
N = len(data)

# Define lags
lags = range(min(35, N))

# Mean and variance
mean = np.mean(data)
var = np.var(data)

# Normalize data
normalized = data - mean

# Pre-allocate autocorrelation values
acf_values = []

# Compute autocorrelation for each lag
for lag in lags:
    if var == 0:
        acf = 0
    else:
        num = np.sum(normalized[:N-lag] * normalized[lag:])
        den = (N - lag) * var
        acf = num / den
    acf_values.append(acf)

# Display the ACF graph
plt.figure(figsize=(10, 5))
plt.stem(lags, acf_values, basefmt=" ")
plt.xlabel("Lags")
plt.ylabel("ACF")
plt.title("AutoCorrelation Function (First 35 Lags)")
plt.grid(True)
plt.show()

# Display ACF values
print("ACF values for first 35 lags:")
print(acf_values)
```


### OUTPUT:
<img width="947" height="527" alt="image" src="https://github.com/user-attachments/assets/4aaa0b05-d894-48cc-9fd4-b6bec27d4689" />


### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
