# Cheatsheet - Unit 4

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[04_unit_4_q_learning/01_q_learning_and_time_difference_learning|4.1 Q-Learning and Time-difference Learning]]

Q-learning replaces model-based expectations with sampled TD targets; SARSA changes the target to the next action selected by the current policy, producing the on-policy versus off-policy distinction.

$$
Q(s,a)\leftarrow Q(s,a)+\alpha
[r+\gamma\max_bQ(s',b)-Q(s,a)].
$$

SARSA replaces $\max_bQ(s',b)$ with $Q(s',a')$. Here $\alpha$ is learning rate and $\gamma$ is discount, unlike the early-unit symbol choices.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=142|Course book pp. 140-150]]

## [[04_unit_4_q_learning/02_reinforcement_learning_with_neural_networks_and_deep_q_learning|4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning]]

A DQN approximates Q-values with learned parameters and features, avoiding independent storage of every state-action value; its bootstrapped, evolving target creates stability problems addressed by later methods.

$$
Q(s,a;\theta)\approx Q(s,a),\qquad
y=r+\gamma\max_bQ(s',b;\theta),\qquad
L=(y-Q(s,a;\theta))^2.
$$

Compare a state-action input with one Q output against a state input with multiple action-Q outputs. Network approximation replaces storage of independent table entries.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=152|Course book pp. 150-153]]

## [[04_unit_4_q_learning/03_experience_replay|4.3 Experience Replay]]

Experience replay stores and reuses state-action-reward-successor tuples; randomized sampling reduces temporal correlations, and prioritized replay concentrates training on experiences expected to improve predictions most.

Experience: $(s,a,r,s')$. Store tuples and randomly sample them for training.

$$
P(i)=p_i^\alpha/\sum_kp_k^\alpha.
$$

Random replay reduces sequential correlations; prioritized replay uses remaining TD prediction discrepancy as its motivation. See the note's source sign/magnitude caution before using the printed priority expression.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=155|Course book pp. 153-154]]

## [[04_unit_4_q_learning/04_double_q_learning|4.4 Double Q-Learning]]

Double DQN separates action selection by the online network from evaluation by the target network, while periodic target copying independently reduces rapid feedback in bootstrapped targets.

$$
y^{\rm DoubleDQN}=
r+\gamma Q\left(s',\operatorname*{argmax}_aQ(s',a;\theta);\theta^-\right).
$$

Online network **selects**; target network **evaluates**. Periodic target copying improves stability; decoupled selection/evaluation addresses maximization bias.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=157|Course book pp. 155-156]]

## [[04_unit_4_q_learning/05_delayed_sparse_rewards_and_hierarchical_learning|4.5 Delayed Sparse Rewards and Hierarchical Learning]]

Sparse delayed rewards make useful feedback difficult to obtain; goal-conditioned values represent different tasks, and hierarchical learning separates selecting goals from acting to accomplish them.

Goal-specific value: $V_g(s)$. Universal approximation: $V(s,g;\theta)$.

Hierarchical DQN cycle: choose a goal with the meta-controller, act toward it with the controller, then choose the next goal after completion.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=158|Course book pp. 156-158]]

## [[04_unit_4_q_learning/06_value_vs_policy_based_learning|4.6 Value- vs. Policy-Based Learning]]

Value-based learning derives a policy from learned action values; policy-based learning directly optimizes policy parameters with gradient ascent, and REINFORCE uses observed returns to estimate the policy-gradient update.

$$
J(\theta)=\mathbb E_{\pi_\theta}\left[\sum_k\gamma^kr_{t+k}\right],
\qquad \theta'\leftarrow\theta+\alpha\nabla_\theta J(\theta).
$$

REINFORCE:

$$
\theta\leftarrow\theta+
\alpha\nabla_\theta\log\pi_\theta(a_i\mid s_i)v_i.
$$

Value-based: derive actions from Q. Policy-based: optimize action-selection parameters directly.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=160|Course book pp. 158-162]]

## [[04_unit_4_q_learning/07_actor_critic_learning|4.7 Actor Critic Learning]]

Actor-critic combines direct policy updates with learned value feedback; advantage centers action quality relative to state value, and the source's synchronous, asynchronous, entropy and surrogate-objective extensions address efficiency, variance and stability.

$$
\Delta\theta=\alpha\nabla_\theta\log\pi_\theta(a\mid s)Q_\omega(s,a),
\qquad
\delta=r+\gamma Q_\omega(s',a')-Q_\omega(s,a).
$$

$$
A(s,a)=Q(s,a)-V(s),\qquad
\hat A=r+\gamma V(s')-V(s).
$$

Actor improves the policy; critic estimates its values. A2C is synchronous, A3C asynchronous; SAC and PPO are introduced at the qualitative level supplied by the book.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=164|Course book pp. 162-168]]
