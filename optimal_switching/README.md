Version 3 is the latest <br>
Version 3 is simpler, it fixes final regime and work backwards, Version 4 considers both (but not updated yet) <br>

# Class "Profit"
This class contains various payoff and costs elements that define the reward. The final profit value is computed for each date and path.

### terminal reward
The terminal function $\Gamma_T$ is set to an option payoff function of choice regardless of the regime in which the process is at, in this case we have a Max Call. (other choices can be made as well). The terminal payoff is received at maturity, with no other costs nor payoffs.
\begin{equation}
\Gamma(T) = \Big(\max_{d \in \{1, \ldots, D \}} x^d - K   \Big)^{+} \tag{1}
\end{equation}

### running reward
The function $\Psi_i = (\Psi_i(t))_{n \in \mathbb{N}}$ represents the running reward received while in mode $q \in \mathbb{I}$. 
\begin{equation}
\Psi_i(t) = \Big[\Big(\max_{d \in \{1, \ldots, D\}} x^d - K   \Big)^{+} \Big] \tag{2}
\end{equation}

### switching cost
The function $\gamma_{i, j} = (\gamma_{i, j}(t))_{t \in \mathbb{T}}$ with $i,j \in \mathbb{I} = \{0, 1 \}$ represents the cost for switching from mode $i \in \mathbb{I}$ to mode $j \in \mathbb{I}$.
\begin{equation} \tag{3}
\gamma_{0,0} \equiv \gamma_{1,1} \equiv 0 \\
\gamma_{0,1}(t) = \Big(\max_{d \in \{1, \ldots, D \}} x^d - K   \Big)^{+} + \delta  \;\;\;\;\; \delta \sim \mathcal{N}(0,1)   \\ 
\gamma_{1, 0}(t) = - \Big(\max_{d \in \{1, \ldots, D \}} x^d - K   \Big)^{+} 
\end{equation}

### the full expression for the profit
The entire expression for the value of the process at each time $n$ can be represented as: 
\begin{equation} \tag{4}
\tilde{Y}_{T}^i = \Gamma \mathbf{1}_{\{\tau = T\}} 
\end{equation}

\begin{equation}
\begin{aligned}
\tilde{Y}_{t}^i &= - \gamma_{i, j}(\tau) + \Psi_i(\tau) + \mathbb{E}[\tilde{Y}_{t+1}^i | \mathcal{F}_t] \;\;\;\;\; \text{if } i \neq j \text{,   for    } t=T-1, \ldots, 0 \\
&= \Psi_i(\tau) + \mathbb{E}[\tilde{Y}_{t+1}^i | \mathcal{F}_t]  \;\;\;\;\; \text{if } i = j \text{,   for    } t=T-1, \ldots, 0
\end{aligned}
\end{equation}
