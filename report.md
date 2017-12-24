# Model Predictive Control Project

---

## The Model

**Student describes their model in detail. This includes the state, actuators and update equations.**

My model is a simple Kinematic Model.
This model has vehicle state [x, y, psi, v, cte, epsi] and actuators [delta, a].

The vehicle state:
```
Vehicle position: x, y
Vehicle orientation: psi
Vehicle velocity: v
Vehicle Cross Track Error: cte
Vehicle Orientation Error: epsi
```

The actuators:
```
Steering angle: delta
Acceleration: a
```

The update equations:
```
x_{t+1} = x_t + v_t * cos(psi) * dt
y_{t+1} = y_t + v_t * sin(psi) * dt
psi_{t+1} = psi_t + v_t * delta_t / Lf * dt
v_{t+1} = v_t + a_t * dt
cte_{t+1} = f(x_t) - y_t + v_t * sin(epsi_t) * dt
epsi_{t+1} = psi_t - psides_t + v_t * delta_t / Lf * dt
```

## Timestep Length and Elapsed Duration (N & dt)

**Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.**

I did manual parameter tuning.
My final parameter values are below:

|Parameter|Value|
|:---:|:---:|
|Timestep length (N)|15|
|Duration (dt)|0.1 [s]|

I tried some N parameters from 5 to 25.
If the value is 15 or more, the car runs without leaving the course.
Generally, long predictions provide more smooth control, but use more computing power.

Next, I tested several dt values from 0.05 to 0.15.
When the value is around 0.1, the running stabilized.


## Polynomial Fitting and MPC Preprocessing

**A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.**

The waypoints are converted from map coordinate system to vehicle's.


## Model Predictive Control with Latency

**The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.**

To accommodate latency, I predicted the state of the vehicle after 100 milliseconds.
The future state of the vehicle is estimated based on the current speed and heading direction.
