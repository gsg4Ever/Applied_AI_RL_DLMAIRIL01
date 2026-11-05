# Cheatsheet - Unit 1

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[01_unit_1_introduction_to_reinforcement_learning/01_understanding_reinforcement_learning|1.1 Understanding Reinforcement Learning]]

Reinforcement learning optimizes sequential decisions by learning from agent-environment interaction; dynamic programming supplies value, Q-factor and Bellman principles, while learning and approximation address explicit-model and table-size obstacles.

**Model:** state space, admissible actions, stage cost/reward, transition rule and lifetime/discounting.

**Evaluation:** fix $\phi$, then solve $V^\phi=T^\phi V^\phi$.

**Improvement:** $\phi'(x)\in\arg\min_{a\in A_x}Q^\phi(x,a)$ for costs.

**Optimality:** solve $V^*=T^*V^*$; replace minima by maxima for reward maximization.

**Policy iteration:** evaluate the policy, improve its actions, and repeat until no strict value improvement remains.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=14|Course book pp. 12-31]]

## [[01_unit_1_introduction_to_reinforcement_learning/02_components_of_reinforcement_learning_systems|1.2 Components of Reinforcement Learning Systems]]

Policy evaluation learns returns or bootstrapped values; Q-learning and SARSA turn these ideas into control, while continuing exploration, replay and neural-network approximation address data and representation limitations.

$$
\text{new estimate}=\text{old estimate}
+\text{learning rate}\,(\text{target}-\text{old estimate}).
$$

Monte Carlo target: observed episode return. TD(0) target: $r+\beta\widehat V(x')$.

Q-learning target (cost convention): $r+\beta\min_b\widehat Q(x',b)$.

SARSA target: $r+\beta\widehat Q(x',a')$, with $a'$ selected by the behavior policy.

$$
\operatorname{MSE}=\operatorname{variance}+\operatorname{bias}^2.
$$

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=34|Course book pp. 32-50]]
