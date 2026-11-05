# Formula and algorithm focus list

Unit 1-3 commonly use $\beta$ for discounting and $\gamma$ for the learning rate. Unit 4-5 commonly use $\gamma$ for discounting and $\alpha$ for the learning rate. The actor-critic example also uses $\beta$ as the critic learning rate. Interpret symbols locally.

## [[01_unit_1_introduction_to_reinforcement_learning/01_understanding_reinforcement_learning|1.1 Understanding Reinforcement Learning]]

**Model:** state space, admissible actions, stage cost/reward, transition rule and lifetime/discounting.

**Evaluation:** fix $\phi$, then solve $V^\phi=T^\phi V^\phi$.

**Improvement:** $\phi'(x)\in\arg\min_{a\in A_x}Q^\phi(x,a)$ for costs.

**Optimality:** solve $V^*=T^*V^*$; replace minima by maxima for reward maximization.

**Policy iteration:** evaluate the policy, improve its actions, and repeat until no strict value improvement remains.

## [[01_unit_1_introduction_to_reinforcement_learning/02_components_of_reinforcement_learning_systems|1.2 Components of Reinforcement Learning Systems]]

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

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/01_introduction_to_sequential_decision_making|2.1 Introduction to Sequential Decision Making]]

Route distance is the sum of its edge labels. The source graph has $24$ complete routes.

For a route required to pass through G:

$$
D^*(A,K\mid G)=D^*(A,G)+D^*(G,K).
$$

Compare the best routes through G and H, using their independent segment optima. This reduces the source's first enumeration from 24 full routes to 16 shorter segments.

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/02_dynamic_programming|2.2 Dynamic Programming]]

$$
P(A\mid B)=P(A\cap B)/P(B),\qquad
\mathbb E[X]=\sum_xxP(X=x).
$$

For a fixed policy and additive discounted stochastic costs:

$$
V^\phi(x)=R(x,\phi(x))+\beta\sum_yP(y\mid x,\phi(x))V^\phi(y).
$$

Specify **state, admissible action, cost, transition, lifetime and accrual rule** before optimizing. A fixed MDP policy induces $p_{xy}=P(y\mid x,\phi(x))$.

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/03_bellmans_equation|2.3 Bellman's Equation]]

$$
V^*(x)=\min_{a\in A_x}\left[R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y)\right].
$$

Backward induction uses known later-stage values. Value iteration uses $V^{n+1}=TV^n$. Policy iteration alternates evaluation and improvement.

Dense sweep complexity: $N_xN_a$ deterministic versus $N_x^2N_a$ stochastic. Stagecoach optimum: 15; treasure-search chronological policy: 3, 4, 5 hours if needed.

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/04_general_utility_functions|2.4 General Utility Functions]]

$$
\Delta u^+=u(w+\Delta w)-u(w),\qquad
\Delta u^-=u(w)-u(w-\Delta w).
$$

Risk-averse: $\Delta u^->\Delta u^+$ in the source comparison; risk-seeking reverses the inequality.

$$
V^*(x)=\min_{a\in A_x}\max\{R(x,a),V^*(q(x,a))\}.
$$

Stagecoach minimax optimum: longest segment 3 on A-C-F-H-I-K.

## [[03_unit_3_bandit_problems/01_one_armed_bandit_problem|3.1 The One-Armed Bandit Problem]]

$$
Q\leftarrow Q+\gamma(r-Q),\qquad
\Delta^\Phi=R^*-R^\Phi.
$$

Known-mean one-bandit choice: use the bandit if $\mu>\delta$; otherwise use the fixed alternative.

A selected arm updates its count and mean; unselected arms do not gain observations. A fixed initial sample followed by permanent commitment can preserve a wrong ranking indefinitely.

## [[03_unit_3_bandit_problems/02_multiple_arm_bandit_problem|3.2 The Multiple Arm Bandit Problem]]

Softmax:

$$
\pi_j(k)=\frac{e^{Q_{k,j-1}/\tau}}{\sum_\ell e^{Q_{\ell,j-1}/\tau}}.
$$

Vanishing epsilon-greedy exploration requires the source condition $\sum_j\epsilon_j=\infty$.

UCB1:

$$
I_{k,j}=Q_{k,j-1}+\sqrt{\frac{2\log(j-1)}{n_{k,j-1}}}.
$$

Gradient preferences use reward minus a baseline; uncertainty indices combine estimated reward with an exploration bonus.

## [[04_unit_4_q_learning/01_q_learning_and_time_difference_learning|4.1 Q-Learning and Time-difference Learning]]

