# Transforming Linear Algebra to Computational Language
## Introduction

In the first module, we established a solid foundation in matrix algebra by exploring pseudocode and implementing fundamental matrix operations using Python. We practiced key concepts such as matrix addition, subtraction, multiplication, and determinants through practical examples in image processing, leveraging the `SymPy` library for symbolic computation.

As we begin the second module, **“Transforming Linear Algebra to Computational Language,”** our focus will shift towards applying these concepts with greater depth and actionable insight. This module is designed to bridge the theoretical knowledge from matrix algebra with practical computational applications. You will learn to interpret and utilize matrix operations, solve systems of equations, and analyze the rank of matrices within a variety of real-world contexts.

A new concept we will introduce is the **Rank-Nullity Theorem**, which provides a fundamental relationship between the rank of a matrix and the dimensions of its null space. This theorem is crucial for understanding the solution spaces of linear systems and the properties of linear transformations. By applying this theorem, you will be able to gain deeper insights into the structure of solutions and the behavior of matrix transformations.

This transition will not only reinforce your understanding of linear algebra but also enhance your ability to apply these concepts effectively in computational settings. Through engaging examples and practical exercises, you will gain valuable experience in transforming abstract mathematical principles into tangible solutions, setting a strong groundwork for advanced computational techniques.

## Relearning of Terms and Operations in Linear Algebra
In this section, we will revisit fundamental matrix operations such as addition, subtraction, scaling, and more through practical examples. Our goal is to transform theoretical linear algebra into modern computational applications. We will demonstrate these concepts using Python, focusing on practical and industrial applications.

### Matrix Addition and Subtraction in Data Analysis

Matrix addition and subtraction are fundamental operations that help in combining datasets and analyzing differences.

**Simple Example: Combining Quarterly Sales Data**

We begin with quarterly sales data from different regions and combine them to get the total sales.

**Tabular Data:**

|Region	|Q1	|Q2	|Q3	|Q4|
|--- |--- |---|---|---|
|A	|2500	|2800	|3100	|2900|
|B	|1500	|1600	|1700	|1800|

**From Scratch Python Implementation:**
```python
import numpy as np
import matplotlib.pyplot as plt

# Quarterly sales data
sales_region_a = np.array([2500, 2800, 3100, 2900])
sales_region_b = np.array([1500, 1600, 1700, 1800])

# Combine sales data
total_sales = sales_region_a + sales_region_b

# Visualization
quarters = ['Q1', 'Q2', 'Q3', 'Q4']
plt.bar(quarters, total_sales, color='skyblue')
plt.xlabel('Quarter')
plt.ylabel('Total Sales')
plt.title('Combined Quarterly Sales Data for Regions A and B')
plt.show()
```

Using `pandas` to handle tabular data:

```python
import pandas as pd
import matplotlib.pyplot as plt

# DataFrames for quarterly sales data
df_a = pd.DataFrame({'Q1': [2500], 'Q2': [2800], 'Q3': [3100], 'Q4': [2900]}, index=['Region A'])
df_b = pd.DataFrame({'Q1': [1500], 'Q2': [1600], 'Q3': [1700], 'Q4': [1800]}, index=['Region B'])

# Combine data
df_total = df_a.add(df_b)

# Visualization
df_total.T.plot(kind='bar', color='skyblue')
plt.xlabel('Quarter')
plt.ylabel('Total Sales')
plt.title('Combined Quarterly Sales Data for Regions A and B')
plt.show()
```

We can extend the this in to more advanced examples. Irrespective to the size of the data, for representation aggregation tasks matrix models are best options and are used in industry as a standard. Let us consider an advanced example to analyse difference in stock prices. For this example we are using a simulated data. The python code for this simulation process is shown below:

```python
import numpy as np
import matplotlib.pyplot as plt

# Simulated observed and predicted stock prices
observed_prices = np.random.uniform(100, 200, size=(100, 5))
predicted_prices = np.random.uniform(95, 210, size=(100, 5))

# Calculate the difference matrix
price_differences = observed_prices - predicted_prices

# Visualization
plt.imshow(price_differences, cmap='coolwarm', aspect='auto')
plt.colorbar()
plt.title('Stock Price Differences')
plt.xlabel('Stock Index')
plt.ylabel('Day Index')
plt.show()
```

Another important matrix operation relevant to data analytics and Machine Learning application is scaling. This is considered as a statistical tool to make various features (attributes) in to same scale so as to avoid unnecessary misleading impact in data analysis and its intepretation. In Machine Learning context, this pre-processing stage is inevitable so as to make the model relevant and usable.

**Simple Example: Normalizing Employee Performance Data**

**Tabular Data:**

|Employee	|Metric A	|Metric B|
|--- |--- |---|
|X	|80	|700|
|Y	|90	|800|
|Z	|100	|900|
|A	|110	|1000|
|B	|120	|1100|

Using simple python code we can simulate the model for min-max scaling.

```python
import numpy as np
import matplotlib.pyplot as plt

# Employee performance data with varying scales
data = np.array([[80, 700], [90, 800], [100, 900], [110, 1000], [120, 1100]])

# Manual scaling
min_vals = np.min(data, axis=0)
max_vals = np.max(data, axis=0)
scaled_data = (data - min_vals) / (max_vals - min_vals)

# Visualization
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.imshow(data, cmap='viridis')
plt.title('Original Data')
plt.colorbar()

plt.subplot(1, 2, 2)
plt.imshow(scaled_data, cmap='viridis')
plt.title('Scaled Data')
plt.colorbar()

plt.show()
```

This method will confine the feature values (attributes) into the range $[0,1]$. So in effect all the features are scaled proportionally to the data spectrum.

Similarly we can use the standard scaling (transformation to normal distribution) using the transformation $\dfrac{x-\bar{x}}{S.D.}$. The python code for this operation is given below:

