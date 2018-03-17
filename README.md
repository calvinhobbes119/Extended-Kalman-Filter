
## Project: Extended-Kalman-Filter [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---
This project implements the Extended Kalman Filter (EKF) for Udacity Self Driving Nano Degree Term 2 Project. It also estimates the performance of the EKF for a test set under different conditions - when both LiDAR and RADAR data is available, when only LiDAR is available, and finally when only RADAR data is available.

[![Both RADAR and LiDAR data available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled.png)](https://youtu.be/6D7yM1h1z3g)

For this project I made the following changes to the started code.

1. Implemented CalculateRMSE and CalculateJacobian methods in tools.cpp.
2. Implemented code to the constructor for the EKF class for initializing the process noise covariance matrix (Q), and the prediction uncertaininty covariance matrix (P). For initializing Q, I assumed a delta_t value of 1s, and acceleration noise variance of 9 m^2/s^4 in the x- and y- directions as suggested in the hints. For initializing P, I assumed that the initial sensor measurements will provide a reasonable estimate for estimating px and py components of the state vector x. So I gave a relatively low uncertaining value to the first two diagonal entries of P (1 m^2), relative to the last two diagonal entries which capture the initial uncertaining in the velocity vx and vy components of the state vector (10 m^2/s^2). I also initialized the measurement matrices for mapping the predicted location to the LiDAR and RADAR measurement space. For the RADAR measurement, I assumed the initial Jacobian matrix to be consistent with a state vector (px, py, vx, vy) = (1, 1, 0, 0). This yielded good results in my testing.

Future improvements
---
I plan to experiment using more data from the challenge track so the car successfully completes the challenge course as well. Currently the car makes it way through roughly 10% of the challenge course before veering off track. The training and validation losses are still fairly high after 20 epochs of training, indicating that the network weights have not yet converged. I am currently testing by increasing the number of epochs as well as collecting more data on the challenge track.
