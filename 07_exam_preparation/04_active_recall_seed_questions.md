# Active recall seed questions

Answer these without the notes. These are generated study questions grounded in the supplied book, not official exam questions.

## [[01_unit_1_introduction_to_reinforcement_learning/01_understanding_reinforcement_learning|1.1 Understanding Reinforcement Learning]]

1. What distinguishes reinforcement learning from supervised learning?
2. How do feature selection and feature extraction differ?
3. What is certainty-equivalence control?
4. What makes a state-action pair admissible?
5. How do deterministic and stochastic transitions differ?
6. What are the three SDP lifetimes in the book?
7. Why discount bounded infinite-horizon costs?
8. What does a policy value function evaluate?
9. What does a Q-factor evaluate?
10. How does Bellman optimality differ from fixed-policy evaluation?
11. How do value iteration and policy iteration differ?
12. What are the two explicit-model obstacles in the poker example?
13. What does the environment output after an action?
14. Which action wins the source's state-3 cost comparison?

## [[01_unit_1_introduction_to_reinforcement_learning/02_components_of_reinforcement_learning_systems|1.2 Components of Reinforcement Learning Systems]]

1. How is an episodic policy value estimated by Monte Carlo?
2. What is the difference between first-visit and every-visit evaluation?
3. What is the general incremental update pattern?
4. Why is learning rate one risky for noisy targets?
5. What does bootstrapping mean?
6. What are the components of mean squared error?
7. What do TD(0) and TD(1) denote in this unit?
8. What does the trace-decay parameter control?
9. How does Q-learning's target differ from SARSA's?
10. Why can a greedy policy get stuck?
11. What does epsilon-greedy combine?
12. How does hindsight replay use a failed episode?
13. What is the purpose of neural-network value approximation?
14. What do the poker network's early hidden layers represent?

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/01_introduction_to_sequential_decision_making|2.1 Introduction to Sequential Decision Making]]

1. What is a sequential decision process?
2. What is constructive enumeration?
3. How many complete routes are in the source stagecoach map?
4. Why does brute-force enumeration scale poorly?
5. Why can the continuation from G be optimized independently?
6. What does the constraint in D*(A,K given G) mean?
7. What is the first decomposition's route-count saving?

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/02_dynamic_programming|2.2 Dynamic Programming]]

1. What does a random variable's support contain?
2. What are the core SDP model components?
3. Why add a dummy action to a terminal state?
4. How do time homogeneity and finite horizon differ?
5. Why can a stage index be included in a state?
6. How does minimax cost differ from total cost?
7. What does the maximin fuel example optimize?
8. Why is irrelevant history undesirable?
9. Why does the expected-value recursion suit additive costs?
10. Can expectation generally be moved through a maximum?
11. What does fixing an MDP policy produce?
12. What is the source coin example's probability of three heads given an odd count?

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/03_bellmans_equation|2.3 Bellman's Equation]]

1. What does Bellman's principle optimize?
2. Why begin backward induction at the terminal stage?
3. What is the optimal stagecoach distance?
4. Why does the one-time-sale modification break the original memoryless model?
5. What must the treasure-search state contain?
6. What is the source's three-day treasure policy?
7. What expected value does the source report for three remaining days?
8. What is a Bellman fixed point?
9. How does policy evaluation differ from policy optimization?
10. Why can optimal policies be nonunique?
11. What are dense deterministic and stochastic sweep complexities?
12. When can sparse transitions reduce stochastic complexity?
13. What causes the source ten-queue example to become infeasible?

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/04_general_utility_functions|2.4 General Utility Functions]]

1. Why might expected monetary payoff be insufficient?
2. What does a utility curve's slope represent?
3. How does a thirsty customer's marginal utility change?
4. Which utility shapes represent risk-aversion, neutrality and seeking?
5. How does concavity compare equal-sized gains and losses?
6. What does the minimax stagecoach criterion minimize?
7. Which source route is minimax-optimal?
8. Why can total-distance-optimal routes differ under minimax?

## [[03_unit_3_bandit_problems/01_one_armed_bandit_problem|3.1 The One-Armed Bandit Problem]]