```python
# Standard scaling from scratch
def standard_scaling(data):
    mean = np.mean(data, axis=0)
    std = np.std(data, axis=0)
    scaled_data = (data - mean) / std
    return scaled_data

# Apply standard scaling
scaled_data_scratch = standard_scaling(data)

print("Standard Scaled Data (from scratch):\n", scaled_data_scratch)

# Visualization
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.imshow(data, cmap='viridis')
plt.title('Original Data')
plt.colorbar()

plt.subplot(1, 2, 2)
plt.imshow(scaled_data_scratch, cmap='viridis')
plt.title('Scaled Data')
plt.colorbar()

plt.show()
```

Here we will use one more type of visualization to demonstrate the distribution of data.

```python
import seaborn as sns
# Create plots
plt.figure(figsize=(14, 7))

# Plot for original data
plt.subplot(1, 2, 1)
sns.histplot(data, kde=True, bins=10, palette="viridis")
plt.title('Original Data Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')

# Plot for standard scaled data
plt.subplot(1, 2, 2)
sns.histplot(scaled_data_scratch, kde=True, bins=10, palette="viridis")
plt.title('Standard Scaled Data Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')

plt.tight_layout()
plt.show()
```
A scatter plot showing the impact of scaling is shown below.

```python
# Plot original and scaled data
plt.figure(figsize=(14, 7))

# Original Data
plt.subplot(1, 3, 1)
plt.scatter(data[:, 0], data[:, 1], color='blue')
plt.title('Original Data')
plt.xlabel('Metric A')
plt.ylabel('Metric B')

# Standard Scaled Data
plt.subplot(1, 3, 2)
plt.scatter(scaled_data_scratch[:, 0], scaled_data_scratch[:, 1], color='green')
plt.title('Standard Scaled Data')
plt.xlabel('Metric A (Standard Scaled)')
plt.ylabel('Metric B (Standard Scaled)')

# Min-Max Scaled Data
plt.subplot(1, 3, 3)
plt.scatter(scaled_data[:, 0], scaled_data[:, 1], color='red')
plt.title('Min-Max Scaled Data')
plt.xlabel('Metric A (Min-Max Scaled)')
plt.ylabel('Metric B (Min-Max Scaled)')

plt.tight_layout()
plt.show()
```

We can use the `scikit-learn` library for do the same thing in a very simple handy approach. The python code for this job is shown below.

```python
from sklearn.preprocessing import MinMaxScaler

# Min-max scaling using sklearn
scaler = MinMaxScaler()
min_max_scaled_data_sklearn = scaler.fit_transform(data)

print("Min-Max Scaled Data (using sklearn):\n", min_max_scaled_data_sklearn)
```

```python
from sklearn.preprocessing import StandardScaler

# Standard scaling using sklearn
scaler = StandardScaler()
scaled_data_sklearn = scaler.fit_transform(data)

print("Standard Scaled Data (using sklearn):\n", scaled_data_sklearn)
```

A scatter plot showing the impact on scaling is shown bellow.

```python
# Plot original and scaled data
plt.figure(figsize=(14, 7))

# Original Data
plt.subplot(1, 3, 1)
plt.scatter(data[:, 0], data[:, 1], color='blue')
plt.title('Original Data')
plt.xlabel('Metric A')
plt.ylabel('Metric B')

# Standard Scaled Data
plt.subplot(1, 3, 2)
plt.scatter(scaled_data_sklearn[:, 0], scaled_data_sklearn[:, 1], color='green')
plt.title('Standard Scaled Data')
plt.xlabel('Metric A (Standard Scaled)')
plt.ylabel('Metric B (Standard Scaled)')

# Min-Max Scaled Data
plt.subplot(1, 3, 3)
plt.scatter(min_max_scaled_data_sklearn[:, 0], min_max_scaled_data_sklearn[:, 1], color='red')
plt.title('Min-Max Scaled Data')
plt.xlabel('Metric A (Min-Max Scaled)')
plt.ylabel('Metric B (Min-Max Scaled)')

plt.tight_layout()
plt.show()
```

### More on Matrix Product and its Applications
In the first module of our course, we introduced matrix products as scalar projections, focusing on how matrices interact through basic operations. In this section, we will expand on this by exploring different types of matrix products that have practical importance in various fields. One such product is the Hadamard product, which is particularly useful in applications ranging from image processing to neural networks and statistical analysis. We will cover the definition, properties, and examples of the *Hadamard product*, and then delve into practical applications with simulated data.

#### Hadamard Product
The Hadamard product (or element-wise product) of two matrices is a binary operation that combines two matrices of the same dimensions to produce another matrix of the same dimensions, where each element is the product of corresponding elements in the original matrices.

> [!NOTE]
> ## Definition (Hadamard Product):
> For two matrices $A$ and $B$ of the same dimension $m\times n$, the Hadamard product $A\circ B$ is defined as: $`(A\circ B)_{ij} = A_{ij}\cdot B_{ij}`$ where $\cdot$ denotes element-wise multiplication.

>[!TIP]
> ## Properties of Hadamard Product
> 1. Commutativity: $A \circ B = B \circ A$
> 2. Associativity: $(A \circ B) \circ C = A \circ (B \circ C)$
> 3. Distributivity: $A \circ (B + C) = (A \circ B) + (A \circ C)$

Some simple examples to demonstrate the Hadamard product is given below.

Example 1: Basic Hadamard Product

Given matrices:

$$A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}, \quad
B = \begin{pmatrix}
5 & 6 \\
7 & 8
\end{pmatrix}$$

The Hadamard product $A\circ B$ is:

$$A \circ B = \begin{pmatrix}
1 \cdot 5 & 2 \cdot 6 \\
3 \cdot 7 & 4 \cdot 8
\end{pmatrix} = \begin{pmatrix}
5 & 12 \\
21 & 32
\end{pmatrix}$$

Example 2: Hadamard Product with Larger Matrices

Given matrices:

$$A = \begin{pmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{pmatrix}, \quad
B = \begin{pmatrix}
9 & 8 & 7 \\
6 & 5 & 4 \\
3 & 2 & 1
\end{pmatrix}$$

The Hadamard product $A\circ B$ is:

$$A \circ B = \begin{pmatrix}
1 \cdot 9 & 2 \cdot 8 & 3 \cdot 7 \\
4 \cdot 6 & 5 \cdot 5 & 6 \cdot 4 \\
7 \cdot 3 & 8 \cdot 2 & 9 \cdot 1
\end{pmatrix} = \begin{pmatrix}
9 & 16 & 21 \\
24 & 25 & 24 \\
21 & 16 & 9
\end{pmatrix}$$

In the following code chunks the computational process of Hadamard product is implemented in `Python`. Here both the from the scratch and use of external module versions are included.

**1. Compute Hadamard Product from Scratch (without Libraries)**

Here’s how you can compute the Hadamard product manually:

```python
# Define matrices A and B
A = [[1, 2, 3], [4, 5, 6]]
B = [[7, 8, 9], [10, 11, 12]]

# Function to compute Hadamard product
def hadamard_product(A, B):
    # Get the number of rows and columns
    num_rows = len(A)
    num_cols = len(A[0])
    
    # Initialize the result matrix
    result = [[0]*num_cols for _ in range(num_rows)]
    
    # Compute the Hadamard product
    for i in range(num_rows):
        for j in range(num_cols):
            result[i][j] = A[i][j] * B[i][j]
    
    return result

# Compute Hadamard product
hadamard_product_result = hadamard_product(A, B)

# Display result
print("Hadamard Product (From Scratch):")
for row in hadamard_product_result:
    print(row)
```

**2. Compute Hadamard Product Using** `SymPy`

Here’s how to compute the Hadamard product using `SymPy`:

```python
import sympy as sp

# Define matrices A and B
A = sp.Matrix([[1, 2, 3], [4, 5, 6]])
B = sp.Matrix([[7, 8, 9], [10, 11, 12]])

# Compute Hadamard product using SymPy
Hadamard_product_sympy = A.multiply_elementwise(B)

# Display result
print("Hadamard Product (Using SymPy):")
print(Hadamard_product_sympy)
```

**Practical Applications**

*Application 1: Image Masking*

The Hadamard product can be used for image masking. Here’s how you can apply a mask to an image and visualize it:

```python
import matplotlib.pyplot as plt
import numpy as np

# Simulated large image (2D array) using NumPy
image = np.random.rand(100, 100)

# Simulated mask (binary matrix) using NumPy
mask = np.random.randint(0, 2, size=(100, 100))

# Compute Hadamard product
masked_image = image * mask

# Plot original image and masked image
fig, ax = plt.subplots(1, 2, figsize=(12, 5))
ax[0].imshow(image, cmap='gray')
ax[0].set_title('Original Image')
ax[1].imshow(masked_image, cmap='gray')
ax[1].set_title('Masked Image')
plt.show()
```

*Application 2: Element-wise Scaling in Neural Networks*

The Hadamard product can be used for dropout1 in neural networks. A simple simulated example is given below.

```python
# Simulated large activations (2D array) using NumPy
activations = np.random.rand(100, 100)

# Simulated dropout mask (binary matrix) using NumPy
dropout_mask = np.random.randint(0, 2, size=(100, 100))

# Apply dropout
dropped_activations = activations * dropout_mask

# Display results
print("Original Activations:")
print(activations)
print("\nDropout Mask:")
print(dropout_mask)
print("\nDropped Activations:")
print(dropped_activations)
```

*Application 3: Statistical Data Analysis*

In statistics, the Hadamard product can be applied to scale covariance matrices. Here’s how we can compute the covariance matrix using matrix operations and apply scaling.

```python
import sympy as sp
import numpy as np

# Simulated large dataset (2D array) using NumPy
data = np.random.rand(100, 10)

# Compute the mean of each column
mean = np.mean(data, axis=0)

# Center the data
centered_data = data - mean

# Compute the covariance matrix using matrix product operation
cov_matrix = (centered_data.T @ centered_data) / (centered_data.shape[0] - 1)
cov_matrix_sympy = sp.Matrix(cov_matrix)

# Simulated scaling factors (2D array) using SymPy Matrix
scaling_factors = sp.Matrix(np.random.rand(10, 10))

# Compute Hadamard product
scaled_cov_matrix = cov_matrix_sympy.multiply(scaling_factors)

# Display results
print("Covariance Matrix:")
print(cov_matrix_sympy)
print("\nScaling Factors:")
print(scaling_factors)
print("\nScaled Covariance Matrix:")
print(scaled_cov_matrix)
```

#### Inner Product of Matrices

The inner product of two matrices is a generalized extension of the dot product, where each matrix is treated as a vector in a high-dimensional space. For two matrices $A$ and $B$ of the same dimension $m\times n$, the inner product is defined as the sum of the element-wise products of the matrices.

>[!NOTE]
>## Definition (Inner product)

For two matrices $A$ and $B$ of dimension $m\times n$, the inner product $\langle A, B \rangle$ is given by:

$$\langle A, B \rangle = \sum_{i=1}^{m} \sum_{j=1}^{n} A_{ij} \cdot B_{ij}$$

where $\cdot$ denotes element-wise multiplication.

>[!NOTE]
>## Properties

1. Commutativity: $\langle A, B \rangle = \langle B, A \rangle$

2. Linearity: $\langle A + C, B \rangle = \langle A, B \rangle + \langle C, B \rangle$

3. Positive Definiteness: $\langle A, A \rangle \geq 0$
with equality if and only if $A$ is a zero matrix.

Some simple examples showing the mathematical process of calculating the inner product is given bellow.

**Example 1: Basic Inner Product**

Given matrices:

$$A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}, \quad
B = \begin{pmatrix}
5 & 6 \\
7 & 8
\end{pmatrix}$$

