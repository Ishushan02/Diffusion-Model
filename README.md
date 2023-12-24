# Diffusion-Model

**Inshort Procedures**
- First we take an Image.
- Add Gaussian Noise to it.**(Forward Process)** (Gaussian because it is assumed that all data is obtained from certain distribution)
- Keep on Adding Gaussian Noise till the time stamp you aim for. (like 0, 1, 2, 3, .... 100)
- Now once till T time stamp the noise image is completely distorted, feed it to U-Net.
- As we already know what noise we had added(true noise) and let the U-Net predict the noise for every iteraion (predicted_noise).
- We try to minimize the loss of (predicted_noise, true noise) using mean squared error. {1/2(predict^2 - true^2)} **(Training Process)**
- After certain iteration we can see that the loss coming down, hence the predicted noise is good enough.
- So, at the end we remove the predicted noise from the image to get clear image. **(Sampling)**


**Forward Process**
- q(X_t|X_t-1) to predict the sampling at time t given the previos one(t-1)
- q(X_t|X_t-1) = Sampling(sqrt(1-beta_t)*X_t-1, beta_t*I) {gaussian Sampling(mean, variance)}
- beta is the random value which will be train and I is the noise which we add 
- q(X(1:T)|X_0) - X from starting procedure till T time stamp initial image X0
- q(X(1:T)|X_0) = pi(q(X_t|X_t-1)) (product of i terms at ith time stamp)
- But in the research paper(Berkeley original paper) it is also given a generic formula which we will use in our code
- q(X_t|X_0) - X at any timestap t given X_0(initial image)
- q(X_t|X_0) = sampling(sqrt(alpha_hat_t)*X0, (1-alpha_hat_t)*I)
- alpha_hat_t = pi(alpha_i); (product of i terms at ith time stamp)
- If we compare the alpha and beta formula we can conclude that alpha = (1-beta)
- hence we return the distorted image and actual noise from forward procedure

**Training Process**
- As we have the true_noise and distorted image, we will feed distorted_image to U-Net.
- The distorted image is fed to U-net to predict the noise
- now we have predicted noise and true noise try to find the mean squared error of it.
- After we find the mean squared, we will then try decreasing the loss.
- The Loss is decreased untill it has reached global optimum

**Sampling Process**
- Now we have to go the reverse way from T, T-1, ...., t ,... 3, 2, 1, 0.
- At each time stamp we have to remove the noise to get back to original good image.
- X_t-1 = [(1/sqrt(alpha_t))*(X_t - ((1-alpha_t)/sqrt(1-alpha_hat_t) * noise))] + variance
- continue this till 0 timestamp at at 0 time stamp make variance as 0


**The above mentioned procedure is executed in the Python File**

**Run the Project**
- I would recommend you to run the project in Colab to see each step output for better clarity at each step.
- Upload any local image to see the following steps of ipython notebook.