1. What is a one-armed bandit in this book?
2. If the bandit mean is known, when should it beat the fixed alternative?
3. What does a stage discount sequence define?
4. What is the incremental reward-estimate update?
5. Which count determines a running mean's step size?
6. What is regret?
7. Why can fixed initial sampling followed by permanent commitment fail?
8. What remains wrong with updating only the chosen bandit?

## [[03_unit_3_bandit_problems/02_multiple_arm_bandit_problem|3.2 The Multiple Arm Bandit Problem]]

1. Why does the source's greedy three-arm policy sometimes choose arm 2 forever?
2. What does forced exploration prevent?
3. What is the cost of a constant epsilon in the long run?
4. What condition does the book give for vanishing exploration?
5. How does softmax temperature affect selection?
6. What does a gradient bandit policy learn?
7. Why does adding a common preference constant leave softmax unchanged?
8. What are the two components of an uncertainty-based index?
9. How does a one-sided confidence bound differ from a two-sided interval?
10. What is the source's 95% confidence interval for mean 34.6 and standard deviation 5.7 with n=5?
11. What is the corresponding one-sided 95% upper bound?
12. What does UCB1 add to the current reward estimate?
13. How do the two counts in UCB1 differ?
14. Does UCB1's displayed bonus use a sample variance or t critical value?

## [[04_unit_4_q_learning/01_q_learning_and_time_difference_learning|4.1 Q-Learning and Time-difference Learning]]

1. What is Q1 for the last remaining action?
2. How do a Q-value, state value and policy differ?
3. What replaces unknown transition probabilities in Q-learning?
4. What is Q-learning's target?
5. What is the TD error?
6. What does the learning rate control?
7. What makes SARSA on-policy?
8. Why is Q-learning off-policy?
9. What is an episode?
10. What continuation is used after termination?

## [[04_unit_4_q_learning/02_reinforcement_learning_with_neural_networks_and_deep_q_learning|4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning]]

1. Why does a tabular Q representation become impractical?
2. What does theta represent in Q(s,a;theta)?
3. How does the Atari DQN obtain features?
4. What are the two network architectures in Figure 20?
5. What is the source's DQN target?
6. Why is the DQN target different from a fixed supervised label?
7. Why can naive neural-network Q-learning become unstable?

## [[04_unit_4_q_learning/03_experience_replay|4.3 Experience Replay]]

1. What does an experience tuple contain?
2. Why store a replay buffer?
3. Why randomly sample from replay?
4. What does uniform replay ignore?
5. What motivates prioritized replay in the book?
6. What does the priority exponent control?

## [[04_unit_4_q_learning/04_double_q_learning|4.4 Double Q-Learning]]

1. Why use a target-network copy?
2. What target refresh interval does the cited original DQN example report?
3. What causes maximization bias?
4. Which network selects the next action in Double DQN?
5. Which network evaluates that selected action?
6. Are target stabilization and Double Q selection/evaluation separation identical?

## [[04_unit_4_q_learning/05_delayed_sparse_rewards_and_hierarchical_learning|4.5 Delayed Sparse Rewards and Hierarchical Learning]]

1. Why is the blind cliff walk hard to learn?
2. What does Vg(s) represent?
3. What do demons do in the Horde architecture?
4. How does a universal value function differ?
5. What does the meta-controller choose?
6. What does the lower-level controller choose?
7. Why is independent knowledge of goals not always sufficient?

## [[04_unit_4_q_learning/06_value_vs_policy_based_learning|4.6 Value- vs. Policy-Based Learning]]

1. How does value-based learning obtain a policy?
2. What does policy-based learning optimize directly?
3. How do deterministic and stochastic policies differ?
4. What does the policy objective J represent?
5. Why does the parameter update use gradient ascent?
6. What weights the source policy-gradient expression?
7. What does REINFORCE substitute for that action value?
8. Why is the presented policy-gradient approach on-policy?

## [[04_unit_4_q_learning/07_actor_critic_learning|4.7 Actor Critic Learning]]

1. What do actor and critic learn?
2. Why can learned actor-critic updates fail to improve a policy?
3. Why does the basic critic update have no next-action maximum?
4. Are the actor and critic learning rates necessarily identical?
5. What is the advantage function?
6. What provides the source's sampled advantage estimate?
7. How do A2C and A3C differ?
8. What does Soft Actor Critic add to reward optimization?
9. How does the book describe PPO stabilization?

