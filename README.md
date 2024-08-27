# Lagrange Interpolation Numerical Method Implementation in Python

This repository contains a Python implementation of the Lagrange Interpolation method for estimating the value of a function at a given interpolating point based on a set of data points. The code reads the data points from an Excel file (`datai.xls`), performs the Lagrange interpolation, and plots the results.

## Table of Contents
- [Lagrange Interpolation Theory](#lagrange-interpolation-theory)
- [Dependencies](#dependencies)
- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
- [Example](#example)
- [Files in the Repository](#files-in-the-repository)
- [Input Parameters](#input-parameters)
- [Troubleshooting](#troubleshooting)
- [Author](#author)

## Lagrange Interpolation Theory
Lagrange Interpolation is a polynomial interpolation method that expresses the interpolating polynomial as a linear combination of Lagrange basis polynomials. It is particularly useful when the data points are distinct and not evenly spaced.

**Formula:**
Given \( n \) data points \((x_0, y_0)\), \((x_1, y_1)\), ..., \((x_{n-1}, y_{n-1})\), the interpolating polynomial \( P(x) \) is given by:
   \[
   P(x) = \sum_{i=0}^{n-1} y_i \prod_{\substack{0 \le j < n \\ j \ne i}} \frac{x - x_j}{x_i - x_j}
   \]

## Dependencies
To run this code, you need the following libraries:
- `numpy`
- `xlrd`
- `matplotlib`

## Installation
To install the required libraries, you can use `pip`:
```sh
pip install numpy xlrd matplotlib
```

## Usage
1. Clone the repository.
2. Ensure the script and the Excel file (`datai.xls`) are in the same directory.
3. Run the script using Python:
    ```sh
    python lagrange_interpolation.py
    ```
4. Provide the required input when prompted:
    - Enter the interpolating point.

## Code Explanation
The code starts by importing the necessary libraries and taking the interpolating point as input. It reads the data points from the Excel file and performs the Lagrange interpolation to compute the value at the specified interpolating point. The results are then plotted.

Below is a snippet from the code illustrating the main logic:

```python
import numpy as np
import xlrd
from matplotlib import pyplot as plt

# Taking necessary input values from keyboard
X = float(input('Enter the interpolating point: '))

# Reading data from excel file
loc = ('datai.xls')
wb = xlrd.open_workbook(loc)
sheet = wb.sheet_by_index(0)

n = sheet.ncols - 1
x = np.zeros([n])
y = np.zeros([n])
Y = 0

for i in range(1, sheet.ncols):
    x[i-1] = sheet.cell_value(0, i)
    y[i-1] = sheet.cell_value(1, i)

# Performing Lagrange interpolation    
for i in range(n):
    a = 1
    b = 1
    for j in range(n):
        if j != i:
            a *= (X - x[j])
            b *= (x[i] - x[j])
    Y += (a / b) * y[i]
    
print('The interpolating result at x = ' + str(Y))

plt.figure(1)
plt.plot(x, y) 
plt.plot(X, Y, 'o')
plt.xlabel('Values of x')
plt.ylabel('Values of y')
plt.title('Graphical verification of the interpolation result')
plt.legend(['Measured', 'Estimated / Interpolated'], loc='best')
plt.show()
```

The code completes by plotting the original data points and the interpolated point using `matplotlib`.

## Example
Below is an example of how to use the script:

1. Prepare the `datai.xls` file with the data points. The first row should contain the \( x \)-values and the second row should contain the corresponding \( y \)-values.
2. **Run the script**:
    ```sh
    python lagrange_interpolation.py
    ```

3. **Enter the input value**:
    ```
    Enter the interpolating point: 2.5
    ```

4. **Output**:
    - The script will compute the interpolated value at the specified point and plot the original data points along with the interpolated point.

## Files in the Repository
- `lagrange_interpolation.py`: The main script for performing Lagrange Interpolation.
- `datai.xls`: Excel file from which the data points are read.

## Input Parameters
The initial input data is expected to be in the form of two rows within the `datai.xls` file:
- First row: \( x \)-values
- Second row: \( y \)-values

## Troubleshooting
1. **Excel File**: Ensure that the input data is correctly formatted and placed in the `datai.xls` file.
2. **Interpolating Point**: Ensure the interpolating point falls within the range of the input \( x \)-values.
3. **Python Version**: This script is compatible with Python 3. Ensure you have Python 3 installed.

## Author
Script created by sudipto3331.

---

This documentation should guide you through understanding, installing, and using the Lagrange Interpolation script. For further issues or feature requests, please open an issue in the repository on GitHub. Feel free to contribute by creating issues and submitting pull requests. Happy coding!