The inner product $\langle A, B \rangle$ is:

$$\langle A, B \rangle = 1 \cdot 5 + 2 \cdot 6 + 3 \cdot 7 + 4 \cdot 8 = 5 + 12 + 21 + 32 = 70$$

**Example 2: Inner Product with Larger Matrices**

Given matrices:

$$A = \begin{pmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{pmatrix}, \quad
B = \begin{pmatrix}
9 & 8 & 7 \\
6 & 5 & 4 \\
3 & 2 & 1
\end{pmatrix}$$

The inner product $\langle A, B \rangle$ is calculated as:

$$\begin{align*}
\langle A, B \rangle &= 1 \cdot 9 + 2 \cdot 8 + 3 \cdot 7 + 4 \cdot 6 + 5 \cdot 5 + 6 \cdot 4 + 7 \cdot 3 + 8 \cdot 2 + 9 \cdot 1\\
&= 9 + 16 + 21 + 24 + 25 + 24 + 21 + 16 + 9\\
&= 175
\end{align*}$$

Now let’s look into the computational part of inner product.

*1.Compute Inner Product from Scratch (without Libraries)*
Here’s how you can compute the inner product from the scratch:

```python
# Define matrices A and B
A = [[1, 2, 3], [4, 5, 6]]
B = [[7, 8, 9], [10, 11, 12]]

# Function to compute inner product
def inner_product(A, B):
    # Get the number of rows and columns
    num_rows = len(A)
    num_cols = len(A[0])
    
    # Initialize the result
    result = 0
    
    # Compute the inner product
    for i in range(num_rows):
        for j in range(num_cols):
            result += A[i][j] * B[i][j]
    
    return result

# Compute inner product
inner_product_result = inner_product(A, B)

# Display result
print("Inner Product (From Scratch):")
print(inner_product_result)
```

*2.Compute Inner Product Using NumPy*
Here’s how to compute the inner product using `Numpy`:

```python
import numpy as np
# Define matrices A and B
A = np.array([[1, 2, 3], [4, 5, 6]])
B = np.array([[7, 8, 9], [10, 11, 12]])
# calculating innerproduct
inner_product = (A*B).sum() # calculate element-wise product, then column sum

print("Inner Product (Using numpy):")
print(inner_product)
```

The same operation can be done using `SymPy` functions as follows.

```python
import sympy as sp
import numpy as np  
# Define matrices A and B
A = sp.Matrix([[1, 2, 3], [4, 5, 6]])
B = sp.Matrix([[7, 8, 9], [10, 11, 12]])

# Compute element-wise product
elementwise_product = A.multiply_elementwise(B)

# Calculate sum of each column
inner_product_sympy = np.sum(elementwise_product)

# Display result
print("Inner Product (Using SymPy):")
print(inner_product_sympy)
```

A vector dot product (in Physics) can be calculated using `SymPy .dot()` function as shown below.

Let  $`A=\begin{pmatrix}1&2&3\end{pmatrix}`$ and  $`B=\begin{pmatrix}4&5&6\end{pmatrix}`$, then the dot product,$`A\cdot B`$ is computed as:

```python
import sympy as sp
A=sp.Matrix([1,2,3])
B=sp.Matrix([4,5,6])
display(A.dot(B)) # calculate fot product of A and B
```

>[!CAUTION]
>In SymPy , `sp.Matrix([1,2,3])` create a column vector. But `np.array([1,2,3])` creates a row vector. So be careful while applying matrix/ dot product operations on these objects.


The same dot product using `numpy` object can be done as follows:

```python
import numpy as np
A=np.array([1,2,3])
B=np.array([4,5,6])
display(A.dot(B.T))# dot() stands for dot product B.T represents the transpose of B
```

**Practical Applications**

*Application 1: Signal Processing*

In signal processing, the inner product can be used to measure the similarity between two signals. Here the most popular measure of similarity is the `cosine` similarity. This measure is defined as:

 $$\cos \theta=\dfrac{A\cdot B}{||A|| ||B||}$$

Now consider two digital signals are given. It’s cosine similarity measure can be calculated with a simulated data as shown below.

```python
import numpy as np

# Simulated large signals (1D array) using NumPy
signal1 = np.sin(np.random.rand(1000))
signal2 = np.cos(np.random.rand(1000))

# Compute inner product
inner_product_signal = np.dot(signal1, signal2)
#cosine_sim=np.dot(signal1,signal2)/(np.linalg.norm(signal1)*np.linalg.norm(signal2))
# Display result
cosine_sim=inner_product_signal/(np.sqrt(np.dot(signal1,signal1))*np.sqrt(np.dot(signal2,signal2)))
print("Inner Product (Using numpy):")
print(inner_product_signal)
print("Similarity of signals:")
print(cosine_sim)
```

*Application 2: Machine Learning - Feature Similarity*

In machine learning, the inner product is used to calculate the similarity between feature vectors.

```python
import numpy as np

# Simulated feature vectors (2D array) using NumPy
features1 = np.random.rand(100, 10)
features2 = np.random.rand(100, 10)

# Compute inner product for each feature vector
inner_products = np.einsum('ij,ij->i', features1, features2) # use Einstien's sum

# Display results
print("Inner Products of Feature Vectors:")
display(inner_products)
```

*Application 3: Covariance Matrix in Statistics*

The inner product can be used to compute covariance matrices for statistical data analysis. If $X$ is a given distribution and $x=X-\bar{X}$. Then the covariance of $X$ can be calculated as $cov(X)=\dfrac{1}{n-1}(x\cdot x^T)$. The python code a simulated data is shown below.

```python
import sympy as sp
import numpy as np

# Simulated large dataset (2D array) using NumPy
data = np.random.rand(100, 10)

# Compute the mean of each column
mean = np.mean(data, axis=0)

# Center the data
centered_data = data - mean

# Compute the covariance matrix using matrix product operation
cov_matrix = (centered_data.T @ centered_data) / (centered_data.shape[0] - 1)
cov_matrix_sympy = sp.Matrix(cov_matrix)

# Display results
print("Covariance Matrix:")
display(cov_matrix_sympy)
```
These examples demonstrate the use of inner product and dot product in various applications.

#### Outer Product
The outer product of two vectors results in a matrix, and it is a way to combine these vectors into a higher-dimensional representation.

>[!NOTE]
>## Definition (Outer Product)

For two vectors $\mathbf{u}$ and $\mathbf{v}$ of dimensions $m$ and $n$ respectively, the outer product $\mathbf{u} \otimes \mathbf{v}$ is an $m\times n$ matrix defined as:

$$(\mathbf{u} \otimes \mathbf{v})_{ij} = u_i \cdot v_j$$

where $\cdot$ denotes the outer product operation. In matrix notation, for two column vectors $u,v$,

$$u\otimes v=uv^T$$

>[!NOTE]
>## Properties

1. Linearity: $(\mathbf{u} + \mathbf{w}) \otimes \mathbf{v} = (\mathbf{u} \otimes \mathbf{v}) + (\mathbf{w} \otimes \mathbf{v})$

2. Distributivity: $\mathbf{u} \otimes (\mathbf{v} + \mathbf{w}) = (\mathbf{u} \otimes \mathbf{v}) + (\mathbf{u} \otimes \mathbf{w})$

3. Associativity: $(\mathbf{u} \otimes \mathbf{v}) \otimes \mathbf{w} = \mathbf{u} \otimes (\mathbf{v} \otimes \mathbf{w})$

Some simple examples of outer product is given below.

**Example 1: Basic Outer Product**

Given vectors:

$$\mathbf{u} = \begin{pmatrix}
1 \\
2
\end{pmatrix}, \quad
\mathbf{v} = \begin{pmatrix}
3 \\
4 \\
5\end{pmatrix}$$

The outer product $\mathbf{u} \otimes \mathbf{v}$ is:

$$\mathbf{u} \otimes \mathbf{v} = \begin{pmatrix}
1 \cdot 3 & 1 \cdot 4 & 1 \cdot 5 \\
2 \cdot 3 & 2 \cdot 4 & 2 \cdot 5
\end{pmatrix} = \begin{pmatrix}
3 & 4 & 5 \\
6 & 8 & 10
\end{pmatrix}$$

**Example 2: Outer Product with Larger Vectors**

Given vectors:

$$\mathbf{u} = \begin{pmatrix}
1 \\
2 \\
3
\end{pmatrix}, \quad
\mathbf{v} = \begin{pmatrix}
4 \\
5
\end{pmatrix}$$

The outer product $\mathbf{u} \otimes \mathbf{v}$ is:

$$\mathbf{u} \otimes \mathbf{v} = \begin{pmatrix}
1 \cdot 4 & 1 \cdot 5 \\
2 \cdot 4 & 2 \cdot 5 \\
3 \cdot 4 & 3 \cdot 5
\end{pmatrix} = \begin{pmatrix}
4 & 5 \\
8 & 10 \\
12 & 15
\end{pmatrix}$$

**1. Compute Outer Product of Vectors from Scratch (without Libraries)**

Here’s how you can compute the outer product manually:

```python
# Define vectors u and v
u = [1, 2]
v = [3, 4, 5]

# Function to compute outer product
def outer_product(u, v):
    # Initialize the result
    result = [[a * b for b in v] for a in u]
    return result

# Compute outer product
outer_product_result = outer_product(u, v)

# Display result
print("Outer Product of Vectors (From Scratch):")
for row in outer_product_result:
    print(row)
```

**2. Compute Outer Product of Vectors Using `SymPy`**

Here’s how to compute the outer product using `SymPy`:

```python
import sympy as sp

# Define vectors u and v
u = sp.Matrix([1, 2])
v = sp.Matrix([3, 4, 5])

# Compute outer product using SymPy
outer_product_sympy = u * v.T

# Display result
print("Outer Product of Vectors (Using SymPy):")
display(outer_product_sympy)
```
**Outer Product of Matrices**

The outer product of two matrices extends the concept from vectors to higher-dimensional tensors. For two matrices $A$ and $B$, the outer product results in a higher-dimensional tensor and is generally expressed as block matrices.

>[!NOTE]
>## Definition (Outer Product of Matrices)

For two matrices $A$ of dimension $m\times p$ and $B$ of dimension $q\times n$, the outer product $A \otimes B$ results in a tensor of dimension $m \times q \times p \times n$. The entries of the tensor are given by:

$$(A \otimes B)_{ijkl} = A_{ij} \cdot B_{kl}$$

where $\cdot$ denotes the outer product operation.

>[!NOTE]
>## Properties

1. Linearity: $(A + C) \otimes B = (A \otimes B) + (C \otimes B)$

2. Distributivity: $A \otimes (B + D) = (A \otimes B) + (A \otimes D)$

3. Associativity: $(A \otimes B) \otimes C = A \otimes (B \otimes C)$

Here are some simple examples to demonstrate the mathematical procedure to find outer product of matrices.

**Example 1: Basic Outer Product of Matrices**

Given matrices:

$$A = \begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}, \quad
B = \begin{pmatrix}
5 \\
6
\end{pmatrix}$$

