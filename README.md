# Kalman Filter

A Kalman Filter is a tool that helps to predict values.It is an iterative mathematical process that uses a set of equations and consecutive data inputs to estimate the values we are interested in associated with the object quickly.

The first thing, kalman filters work with gaussians or normal distribution. To define a Gaussian, we have basically two things- mean and variance. 
Mean(μ) you obviously know, Variance(σ²) basically tells how much the numbers are spread out and how far are they from mean. Standard Deviation(σ) is just the square root of Variance(σ²).

<img src ="https://github.com/sona-19/KalmanFilter/blob/master/images/index.jpeg">
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



<b>Mathematical Model</b>

<img src = "https://github.com/sona-19/KalmanFilter/blob/master/images/prediction.jpeg" >

Equations for Predict step
<img src = "https://github.com/sona-19/KalmanFilter/blob/master/images/update.jpeg">


Equations for update step


Suppose we are want to predict the position and velocity of car from the measurements coming from different sensors.

    x -> mean state vector containing position and velocity.
    P -> covariance matrix (denoting error).
    
    
 x vector is given as - 
 
 
 <img src = "https://github.com/sona-19/KalmanFilter/blob/master/images/xvector.gif">
    
 <b>Prediction Step</b>

    Equation 1-:

    x′ = F.x + B.μ + ν

    x′ -> Predicted Value
    F -> State Transition Matrix
    B -> Control Input Matrix
    μ -> Control Vector
    ν -> Process Noise

<b>F Matrix</b>

F is a state transition matrix or an adaptable matrix that are required to convert matrix from one form to the other. For example- say we have a model where we are predicting the position and velocity of the object which is not accelerating. So in this case the new p and v after a time delta t is given as-:

p′ = p + vΔt

v′=v
So in this case the F matrix will be:


<img src = "https://github.com/sona-19/KalmanFilter/blob/master/images/Fmatrix.gif">
F Matrix


<b>B Matrix</b>

B is the control input matrix that denotes the change in state of object due to internal or any external force. For example- the force of gravity or the force of friction to the object.

<b>Why B.μ = 0?</b>

Mostly, in the context of autonomous cars the value of control product vector is equal to zero because we cannot model the external forces acting on objects from the car.


<b>ν</b>

This is the noise in the process. We add random noise that might be present in the channel to make our prediction a little correct.


    Equation 2-:

    P′ = FPFᵀ + Q

    P′ -> Predicted Covariance
    Fᵀ -> Transpose of State Transition Matrix
    Q -> Noise

<b>Q Matrix</b>

We assume that the object changed direction or maybe accelerated or decelerated. So after a time Δt, our uncertainty increases by a factor of Q which is again noise. So we add noise into noise technically.

So in the prediction step we get the two predicted values x′ and P′.


<b>Update Step</b>

    Equation 1:

    y= z - H.x′

    z -> actual measurement
    H -> State Transition Matrix
    x′ -> Predicted Value
    y -> Difference between Measured Value and Actual Value

<b>z</b>

This is the actual measured value that is coming from the sensor.

<b>H</b>

This is again a state transition matrix. With H, we can discard information from the state variable that we do not require. Technically H is doing the same work what F was doing in Prediction Step.

    Equation 2:

    S= HP′Hᵀ + R
    K= P′HᵀS⁻¹

    R -> Measurement Noise
    K -> Kalman Gain
    S-> Total Error
    S⁻¹ -> The inverse of S

<b>R</b>

R denotes the noise in the measurement. What? So those devices are not 100% accurate? Yup, nothing is perfect in this world and not even the devices that measure the values. All devices comes with a predefined value for R parameter that is given by the manufacturer, this value always remains constant throughout the cycle.

<b>K</b>

We have a complex equation here but it is very simple. We are calculating the Kalman Gain K, formula for which was given earlier.


<b>S</b>

This is the total error in the system. The error in our prediction plus the error in measurement.

So why so complicated equation for K as earlier in the formula it was simple?
This is because we do not have a notion of division for matrices. Hence we opt to calculate the total error first and then multiply the error in our prediction with the inverse of total error.

    Equation 3:

    x = x′ + K.y
    P = (I- KH)P′

<b>Final Step</b>

This is the final step where we update our x and P according to the calculations done by the Kalman Gain. Note- On the LHS, we have x and P and not x′ and P′ because we are now setting x and P for the next prediction step, hence we need to find their values.



<img src = "">

<b>References</b>

1. https://towardsdatascience.com/kalman-filter-interview-bdc39f3e6cf3
2. https://www.youtube.com/channel/UCiGxYawhEp4QyFcX0R60YdQ
3. https://github.com/csalinasonline/KalmanMatlabCode
