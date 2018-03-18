## Project: Extended-Kalman-Filter [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---
This project implements the Extended Kalman Filter (EKF) for Udacity Self Driving Nano Degree Term 2 Project. It also estimates the performance of the EKF for a test set under different conditions - when both LiDAR and RADAR data is available, when only LiDAR is available, and finally when only RADAR data is available.

Code changes
---
For this project I made the following changes to the started code.

1. __*tools.cpp*__ Implemented CalculateRMSE and CalculateJacobian methods in tools.cpp.
2. __*EKF.cpp*__ Implemented code to the constructor for the EKF class for initializing the process noise covariance matrix (Q), and the prediction uncertaininty covariance matrix (P). For initializing Q, I assumed a delta_t value of 1s, and acceleration noise variance of 9 m^2/s^4 in the x- and y- directions as suggested in the hints. For initializing P, I assumed that the initial sensor measurements will provide a reasonable estimate for estimating px and py components of the state vector x. So I gave a relatively low uncertaining value to the first two diagonal entries of P (1 m^2), relative to the last two diagonal entries which capture the initial uncertaining in the velocity vx and vy components of the state vector (10 m^2/s^2). I also initialized the measurement matrices for mapping the predicted location to the LiDAR and RADAR measurement space. For the RADAR measurement, I assumed the initial Jacobian matrix to be consistent with a state vector (px, py, vx, vy) = (1, 1, 0, 0). This yielded good results in my testing.
3. __*EKF.cpp*__ Implemented ProcessMeasurement() method for EKF class to initialize the positions within state vector appropriately based on whether the first method is a LiDAR or RADAR measurement. Assume that our initial state for vx and vy is zero. Update the logic for the prediction step to calculate delta_t based on the difference in timestamps between the previous and current measurements, and update Q accordingly. Invoke the predict method of the KalmanFilter object after this update is complete. Update the measurement step to assign the proper measurement and sensor noise covariance matrices based on the type of sensor (LiDAR vs RADAR), and invoke the update method either for a regular Kalman Filter (in the case of a LiDAR sensor which linearly maps the state space to the measurement space), or for an extended Kalman Filter (in the case of a RADAR sensor where the mapping from state space to measurement space is non-linear, and requires the Jacobian matrix to linearize the conversion matrix in the neightborhood of the operating region).
4. __*kalman_filter.cpp*__ Update the Predict() method for the Kalman Filter class. This method is used for predicting the next state based on the current state and measurement time-step (and is independent of the type of sensor). Also, implement the Update() and UpdateEKF() methods based on the calculations as explained in the Udacity videos.

Performance
---
The video below shows the performance of my code when both LiDAR and RADAR data is available. As shown in the video, the RMSE values for the state vector are below the thresholds stated in the Project rubric.

[![Both RADAR and LiDAR data available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled.png)](https://youtu.be/6D7yM1h1z3g)

The next two videos shows the performance of the EKF when only LiDAR or RADAR measurements are used. As expected the RMSE values are worse when only one sensor data is used.

[![Only LiDAR data is available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled.png)](https://youtu.be/lPIjNGOuaVE)

[![Only RADAR data is available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled.png)](https://youtu.be/T0g1Duec7bw)

As an experiment, I changed the code to study the performance when the timesteps between the measurements is only significantly higher than the dataset we have. As expected, the EKF continues to extrapolate the position linearly based on the last available update step leading to drift, and corrects itself whenever new measurement data becomes available.

[![When less frequent measurement updates are available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled1.png)](https://youtu.be/0Bmtsg-pFLk)