The outer product $A \otimes B$ is:

$$A \otimes B = \begin{pmatrix}
1 \cdot 5 & 1 \cdot 6 \\
2 \cdot 5 & 2 \cdot 6 \\
3 \cdot 5 & 3 \cdot 6 \\
4 \cdot 5 & 4 \cdot 6
\end{pmatrix} = \begin{pmatrix}
5 & 6 \\
10 & 12 \\
15 & 18 \\
20 & 24
\end{pmatrix}$$

**Example 2: Outer Product with Larger Matrices**

Given matrices:

$$A = \begin{pmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{pmatrix}, \quad
B = \begin{pmatrix}
7 \\
8
\end{pmatrix}$$

The outer product $A \otimes B$ is:

$$A \otimes B = \begin{pmatrix}
1 \cdot 7 & 1 \cdot 8 \\
2 \cdot 7 & 2 \cdot 8 \\
3 \cdot 7 & 3 \cdot 8 \\
4 \cdot 7 & 4 \cdot 8 \\
5 \cdot 7 & 5 \cdot 8 \\
6 \cdot 7 & 6 \cdot 8
\end{pmatrix} = \begin{pmatrix}
7 & 8 \\
14 & 16 \\
21 & 24 \\
28 & 32 \\
35 & 40 \\
42 & 48
\end{pmatrix}$$

**Example 3: Compute the outer product of the following vectors $\mathbf{u} = [0, 1, 2]$ and $\mathbf{v} = [2, 3, 4]$.**

To find the outer product, we calculate each element $(i, j)$ as the product of the $(i)$-th element of $\mathbf{u}$ and the $(j)$-th element of $\mathbf{v}$. Mathematically:

$$\mathbf{u} \otimes \mathbf{v} = \begin{bmatrix}
0 \cdot 2 & 0 \cdot 3 & 0 \cdot 4 \\
1 \cdot 2 & 1 \cdot 3 & 1 \cdot 4 \\
2 \cdot 2 & 2 \cdot 3 & 2 \cdot 4
\end{bmatrix}
= \begin{bmatrix}
0 & 0 & 0 \\
2 & 3 & 4 \\
4 & 6 & 8
\end{bmatrix}$$

**1. Compute Outer Product of Matrices from Scratch (without Libraries)**

Here’s how you can compute the outer product manually:

```python
# Define matrices A and B
A = [[1, 2], [3, 4]]
B = [[5], [6]]

# Function to compute outer product
def outer_product_matrices(A, B):
    m = len(A)
    p = len(A[0])
    q = len(B)
    n = len(B[0])
    result = [[0] * (n * p) for _ in range(m * q)]

    for i in range(m):
        for j in range(p):
            for k in range(q):
                for l in range(n):
                    result[i*q + k][j*n + l] = A[i][j] * B[k][l]

    return result

# Compute outer product
outer_product_result_matrices = outer_product_matrices(A, B)

# Display result
print("Outer Product of Matrices (From Scratch):")
for row in outer_product_result_matrices:
    print(row)
```

Here is the `Python` code to compute the outer product of these vectors using the `NumPy` function `.outer()`:

```python
import numpy as np

# Define vectors
u = np.array([[1,2],[3,4]])
v = np.array([[5],[4]])

# Compute outer product
outer_product = np.outer(u, v)

print("Outer Product of u and v:")
display(outer_product)
```

**Example 3: Real-world Application in Recommendation Systems**

In recommendation systems, the outer product can represent user-item interactions. A simple context is here. Let the user preferences of items is given as $u=[4, 3, 5]$ and the item scores is given by $v=[2, 5, 4]$. Now the recommendation score can be calculated as the outer product of these two vectors. Calculation of this score is shown below. The outer product $\mathbf{u} \otimes \mathbf{v}$ is calculated as follows:

$$\mathbf{u} \otimes \mathbf{v} = \begin{bmatrix}
4 \cdot 2 & 4 \cdot 5 & 4 \cdot 4 \\
3 \cdot 2 & 3 \cdot 5 & 3 \cdot 4 \\
5 \cdot 2 & 5 \cdot 5 & 5 \cdot 4
\end{bmatrix}
= \begin{bmatrix}
8 & 20 & 16 \\
6 & 15 & 12 \\
10 & 25 & 20
\end{bmatrix}$$

The python code for this task is given below.

```python
import numpy as np
import matplotlib.pyplot as plt

# Define the user and product ratings vectors
user_ratings = np.array([4, 3, 5])
product_ratings = np.array([2, 5, 4])

# Compute the outer product
predicted_ratings = np.outer(user_ratings, product_ratings)

# Print the predicted ratings matrix
print("Predicted Ratings Matrix:")
display(predicted_ratings)

# Plot the result
plt.imshow(predicted_ratings, cmap='coolwarm', interpolation='nearest')
plt.colorbar()
plt.title('Predicted Ratings Matrix (Recommendation System)')
plt.xlabel('Product Ratings')
plt.ylabel('User Ratings')
plt.xticks(ticks=np.arange(len(product_ratings)), labels=product_ratings)
plt.yticks(ticks=np.arange(len(user_ratings)), labels=user_ratings)
plt.show()
```

>[!NOTE]
>## Additional Properties & Definitions

1. **Definition and Properties**

Given two vectors:

 - $\mathbf{u} \in \mathbb{R}^m$
 - $\mathbf{v} \in \mathbb{R}^n$

The outer product $\mathbf{u} \otimes \mathbf{v}$ results in an $m \times n$ matrix where each element $(i, j)$ of the matrix is calculated as:

$$(\mathbf{u} \otimes \mathbf{v})_{ij} = u_i \cdot v_j$$

2. **Non-Symmetry**

The outer product is generally not symmetric. For vectors $\mathbf{u}$ and $\mathbf{v}$, the matrix $\mathbf{u} \otimes \mathbf{v}$ is not necessarily equal to $\mathbf{v} \otimes \mathbf{u}$:

$$\mathbf{u} \otimes \mathbf{v} \neq \mathbf{v} \otimes \mathbf{u}$$

3. **Rank of the Outer Product**

The rank of the outer product matrix $\mathbf{u} \otimes \mathbf{v}$ is always 1, provided neither $\mathbf{u}$ nor $\mathbf{v}$ is a zero vector. This is because the matrix can be expressed as a single rank-1 matrix.

4. **Distributive Property**

The outer product is distributive over vector addition. For vectors $\mathbf{u}_1, \mathbf{u}_2 \in \mathbb{R}^m$ and $\mathbf{v} \in \mathbb{R}^n$:

$$(\mathbf{u}_1 + \mathbf{u}_2) \otimes \mathbf{v} = (\mathbf{u}_1 \otimes \mathbf{v}) + (\mathbf{u}_2 \otimes \mathbf{v})$$

5. **Associativity with Scalar Multiplication**

The outer product is associative with scalar multiplication. For a scalar $\alpha$ and vectors $\mathbf{u} \in \mathbb{R}^m$ and $\mathbf{v} \in \mathbb{R}^n$:

$$\alpha (\mathbf{u} \otimes \mathbf{v}) = (\alpha \mathbf{u}) \otimes \mathbf{v} = \mathbf{u} \otimes (\alpha \mathbf{v})$$

6. **Matrix Trace**

The trace of the outer product of two vectors is given by:

$$\text{tr}(\mathbf{u} \otimes \mathbf{v}) = (\mathbf{u}^T \mathbf{v}) \cdot (\mathbf{v}^T \mathbf{u})$$

Here, $\text{tr}$ denotes the trace of a matrix, which is the sum of its diagonal elements.

7. **Matrix Norm**

The Frobenius norm of the outer product matrix can be expressed in terms of the norms of the original vectors:

$$\| \mathbf{u} \otimes \mathbf{v} \|_F = \| \mathbf{u} \|_2 \cdot \| \mathbf{v} \|_2$$

where $\| \cdot \|_2$ denotes the Euclidean norm.

**Example Calculation in** `Python`

Here’s how to compute and visualize the outer product properties using `Python`:

```python
import numpy as np
import matplotlib.pyplot as plt

# Define vectors
u = np.array([1, 2, 3])
v = np.array([4, 5])

# Compute outer product
outer_product = np.outer(u, v)

# Display results
print("Outer Product Matrix:")
print(outer_product)

# Compute and display rank
rank = np.linalg.matrix_rank(outer_product)
print(f"Rank of Outer Product Matrix: {rank}")

# Compute Frobenius norm
frobenius_norm = np.linalg.norm(outer_product, 'fro')
print(f"Frobenius Norm: {frobenius_norm}")

# Plot the result
plt.imshow(outer_product, cmap='viridis', interpolation='nearest')
plt.colorbar()
plt.title('Outer Product Matrix')
plt.xlabel('Vector v')
plt.ylabel('Vector u')
plt.xticks(ticks=np.arange(len(v)), labels=v)
plt.yticks(ticks=np.arange(len(u)), labels=u)
plt.show()
```

## Kronecker Product
In mathematics, the Kronecker product, sometimes denoted by $\otimes$, is an operation on two matrices of arbitrary size resulting in a block matrix. It is a specialization of the tensor product (which is denoted by the same symbol) from vectors to matrices and gives the matrix of the tensor product linear map with respect to a standard choice of basis. The Kronecker product is to be distinguished from the usual matrix multiplication, which is an entirely different operation. The Kronecker product is also sometimes called *matrix direct product*.

>[!NOTE]
>##

If $A$ is an $m\times n$ matrix and $B$ is a $p\times q$ matrix, then the Kronecker product $A\otimes B$ is the $pm \times qn$ block matrix defined as: Each $a_{ij}$ of $A$ is replaced by the matrix $a_{ij}B$. Symbolically this will result in a block matrix defined by:

$$A\otimes B=\begin{bmatrix}A \otimes B = \begin{bmatrix}
a_{11}B & a_{12}B & \cdots & a_{1n}B \\
a_{21}B & a_{22}B & \cdots & a_{2n}B \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1}B & a_{m2}B & \cdots & a_{mn}B
\end{bmatrix} \end{bmatrix}$$

