#Report

###Student describes their model in detail. This includes the state, actuators and update equations.

I use a kinematic bicycle model. The update equations are:

	x_[t+1] = x[t] + v[t] * cos(psi[t]) * dt
	y_[t+1] = y[t] + v[t] * sin(psi[t]) * dt
	psi_[t+1] = psi[t] + v[t] / Lf * delta[t] * dt
	v_[t+1] = v[t] + a[t] * dt
	cte[t+1] = f(x[t]) - y[t] + v[t] * sin(epsi[t]) * dt
	epsi[t+1] = psi[t] - psides[t] + v[t] * delta[t] / Lf * dt


Variable | Meaning
---|---
x,y|position of the car
psi|heading direction
v|velocity
cte|cross-track error
epsi|orientation error

###Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

The time (**T = N * dt**) defines the prediction horizon. Long prediction horizon lead more accurate, and let us control our car smoother. Shorter time stamp (**dt**) also lead more accurate, but it also cost more time.

I tried several values, and then choose to use **[N = 25, dt = 0.05]** which is similar with quiz.

###A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.

First, I transform the waypoints from global coordinate system to the car coordinate system. And then I use a three order polynomial to fit the waypoints.

###The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.

We assum that during the 0.1 second latency, our car drifts at current speed, heading, and rate of trun. Then we just use the state after 0.1 second as initial state for our model.