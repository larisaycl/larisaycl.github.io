---
title: "Unscented Kalman Filter"
excerpt: "Unscented Kalman Filter for localization of a wheeled mobile robot<br/><img src='/images/portfolio-ukf/ukf-gt_vs_ukf.png'>"
collection: portfolio
---

# Overview
This project was done as a homework assignment for CS/ME 469 ML and AI for Robotics at Northwestern. The task was to implement the Unscented Kalman Filter (UKF) from scratch for a mobile robot to localize itself. The UKF was tested on a real robot dataset, and results from filtering were compared to ground truth robot positions measured using a system fo cameras. The datasets used for the project can be found [here](http://asrl.utias.utoronto.ca/datasets/mrclam/index.html). Code is not provided since this is a regular homework assignment. 

# Models
The motion model for the robot was designed based on differential drive kinematics [1] and used as the state transition model for the UKF.

![](/images/portfolio-ukf/ukf-motion_model_1.png)

![](/images/portfolio-ukf/ukf-motion_model_2.png)

The sensor model for the robot was designed based on the range-bearing sensor model and used as the measurement model for the UKF.

![](/images/portfolio-ukf/ukf-sensor_model.png)

# UKF Algorithm
The UKF algorithm is a Bayes filter using a moments parametrization (mean and covari­ance). It assumes that the belief state can be represented by a gaussian (i.e. the initial belief is normally distributed).
Like the Extended Kalman Filter (EKF), it can be used for systems with non­linear dynamics (g) and measurement models (h). It differs from the EKF in how it linearizes the transformation of the gaussian
through non­linear functions. The UKF employs the unscented transform,­ explicitly sampling sigma points from the
gaussian and passing each of them through g and h. These sigma points are sampled at the mean and symmetrically
about the mean for each of the state variables, resulting in 2n + 1 sigma points, where
n is the dimensionality of the state. Sampled sigma points are then passed through the non­linear state­-transition
function g along with the control command at that each timestep the set of transformed sigma points.

More on the UKF can be found at [1] and [2].

# Results
Using only the motion model, robot motion was forward simulated and compared against the ground truth: 

![](/images/portfolio-ukf/ukf-gt_vs_dead.png)

When filtering is applied using the UKF, the simulated robot motion was much closer to the ground truth:

![](/images/portfolio-ukf/ukf-gt_vs_ukf.png)


# References
[1] Thrun, S., Burgard, W., Fox, D. & Arkin, R. (2005). Probabilistic robotics. MIT Press.

[2] Terejanu, G. A. (2011). Unscented kalman filter tutorial. University at Buffalo, Buffalo.