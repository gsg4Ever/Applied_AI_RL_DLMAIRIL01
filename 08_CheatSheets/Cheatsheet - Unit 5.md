# Cheatsheet - Unit 5

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[05_unit_5_reinforcement_learning_approaches/01_model_free_learning|5.1 Model-Free Learning]]

Model-free learning uses experience directly: Monte Carlo prediction averages complete episode returns, while TD learns from reward-plus-continuation estimates and can support stepwise control.

Every-visit Monte Carlo: generate a complete episode, calculate each visit's return, and average returns by state.

$$
V(s)=\frac1{N(s)}\sum_jG_j(s).
$$

TD learning can update after a single interaction, using a bootstrapped successor value.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=173|Course book pp. 171-172]]

## [[05_unit_5_reinforcement_learning_approaches/02_model_based_learning|5.2 Model-Based Learning]]

Model-based learning estimates rewards and transitions for planning; Dyna reuses learned information, MCTS limits search, and MBPO limits imagined rollout length to reduce compounded model error.

Model: $\mathcal M_\theta=\{P_\theta,R_\theta\}$ with known state/action spaces.

Dyna combines real experience, model learning and planning.

MCTS: **selection -> expansion -> simulation -> backpropagation**.

MBPO: sample previously encountered states, then use an ensemble for short imagined trajectories instead of one long unreliable rollout.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=174|Course book pp. 172-176]]

## [[05_unit_5_reinforcement_learning_approaches/03_exploration_vs_exploitation|5.3 Exploration vs. Exploitation]]

Exploration trades current reward against useful information: epsilon-greedy and Boltzmann randomize actions, posterior/bootstrapped methods represent uncertainty, curiosity rewards controllable learning, and model-based methods use known-state tests, optimism or prioritized updates.

Epsilon-greedy: greedy with $1-\epsilon$, random with $\epsilon$.

$$
P(a\mid s)=\exp(Q(s,a)/T)/\sum_b\exp(Q(s,b)/T).
$$

E3 switches between exploiting a sufficiently good known model and seeking unknown states. R-max makes unknown pairs optimistic. Sweeping prioritizes large **absolute** TD errors.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=179|Course book pp. 177-181]]