#### Properties of the Kronecker Product
1. **Associativity**

The Kronecker product is associative. For matrices $A \in \mathbb{R}^{m \times n},B \in \mathbb{R}^{p \times q}$ and $C \in \mathbb{R}^{r \times s}$:

$$(A \otimes B) \otimes C = A \otimes (B \otimes C)$$

2. **Distributivity Over Addition**

The Kronecker product distributes over matrix addition. For matrices $A \in \mathbb{R}^{m \times n}, B \in \mathbb{R}^{p \times q}$ and $C \in \mathbb{R}^{p \times q}$:

$$A \otimes (B + C) = (A \otimes B) + (A \otimes C)$$

3. **Mixed Product Property**

The Kronecker product satisfies the mixed product property with the matrix product. For matrices $A \in \mathbb{R}^{m \times n}, B \in \mathbb{R}^{p \times q}, C \in \mathbb{R}^{r \times s}$ and $D \in \mathbb{R}^{r \times s}$:

$$(A \otimes B) (C \otimes D) = (A C) \otimes (B D)$$

4. **Transpose**

The transpose of the Kronecker product is given by:

$$(A \otimes B)^T = A^T \otimes B^T$$

5. **Norm**

The Frobenius norm of the Kronecker product can be computed as:

$$\| A \otimes B \|_F = \| A \|_F \cdot \| B \|_F$$

