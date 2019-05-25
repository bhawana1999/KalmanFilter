# Kalman Filter

A Kalman Filter is a tool that helps to predict values.It is an iterative mathematical process that uses a set of equations and consecutive data inputs to estimate the values we are interested in associated with the object quickly.

The first thing, kalman filters work with gaussians or normal distribution. To define a Gaussian, we have basically two things- mean and variance. 
Mean(μ) you obviously know, Variance(σ²) basically tells how much the numbers are spread out and how far are they from mean. Standard Deviation(σ) is just the square root of Variance(σ²).

A Gaussian in a Kalman Filter represents the predicted value with noise/error/uncertainty in our prediction often known as the variance. The predicted value is centered around the mean with the width of the Gaussian denoting the uncertainty in our value. Basically it tells how much sure we are of a certain value to be true. More the width of the Gaussian denotes more uncertainty.

 It is basically a two step process-
1. Predict
2. Update

In Predict we just predict the new value called predicted value based on the initial value and then predict the uncertainty/error/variance in our prediction according to the various process noises present in the system.

In Update, we take in account the actual measurement coming from the device and we call this as measured value. Here we calculate the difference between our predicted value and measured value and then decide which value to keep by calculating the Kalman Gain. We then calculate the new value and new uncertainty/error/variance based on our decision made by Kalman Gain. These calculated values will finally be the predictions done by our Kalman Filter in iteration 1.

The output of the update step is again fed into the Predict State and the cycle goes on until the error/uncertainty between our predicted and actual values tends to converge to zero.

x -> Mean
P -> Variance

<img src = "" >


<b>Kalman Gain</b> is a parameter which decides how much weight should be given to predicted value and measured value. It is a parameter that decides whether our actual value is close to predicted value or measured value.
               
               K = Error In Prediction / (Error in Prediction + Error in Measurement)

The value of the K ranges from 0 to 1. If we have a large error in measurement, K is nearer to 0,this means our predicted value is close to actual value. If we have a large error in prediction, K is closer to 1, this means our measured value is closer to actual value.
