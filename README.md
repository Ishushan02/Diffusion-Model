# Diffusion-Model

Inshort Procedures
- First we take an Image.
- Add Gaussian Noise to it.**(Forward Process)** (Gaussian because it is assumed that all data is obtained from certain distribution)
- Keep on Adding Gaussian Noise till the time stamp you aim for. (like 0, 1, 2, 3, .... 100)
- Now once till T time stamp the noise image is completely distorted, feed it to U-Net.
- As we already know what noise we had added(true noise) and let the U-Net predict the noise for every iteraion (predicted_noise).
- We try to minimize the loss of (predicted_noise, true noise) using mean squared error. {1/2(predict^2 - true^2)} **(Training Process)**
- After certain iteration we can see that the loss coming down, hence the predicted noise is good enough.
- So, at the end we remove the predicted noise from the image to get clear image. **(Sampling)**



                                                                                           