where $| |_F $ denotes the Frobenius norm.

>[!TIP]
>## Frobenius Norm
>The Frobenius norm, also known as the Euclidean norm for matrices, is a measure of a matrix’s magnitude. It is defined as the square root of the sum of the absolute squares of its elements. Mathematically, for a matrix $A$ with elements $a_{ij}$, the Frobenius norm is given by:

$$\|A\|_F = \sqrt{\sum_{i,j} |a_{ij}|^2}$$

Example 1: Calculation of Frobenius Norm

Consider the matrix $A$:

$$A = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}$$

To compute the Frobenius norm:

$$\|A\|_F = \sqrt{1^2 + 2^2 + 3^2 + 4^2}
= \sqrt{1 + 4 + 9 + 16}
= \sqrt{30}
\approx 5.48$$

Example 2: Frobenius Norm of a Sparse Matrix

Consider the sparse matrix $B$:

$$B = \begin{bmatrix}
0 & 0 & 0 \\
0 & 5 & 0 \\
0 & 0 & 0
\end{bmatrix}$$

To compute the Frobenius norm:

$$\|B\|_F = \sqrt{0^2 + 0^2 + 0^2 + 5^2 + 0^2 + 0^2}
= \sqrt{25}
= 5$$

Example 3: Frobenius Norm in a Large Matrix

