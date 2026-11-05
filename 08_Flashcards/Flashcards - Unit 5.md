# Flashcards - Unit 5

#flashcards/DLMAIRIL01/unit5

Source-derived cards. No imported review history; all cards start unscheduled.

## 5.1 Model-Free Learning

Source: [[05_unit_5_reinforcement_learning_approaches/01_model_free_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=173|Course book pp. 171-172]].

What does a model-free method avoid building first?::An explicit environment model of transition probabilities and rewards.
What is the difference between prediction and control?::Prediction evaluates a policy; control improves action selection.
What does every visit mean in Monte Carlo evaluation?::Include the return from each occurrence of a state, including repeated visits in one episode.
What is averaged to estimate a state value?::The subsequent returns associated with visits to that state.
Why does the presented Monte Carlo procedure need termination?::It must observe a complete episode to obtain its full returns.
How can TD update earlier?::It bootstraps a continuation estimate after the next reward and state.
How does SARSA's successor target differ from Q-learning's?::SARSA uses the policy-selected next action; Q-learning uses the maximum next-state Q-value.

## 5.2 Model-Based Learning

Source: [[05_unit_5_reinforcement_learning_approaches/02_model_based_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=174|Course book pp. 172-176]].

What does an estimated model contain?::Transition probabilities and rewards representing current knowledge.
Why is planning on a learned model approximate?::Its transition and reward estimates are not fully known exact values.
What does Dyna combine?::Real interaction, model updates and repeated model-informed value improvement.
Which disagreement matters to Ready Policy One?::Disagreement between observations and model predictions in regions relevant to policy improvement.
Why can a perfect game model still be hard to use?::The number of future move sequences can make exhaustive planning intractable.
What are MCTS's four stages?::Selection, expansion, simulation and backpropagation.
What is propagated during MCTS backpropagation?::Simulation outcomes updating search-node statistics.
What does the source say AlphaGo combines?::MCTS with deep value and policy networks.
Why does MBPO use short imagined trajectories?::Long rollouts compound learned-model errors.
Where do MBPO's rollout starting states come from?::States previously encountered during real interaction.
How many environments are in the cited model-based benchmark?::Eighteen.

## 5.3 Exploration vs. Exploitation

Source: [[05_unit_5_reinforcement_learning_approaches/03_exploration_vs_exploitation]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=179|Course book pp. 177-181]].

What can greedy exploitation miss?::Better actions that current experience has not revealed.
How does Boltzmann exploration differ from uniform random exploration?::Its action probabilities depend on relative Q estimates.
What happens to finite-action Boltzmann probabilities at high temperature?::They approach a uniform distribution.
What information guides Thompson sampling?::Bayesian posterior information updated from observations.
How does bootstrapped DQN represent uncertainty?::Maintain multiple Q estimates and use a randomly selected estimate for behavior.
Why add intrinsic curiosity reward?::External rewards may be too sparse to guide exploration.
Why not reward prediction errors from rustling leaves?::Those changes are outside the agent's control and distract from useful learning.
When does an E3 state become known?::After enough observations to estimate rewards and transitions sufficiently accurately.
How does E3 act in unknown states?::Try a least-sampled action there.
What reward does R-max assign to unknown pairs?::A fixed optimistic R-max proxy until enough observations replace it.
Does Dyna alone define a behavior action policy?::No; action selection is a separate choice.
What discrepancy motivates prioritized sweeping?::The absolute TD error above a chosen threshold.
