# Optimal Stopping/Switching
1) this repository contains two version reproducing the results of [Becker, Cheridito and Jetzen's paper](https://www.jmlr.org/papers/volume20/18-232/18-232.pdf) about pricing an American Option via Backward Induction: [optimal_stopping_V1](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_stopping_V1.ipynb), [optimal_stopping_V2](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/optimal_stopping_V2.ipynb)

2) the repository also includes an extension of these version to the optimal switching problem ("start & stop"), taking as reference the work of [Martyr](https://www.jstor.org/stable/44985404) who gives a discrete-time, finite horizon formulation of the problem that suits the optimal stopping counterpart: [opt_switching_V3](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/opt_switching_V3.ipynb), [opt_switching_V4](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/opt_switching_V4.ipynb)

3) the repository contains a version of the least square policy iteration algorithm used to approximate the continuation value (rather than the stopping time), [Lagoudakis](https://www2.cs.duke.edu/research/AI/LSPI/nips01.pdf), [LSPI_V1](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/LSPI_V1.ipynb)

4) links to summary [slides](https://www.overleaf.com/read/wzbgsfncsrgs) and [report](https://www.overleaf.com/project/627d0a7d14dde7bb79b7c757) (the overleaf link tends to be more updated compared to the pdf files inlcuded here, in case the pdf files here to be considered are the latest ones).

A couple of doubts:
1. discounting
2. value of Y in the recursion formula (switching)
3. switching algorithm with both regimes at the end returns the same value at each time step $n$, this is clearly a mistake.

### Optimal switching

Some [results](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/opt_switching_V3.ipynb) on the pricing of a Bermuda max-call option with start and stop decision, with final regime fixed:

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

Some [results](https://github.com/claudia-viaro/optimal_stopping-switching/blob/main/opt_switching_V4.ipynb) on the pricing of a Bermuda max-call option with start and stop decision, with final regime not fixed. $\rightarrow$ there is a mistake here.

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
- step: it reproduces an agent taking an action (control) in the environment, having seen the current state. In this case actions are to stop or to continue (a=0, a=1). Once an action is taken, the system returns a new state (a new price) and a reward (a payoff/continuation value).

I am transferring the switching problem under a RL formulation using OpenAI Gym architecture: [gym_switching](https://github.com/claudia-viaro/gym_switching). It is notproducing any switching yet
