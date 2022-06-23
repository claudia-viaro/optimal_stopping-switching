# Optimal Stopping/Switching - To navigate in this repository
1) this [repository](https://github.com/claudia-viaro/optimal_stopping-switching/tree/main/optimal_stopping) contains two version reproducing the results of [Becker, Cheridito and Jetzen's paper](https://www.jmlr.org/papers/volume20/18-232/18-232.pdf) about pricing an American Option via Backward Induction.

2) this [repository](https://github.com/claudia-viaro/optimal_stopping-switching/tree/main/optimal_switching) also includes an extension of these version to the optimal switching problem ("start & stop"), taking as reference the work of [Martyr](https://www.jstor.org/stable/44985404) who gives a discrete-time, finite horizon formulation of the problem that suits the optimal stopping counterpart.

3) this [repository](https://github.com/claudia-viaro/optimal_stopping-switching/tree/main/LeastSquarePolicyIteration) contains a version of the least square policy iteration algorithm used to approximate the continuation value (rather than the stopping time), [Lagoudakis](https://www2.cs.duke.edu/research/AI/LSPI/nips01.pdf)

4) links to summary [slides](https://www.overleaf.com/read/wzbgsfncsrgs) and [report](https://www.overleaf.com/project/627d0a7d14dde7bb79b7c757) (the overleaf link tends to be more updated compared to the pdf files inlcuded here, in case the pdf files here to be considered are the latest ones).


A couple of doubts:
1. discounting
2. value of Y in the recursion formula (switching)
3. switching algorithm with both regimes at the end returns the same value at each time step $n$, this is clearly a mistake.

### Optimal stopping 
Some [replications](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/opt_switching_V3.ipynb) on the pricing of a Bermuda max-call option with LSPI

| d |  $s_0$  |   L       |   timeL    | 
|---|---------|-----------|------------|
|2  |    90   |    16.015 |    118.778 |  
|2  |    100  |    24.27  |    112.346 |  
|2  |    110  |    32.525 |    104.045 |  
|3  |    90   |    17.821 |    116.851 |  
|3  |    100  |    26.278 |    117.143 |  
|3  |    110  |    34.734 |    118.504 |  
|4  |    90   |    19.075 |    128.681 |  
|4  |    100  |    27.655 |    130.233 |  
|4  |    110  |    36.254 |    159.904 |  
|5  |    90   |    19.97  |    174.879 |  
|5  |    100  |    28.664 |    179.928 |  
|5  |    110  |    37.361 |    170.0   |  
|10 |    90   |    22.438 |    314.409 |  
|10 |    100  |    12.037 |    304.515 |  
|10 |    110  |    40.33  |    312.012 |  
|20 |    90   |    24.15  |    1141.407|  
|20 |    100  |    33.671 |    1146.562|  
|20 |    110  |    42.954 |    1179.293| 

A [version](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_stopping/optimal_stopping_V1.ipynb) of the replication of the optimal stopping pricing from [Becker, Cheridito and Jetzen's paper](https://www.jmlr.org/papers/volume20/18-232/18-232.pdf) can be found here. By inspecting the loss curves produced at each backward recursion, we can observe that the NN is not learning well <br />
![image](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/figures/loss_curves_optStopping.png)

[Here](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_stopping/optimal_stopping_V2.ipynb) there is a second version, although not updated and possibly not that good (slow).

### Optimal switching

Some [results](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_switching/opt_switching_V3.ipynb) on the pricing of a Bermuda max-call option with start and stop decision, with final regime fixed:

| d  | s_0 | Lower bound | Time  |
|----|-----|-------------|-------|
| 2  | 90  | 97.339      | 0.009 |
| 2  | 100 | 205.426     | 0.006 |
| 2  | 110 | 315.878     | 0.007 |
| 4  | 90  | 130.082     | 0.008 |
| 4  | 100 | 235.951     | 0.008 |
| 4  | 110 | 334.079     | 0.005 |
| 5  | 90  | 134.486     | 0.008 |
| 5  | 100 | 224.051     | 0.006 |
| 5  | 110 | 282.737     | 0.006 |
| 10 | 90  | 158.875     | 0.005 |
| 10 | 100 | 273.452     | 0.008 |
| 10 | 110 | 391.043     | 0.015 |
| 20 | 90  | 100.447     | 0.008 |
| 20 | 100 | 192.448     | 0.01  |
| 20 | 110 | 301.107     | 0.009 |

By inspecting the loss curves produced at each backward recursion, we can observe that the NN is not learning well <br />
![image](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/figures/loss_curves_optSwitching.png) <br />


Some [results](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_switching/opt_switching_V4.ipynb) on the pricing of a Bermuda max-call option with start and stop decision, with final regime not fixed. $\rightarrow$ there is a mistake here.

### In progress
I am transferring this same problem (stopping) under a RL formulation using OpenAI Gym architecture [gym-stopping](https://github.com/claudia-viaro/gym-stopping). I have created the module environment "gym_stopping" which can be installed as:
- git clone https://github.com/claudia-viaro/gym-stopping
- cd gym-update
- !pip install gym-stopping
- import gym
- import gym_stopping
- env =gym.make('stopping-v0')

The environment follows a standard architecture suitable for most RL existing algorithms.
It contains functions:
- reset: it reset the process and returns the initial state, the spot price (currently just one asset d, but should be increased)
- step: it reproduces an agent taking an action (control) in the environment, having seen the current state. In this case actions are to stop or to continue (a=0, a=1). Once an action is taken, the system returns a new state (a new price) and a reward (a payoff/continuation value). <br>

I am transferring the switching problem under a RL formulation using OpenAI Gym architecture: [gym_switching](https://github.com/claudia-viaro/gym_switching). It is notproducing any switching yet.  <br>

The neural network approximation used up to now, seems not to be learning well the model. Changes are needed as well as more metrics to evaluate performance.
