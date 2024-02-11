Name – Yash Rao
BU-ID – U91351678
Course Name – MET CS 767 Advanced Machine Learning and Neural Networks

Task – 1

	Images prepared – 
Parrot 1 –
 ![parrot](https://github.com/yash722/aa/assets/63762309/7f03c175-0bc1-429f-8a4c-9d4939c1694b)


Parrot 2 –
 



















	Histograms for each image are made for the three channels, namely, Red, Blue, and Green channels. The same was performed using OpenCV’s calcHistogram() function and then normalised for getting probabilities for each hex value in that channel. The histograms are as follows – 
Parrot 1 – 
Red – 
 

Blue – 
 

Green – 
 

Parrot 2 –
Red –
 



Blue –
 
Green –
 



	Summary table – 
Channel	D-Statistic	P-Value	Cross Entropy (Parrot 1, Parrot 2)	Cross Entropy (Parrot 2, Parrot 1)	KL -Divergence (Parrot 1, Parrot 2)	KL - Divergence (Parrot 2, Parrot 1)	JS - Divergence (Parrot 1, Parrot 2)
Red	0.188	0.0002	7.796	7.643	0.118	0.115	0.0283
Green	0.121	0.0468	7.82	7.976	0.184	0.257	0.051
Blue	0.285	<<< 0	7.346	7.484	0.168	0.192	0.043

Some observations that can be derived from the table – 

	We can clearly see that the P-Values for the KS – Test conducted on the two histograms for each channels sees all of them being less than the confidence level (which we have considered to be 0.05). Hence, we reject the null hypothesis (that is in the favour of the statement that these come from the same continuous distributions), and we accept the alternative hypothesis that informs us that these distributions come from different distributions.
	The cross entropy for both images shows how well we can project one image onto other without the use of extra information from the test image. Using cross entropy, we can see that a higher amount of extra information is needed to project from image 1 to image 2 and vice versa. 
	KL – Divergence shows how two distributions are similar in terms of the shape of those distributions. A lower value of KL – Divergence from image 1 to image 2 as well as from image 2 to image 1 shows that both the histograms are similar in shape (with the value of the same being closer to 0 in all the three channels).
	JS – Divergence is a symmetrical version of the above metrics used, wherein the JS – Divergence from image 1 to image 2 and image 2 to image 1 are equal. The JS -Divergence values from the table displays that both the images are very similar in their distributions. There are relatively small differences in between the histogram distributions in between the two images.















Task – 2

	Random dataset was generated using make_blobs() function from sklearn library. The dataset is a 3-Dimensional dataset with three clusters. It a total of 300 rows.

 

	There are three steps for creating GMM methodology – 
	Initialising the parameters for each gaussian distribution. In our case, we would be using three gaussian distributions for 3 different clusters. The initialisation section of the code describes initialising the coefficients (pi-values), the means of the distribution and covariance matrices for the distribution. The coefficients are defined to be (1/number of clusters), means are chosen as 3 random points from the dataset and the covariance matrices are initialised as identity matrices.
	The Expectation Step, wherein the conditional probability of datapoints belonging to gaussian distributions is calculated. This is implemented using Bayes Rule of conditional probability. The probabilities are then normalised. The resulting  matrix is called a “responsibility” vector, and it is implemented as follows –
γ=p(z ┤|  x)=(π_k N(x ┤| μ_k,Σ_k))/(∑_(i=1)^K▒〖π_i N(x ┤| μ_i,Σ_i)〗)
The log likelihood is calculated as the sum of the logarithms of the conditional probabilities, which is equal to – ∑_(i=1)^N▒〖ln⁡∑_(j=1)^K▒〖π_k N(x ┤| μ_j,Σ_j)〗〗

	The maximization step, wherein the responsibility vector is used to update the means, coefficients, and co-variance matrices. 
N_k= ∑_(n=1)^N▒γ  ; π_k=  N_k/N
μ_k=(∑_(n=1)^N▒γ*x)/N_k 
Σ_k=  (∑_(n=1)^N▒γ(x- μ_k)〖(x- μ_k)〗^T)/N_k 

	The whole methodology is applied iteratively over the whole dataset with the Expectation Step to get responsibilities, get the log-likelihood and check for convergence. If the iteration is not converged yet, we use the maximization step to update the parameters.
The E-M steps are shows as follows – 
Epoch 1  
 

Epoch 2 
 


Epoch 3 
 
Epoch 4  
 

Epoch 5 
 
Convergence – 

 
