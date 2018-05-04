** RUBRIC POINTS **

[//]: # (Image references)
[image1]: ./model.png "Model"

### Student describes their model in detail. This includes the state, actuators and update equations.

The model used in this project is the kinematic model. The equations can be seen in MPC.cpp lines 134-141. Mathematically they are as follows:

[Model](./model.png)

### Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

I finally settled on using N = 10 and dt = 0.1. I arrived at this combination after several permutation of N and dt ranging from N = 25, dt = 0.05 to N = 7, dt = 0.1. For higher values of Nxdt the car would keep oscillating between the reference trajectory and would eventually leave the road. For lower values of Nxdt the car wasn't performing optimally and increasing the value of N produced better results.

### A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described. 

I had to translate and rotate the coordinate axes to the vehicle's perspective. I did this to make my calculations easier so that the initial x, y and psi are zero. I first did the translation and then the rotation so that the origins coincide.

### The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.

My model handles a latency of 100ms in lines 119-123 of MPC.cpp.
I had the nice property of latency (0.1 sec) to be equal to the chosen dt (0.1 sec). So what I did was, that I update my actuator values to one timestep earlier than a model with no latency. In this way the latency is incorporated in the model.