$$
Q(s,a)\leftarrow Q(s,a)+\alpha
[r+\gamma\max_bQ(s',b)-Q(s,a)].
$$

SARSA replaces $\max_bQ(s',b)$ with $Q(s',a')$. Here $\alpha$ is learning rate and $\gamma$ is discount, unlike the early-unit symbol choices.

## [[04_unit_4_q_learning/02_reinforcement_learning_with_neural_networks_and_deep_q_learning|4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning]]

$$
Q(s,a;\theta)\approx Q(s,a),\qquad
y=r+\gamma\max_bQ(s',b;\theta),\qquad
L=(y-Q(s,a;\theta))^2.
$$

Compare a state-action input with one Q output against a state input with multiple action-Q outputs. Network approximation replaces storage of independent table entries.

## [[04_unit_4_q_learning/03_experience_replay|4.3 Experience Replay]]

Experience: $(s,a,r,s')$. Store tuples and randomly sample them for training.

$$
P(i)=p_i^\alpha/\sum_kp_k^\alpha.
$$

Random replay reduces sequential correlations; prioritized replay uses remaining TD prediction discrepancy as its motivation. See the note's source sign/magnitude caution before using the printed priority expression.

## [[04_unit_4_q_learning/04_double_q_learning|4.4 Double Q-Learning]]

$$
y^{\rm DoubleDQN}=
r+\gamma Q\left(s',\operatorname*{argmax}_aQ(s',a;\theta);\theta^-\right).
$$

Online network **selects**; target network **evaluates**. Periodic target copying improves stability; decoupled selection/evaluation addresses maximization bias.

## [[04_unit_4_q_learning/05_delayed_sparse_rewards_and_hierarchical_learning|4.5 Delayed Sparse Rewards and Hierarchical Learning]]

Goal-specific value: $V_g(s)$. Universal approximation: $V(s,g;\theta)$.

Hierarchical DQN cycle: choose a goal with the meta-controller, act toward it with the controller, then choose the next goal after completion.

## [[04_unit_4_q_learning/06_value_vs_policy_based_learning|4.6 Value- vs. Policy-Based Learning]]

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

## [[04_unit_4_q_learning/07_actor_critic_learning|4.7 Actor Critic Learning]]

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

## [[05_unit_5_reinforcement_learning_approaches/01_model_free_learning|5.1 Model-Free Learning]]

Every-visit Monte Carlo: generate a complete episode, calculate each visit's return, and average returns by state.

$$
V(s)=\frac1{N(s)}\sum_jG_j(s).
$$

TD learning can update after a single interaction, using a bootstrapped successor value.

## [[05_unit_5_reinforcement_learning_approaches/02_model_based_learning|5.2 Model-Based Learning]]

Model: $\mathcal M_\theta=\{P_\theta,R_\theta\}$ with known state/action spaces.

Dyna combines real experience, model learning and planning.

MCTS: **selection -> expansion -> simulation -> backpropagation**.

MBPO: sample previously encountered states, then use an ensemble for short imagined trajectories instead of one long unreliable rollout.

## [[05_unit_5_reinforcement_learning_approaches/03_exploration_vs_exploitation|5.3 Exploration vs. Exploitation]]

Epsilon-greedy: greedy with $1-\epsilon$, random with $\epsilon$.

$$
P(a\mid s)=\exp(Q(s,a)/T)/\sum_b\exp(Q(s,b)/T).
$$

E3 switches between exploiting a sufficiently good known model and seeking unknown states. R-max makes unknown pairs optimistic. Sweeping prioritizes large **absolute** TD errors.

## [[06_worked_appendices/a_treasure_seeking|Appendix A: Treasure Seeking]]

$$
Q(w,a)=13000(1-e^{-a/13})-700a+e^{-a/13}V^*(w-1,0).
$$

Evaluate six actions, store their maximum and its action, then reuse that maximum as the next iteration's continuation.

## [[06_worked_appendices/b_towers_of_hanoi|Appendix B: Towers of Hanoi]]

$3^N$ states; six possible peg-to-peg move types, restricted by admissibility.

$$
V^*(x)=\min_{a\in A_x}[1+V^*(q(x,a))],\qquad V^*(x_\Delta)=0.
$$

Enumerate with `incState`, access by `pHash`, reconstruct through `policyFunction` and `stateMap`. Three-disk output: seven moves, eight states.

## [[06_worked_appendices/c_switchover_queue_control|Appendix C: Switchover Queue Control]]

$$
\tau=\frac1{2\lambda+\mu},\quad
p_{\text{arrival},i}=\frac{\lambda}{2\lambda+\mu},\quad
p_{\text{service}}=\frac{\mu}{2\lambda+\mu}
$$

for the interior three-event case.

$$
V_{n+1}(x)=\min_a\left[R(x,a)+\beta\sum_yP(y\mid x,a)V_n(y)\right].
$$

Arrays use `(U-1,W1,W2)`; policy entries identify the next served queue.

## [[06_worked_appendices/d_cake_eating|Appendix D: Cake Eating]]

$$
V(w,k)=\max_{0\le c\le w}[u(c)+\beta V(w-c,k-1)].
$$

$$
u'(c)=\beta V_w'(w-c,k-1),\qquad
c_k=\frac{w_k}{\sum_{i=0}^{k-1}\beta^i}
$$

for the source's logarithmic utility. With one stage left, consume all remaining wealth.

## [[06_worked_appendices/e_q_learning_treasure_seeking|Appendix E: Q Learning Treasure Seeking]]

Nonterminal target: $r+\max_bQ(w-1,b)$. Terminal target: $r$.

$$
Q(w,a)\leftarrow Q(w,a)+
\frac{\text{target}-Q(w,a)}{n(w,a)}.
$$

Source vector `[5,4,3]` means one/two/three days remaining; chronological policy is three/four/five hours if needed.
