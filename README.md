# Optimal Stopping/Switching
1) this repository contains two version reproducing the results of [Becker, Cheridito and Jetzen's paper](https://www.jmlr.org/papers/volume20/18-232/18-232.pdf) about pricing an American Option via Backward Induction.

2) the repository also includes an extension of these version to the optimal switching problem ("start & stop"), taking as reference the work of [Martyr](https://www.jstor.org/stable/44985404) who gives a discrete-time, finite horizon formulation of the problem that suits the optimal stopping counterpart.

3) the repository contains a version of the least square policy iteration algorithm used to approximate the continuation value (rather than the stopping time), [Lagoudakis](https://www2.cs.duke.edu/research/AI/LSPI/nips01.pdf)

A couple of doubts:
1. discounting
2. value of Y in the recursion formula (switching)
3. switching algorithm using the second version returns decreasing prices for increasing spot prices, even though the functions used are the same as those used in the first version.


### In progress
I am transferring this same problem (stopping) under a RL formulation using OpenAI Gym architecture. I have created the module environment "gym_stopping" which can be installed as:
- git clone https://github.com/claudia-viaro/gym-stopping
- cd gym-update
- !pip install gym-stopping
- import gym
- import gym_stopping
- env =gym.make('stopping-v0')

The environment follows a standard architecture suitable for most RL existing algorithms.
It contains functions:
- reset: it reset the process and returns the initial state, the spot price (currently just one asset d, but should be increased)
- step: it reproduces an agent taking an action in the environment, having seen the current state. In this case actions are to stop or to continue (a=0, a=1)
