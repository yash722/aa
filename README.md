**Name:** Yash Rao  
**BU-ID:** U91351678  
**Course Name:** MET CS 767 Advanced Machine Learning and Neural Networks  

## Task 1: Histogram Comparison

**Images Prepared:**  
- Parrot 1  
- Parrot 2  

**Histograms for Each Image:**  
For each image, histograms were created for the three color channels: Red, Blue, and Green channels. This was done using OpenCV's `calcHistogram()` function, followed by normalization to obtain probabilities for each hex value in that channel.

**Summary Table:**

| Channel | D-Statistic | P-Value | Cross Entropy (Parrot 1, Parrot 2) | Cross Entropy (Parrot 2, Parrot 1) | KL-Divergence (Parrot 1, Parrot 2) | KL-Divergence (Parrot 2, Parrot 1) | JS-Divergence (Parrot 1, Parrot 2) |
|---------|-------------|---------|-------------------------------------|-------------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| Red     | 0.188       | 0.0002  | 7.796                               | 7.643                               | 0.118                             | 0.115                             | 0.0283                            |
| Green   | 0.121       | 0.0468  | 7.82                                | 7.976                               | 0.184                             | 0.257                             | 0.051                             |
| Blue    | 0.285       | <<< 0   | 7.346                               | 7.484                               | 0.168                             | 0.192                             | 0.043                             |

**Observations:**
- The P-Values for the KS-Test conducted on the histograms for each channel are all less than the confidence level (0.05), leading to the rejection of the null hypothesis. This implies that the distributions come from different continuous distributions.
- Cross entropy measures the amount of extra information needed to project one image onto another without using extra information from the test image.
- KL-Divergence indicates how similar two distributions are in terms of shape. Lower values suggest greater similarity.
- JS-Divergence is a symmetrical version of KL-Divergence, and low values suggest high similarity between distributions.

## Task 2: GMM Methodology

**Random Dataset Generation:**  
A random dataset was generated using the `make_blobs()` function from the sklearn library. The dataset is three-dimensional with three clusters, totaling 300 rows.

**GMM Methodology:**

1. **Parameter Initialization:** Coefficients (pi-values), means, and covariance matrices for three Gaussian distributions were initialized. 
2. **Expectation Step:** Conditional probabilities of data points belonging to Gaussian distributions were calculated using Bayes' Rule, resulting in a responsibility vector.
3. **Maximization Step:** The responsibility vector was used to update means, coefficients, and covariance matrices.
4. **Iterative Application:** The methodology was applied iteratively over the dataset until convergence, updating parameters using the E-M steps.

**E-M Steps:**
- Epoch 1  
![Epoch 1](epoch_1.png)
- Epoch 2  
![Epoch 2](epoch_2.png)
- Epoch 3  
![Epoch 3](epoch_3.png)
- Epoch 4  
![Epoch 4](epoch_4.png)
- Epoch 5  
![Epoch 5](epoch_5.png)

**Convergence:**  
The convergence plot indicates the convergence of the iterative process.