Consider the matrix $C$ of size $3$:

$$C = \begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}$$

To compute the Frobenius norm:

$$\begin{align*}
\|C\|_F &= \sqrt{1^2 + 2^2 + 3^2 + 4^2 + 5^2 + 6^2 + 7^2 + 8^2 + 9^2}\\
&= \sqrt{1 + 4 + 9 + 16 + 25 + 36 + 49 + 64 + 81}
&= \sqrt{285}
&\approx 16.88
\end{align*}$$

**Applications of the Frobenius Norm**

 - *Application 1: Image Compression:* In image processing, the Frobenius norm can measure the difference between the original and compressed images, indicating how well the compression has preserved the original image quality.

 - *Application 2: Matrix Factorization:* In numerical analysis, Frobenius norm is used to evaluate the error in matrix approximations, such as in Singular Value Decomposition (SVD). A lower Frobenius norm of the error indicates a better approximation.

 - *Application 3: Error Measurement in Numerical Solutions:* In solving systems of linear equations, the Frobenius norm can be used to measure the error between the true solution and the computed solution, providing insight into the accuracy of numerical methods.

The `linalg` sub module of `NumPy` library can be used to calculate various norms. Basically norm is the generalized form of Euclidean distance.

```python
import numpy as np

# Example 1: Simple Matrix
A = np.array([[1, 2], [3, 4]])
frobenius_norm_A = np.linalg.norm(A, 'fro')
print(f"Frobenius Norm of A: {frobenius_norm_A:.2f}")

# Example 2: Sparse Matrix
B = np.array([[0, 0, 0], [0, 5, 0], [0, 0, 0]])
frobenius_norm_B = np.linalg.norm(B, 'fro')
print(f"Frobenius Norm of B: {frobenius_norm_B:.2f}")

# Example 3: Large Matrix
C = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
frobenius_norm_C = np.linalg.norm(C, 'fro')
print(f"Frobenius Norm of C: {frobenius_norm_C:.2f}")
```

**Frobenius norm of Kronecker product**

Let us consider two matrices,

$$A = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}$$

and

$$B = \begin{bmatrix}
0 & 5 \\
6 & 7
\end{bmatrix}$$

The Kronecker product $C = A \otimes B$ is:

$$C = \begin{bmatrix}
1 \cdot B & 2 \cdot B \\
3 \cdot B & 4 \cdot B
\end{bmatrix}
= \begin{bmatrix}
\begin{bmatrix}
0 & 5 \\
6 & 7
\end{bmatrix} & \begin{bmatrix}
0 \cdot 2 & 5 \cdot 2 \\
6 \cdot 2 & 7 \cdot 2
\end{bmatrix} \\
\begin{bmatrix}
0 \cdot 3 & 5 \cdot 3 \\
6 \cdot 3 & 7 \cdot 3
\end{bmatrix} & \begin{bmatrix}
0 \cdot 4 & 5 \cdot 4 \\
6 \cdot 4 & 7 \cdot 4
\end{bmatrix}
\end{bmatrix}$$

This expands to:

$$C = \begin{bmatrix}
0 & 5 & 0 & 10 \\
6 & 7 & 12 & 14 \\
0 & 15 & 0 & 20 \\
18 & 21 & 24 & 28
\end{bmatrix}$$

*Computing the Frobenius Norm*

To compute the Frobenius norm of $C$:

$$\|C\|_F = \sqrt{\sum_{i=1}^{4} \sum_{j=1}^{4} |c_{ij}|^2}$$

$$\|C\|_F = \sqrt{0^2 + 5^2 + 0^2 + 10^2 + 6^2 + 7^2 + 12^2 + 14^2 + 0^2 + 15^2 + 0^2 + 20^2 + 18^2 + 21^2 + 24^2 + 28^2}$$

$$\|C\|_F = \sqrt{0 + 25 + 0 + 100 + 36 + 49 + 144 + 196 + 0 + 225 + 0 + 400 + 324 + 441 + 576 + 784}$$

$$\|C\|_F = \sqrt{2896}$$

$$\|C\|_F \approx 53.87$$

---

1. A regularization techniques in Deep learning. This approach deactivate some selected neurons to control model over-fitting

2. Remember that the covariance of $X$ is defined as $Cov(X)=\dfrac{\sum (X-\bar{X})^2}{n-1}$.