## [[05_unit_5_reinforcement_learning_approaches/01_model_free_learning|5.1 Model-Free Learning]]

1. What does a model-free method avoid building first?
2. What is the difference between prediction and control?
3. What does every visit mean in Monte Carlo evaluation?
4. What is averaged to estimate a state value?
5. Why does the presented Monte Carlo procedure need termination?
6. How can TD update earlier?
7. How does SARSA's successor target differ from Q-learning's?

## [[05_unit_5_reinforcement_learning_approaches/02_model_based_learning|5.2 Model-Based Learning]]

1. What does an estimated model contain?
2. Why is planning on a learned model approximate?
3. What does Dyna combine?
4. Which disagreement matters to Ready Policy One?
5. Why can a perfect game model still be hard to use?
6. What are MCTS's four stages?
7. What is propagated during MCTS backpropagation?
8. What does the source say AlphaGo combines?
9. Why does MBPO use short imagined trajectories?
10. Where do MBPO's rollout starting states come from?
11. How many environments are in the cited model-based benchmark?

## [[05_unit_5_reinforcement_learning_approaches/03_exploration_vs_exploitation|5.3 Exploration vs. Exploitation]]

1. What can greedy exploitation miss?
2. How does Boltzmann exploration differ from uniform random exploration?
3. What happens to finite-action Boltzmann probabilities at high temperature?
4. What information guides Thompson sampling?
5. How does bootstrapped DQN represent uncertainty?
6. Why add intrinsic curiosity reward?
7. Why not reward prediction errors from rustling leaves?
8. When does an E3 state become known?
9. How does E3 act in unknown states?
10. What reward does R-max assign to unknown pairs?
11. Does Dyna alone define a behavior action policy?
12. What discrepancy motivates prioritized sweeping?

## [[06_worked_appendices/a_treasure_seeking|Appendix A: Treasure Seeking]]

1. What does valueTemp contain before a new recursion step?
2. Why is the continuation multiplied by exp(-a/13)?
3. Why are six candidate values sufficient at each step?
4. What does the policy list store?
5. How many iterations does the source program specify?
6. What does the horizontal axis of the output mean?
7. What is the three-day chronological policy?

## [[06_worked_appendices/b_towers_of_hanoi|Appendix B: Towers of Hanoi]]

1. Why is disk-to-peg membership sufficient to define a state?
2. How many states are represented for N disks?
3. What makes a potential peg-to-peg move illegal?
4. What objective does the one-unit move cost encode?
5. What does incState do?
6. What does pHash do?
7. Why keep old and new value arrays?
8. What does the stored policy contain?
9. Why does the output contain one more state than moves?
10. What result does the source report for three disks?

## [[06_worked_appendices/c_switchover_queue_control|Appendix C: Switchover Queue Control]]

1. What information is needed in the switchover state?
2. What do the two cost components represent?
3. What is the interior total event rate?
4. How is each next-event probability calculated?
5. Why do boundary transition probabilities change?
6. How many states are represented at capacity K?
7. What is the value array's index order?
8. What does a policy matrix entry mean?
9. What does makeTransitionList provide?
10. Does a policy entry equal the value function?
11. What does the convergence plot display?

## [[06_worked_appendices/d_cake_eating|Appendix D: Cake Eating]]

1. Why must the cake-eating state include stages remaining?
2. What does concave utility imply about marginal utility?
3. How does wealth change after consumption?
4. What does the interior first-order condition balance?
5. Why consume all wealth in the final stage?
6. What is the two-stage current log-utility allocation?
7. What is the general source allocation denominator?
8. Why use calculus rather than enumerate every action?

## [[06_worked_appendices/e_q_learning_treasure_seeking|Appendix E: Q Learning Treasure Seeking]]

1. What behavior does the source agent use?
2. Does finding the treasure early reduce the scheduled rental bill?
3. What determines a successful simulated search?
4. When does an episode terminate?
5. What future value is used in a terminal update?
6. What is the source learning rate for a visited pair?
7. What does Qfactor row w-minus-one represent?
8. What does the source variable named target actually store?
9. How should policy vector [5,4,3] be read?
10. Why can the learned policy be correct with inaccurate values?
