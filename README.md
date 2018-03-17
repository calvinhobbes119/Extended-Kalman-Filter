## Project: Extended-Kalman-Filter [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---
This project implements the Extended Kalman Filter (EKF) for Udacity Self Driving Nano Degree Term 2 Project. It also estimates the performance of the EKF for a test set under different conditions - when both LiDAR and RADAR data is available, when only LiDAR is available, and finally when only RADAR data is available.

[![Both RADAR and LiDAR data available](https://github.com/calvinhobbes119/Extended-Kalman-Filter/blob/master/Untitled.png)](https://youtu.be/6D7yM1h1z3g)

Future improvements
---
I plan to experiment using more data from the challenge track so the car successfully completes the challenge course as well. Currently the car makes it way through roughly 10% of the challenge course before veering off track. The training and validation losses are still fairly high after 20 epochs of training, indicating that the network weights have not yet converged. I am currently testing by increasing the number of epochs as well as collecting more data on the challenge track.
