# Flashcards - Unit 1

#flashcards/DLMAIRIL01/unit1

Source-derived cards. No imported review history; all cards start unscheduled.

## 1.1 Understanding Reinforcement Learning

Source: [[01_unit_1_introduction_to_reinforcement_learning/01_understanding_reinforcement_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=14|Course book pp. 12-31]].

What distinguishes reinforcement learning from supervised learning?::RL learns sequential decisions from interaction rewards rather than labelled correct input-output pairs.
How do feature selection and feature extraction differ?::Selection keeps informative existing inputs; extraction constructs derived inputs.
What is certainty-equivalence control?::Compute an optimal rule for the estimated model while treating that estimate as exact.
What makes a state-action pair admissible?::The action belongs to the set of actions allowed from that state.
How do deterministic and stochastic transitions differ?::A transition function specifies one successor; a kernel specifies probabilities of successors.
What are the three SDP lifetimes in the book?::Finite horizon, infinite horizon and shortest path/episodic termination.
Why discount bounded infinite-horizon costs?::A discount below one bounds the sum by a convergent geometric series.
What does a policy value function evaluate?::Expected total cost or return from a state while following a specified policy.
What does a Q-factor evaluate?::A selected first action followed by a given or optimal continuation policy.
How does Bellman optimality differ from fixed-policy evaluation?::Optimality minimizes or maximizes over admissible actions; evaluation keeps the policy fixed.
How do value iteration and policy iteration differ?::Value iteration updates values directly; policy iteration alternates policy evaluation and improvement.
What are the two explicit-model obstacles in the poker example?::Huge state/action tables and difficulty specifying accurate reward and transition models.
What does the environment output after an action?::A reward and a successor state.
Which action wins the source's state-3 cost comparison?::Action 2: its Q-factor is 56.15 versus 80.495 for action 1.

## 1.2 Components of Reinforcement Learning Systems

Source: [[01_unit_1_introduction_to_reinforcement_learning/02_components_of_reinforcement_learning_systems]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=34|Course book pp. 32-50]].

How is an episodic policy value estimated by Monte Carlo?::Run episodes with the policy and average returns associated with each state.
What is the difference between first-visit and every-visit evaluation?::First-visit uses the first occurrence per episode; every-visit uses all occurrences.
What is the general incremental update pattern?::Old estimate plus learning rate times target minus old estimate.
Why is learning rate one risky for noisy targets?::It replaces the accumulated estimate entirely with the latest noisy target.
What does bootstrapping mean?::An estimated value is used as part of the update target.
What are the components of mean squared error?::Estimator variance plus squared estimator bias.
What do TD(0) and TD(1) denote in this unit?::The book identifies the one-step bootstrap and Monte Carlo endpoints respectively.
What does the trace-decay parameter control?::The influence of later temporal differences in the update.
How does Q-learning's target differ from SARSA's?::Q-learning uses the best estimated successor action; SARSA uses the action selected by the current policy.
Why can a greedy policy get stuck?::Unchosen actions receive no new evidence, so initially wrong estimates may never be corrected.
What does epsilon-greedy combine?::Greedy action selection with probability one minus epsilon and exploration with probability epsilon.
How does hindsight replay use a failed episode?::Relabel an actually achieved outcome as the goal and learn from that successful alternative task.
What is the purpose of neural-network value approximation?::Compact representation and useful value estimates without an independent table entry or visit for every state.
What do the poker network's early hidden layers represent?::Features such as suit and rank counts derived from card-indicator inputs.
