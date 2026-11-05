# Flashcards - Unit 4

#flashcards/DLMAIRIL01/unit4

Source-derived cards. No imported review history; all cards start unscheduled.

## 4.1 Q-Learning and Time-difference Learning

Source: [[04_unit_4_q_learning/01_q_learning_and_time_difference_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=142|Course book pp. 140-150]].

What is Q1 for the last remaining action?::The expected immediate reward r(s,a).
How do a Q-value, state value and policy differ?::Q values a particular first action; V gives a state's value; the policy chooses an action.
What replaces unknown transition probabilities in Q-learning?::Sampled rewards and successor states from interactions.
What is Q-learning's target?::Observed reward plus discounted maximum estimated next-state Q-value.
What is the TD error?::The update target minus the current Q estimate.
What does the learning rate control?::The size of the estimate change caused by one experience.
What makes SARSA on-policy?::Its next action is selected by the same policy used to generate the experience.
Why is Q-learning off-policy?::Its target uses a maximizing next-state value rather than necessarily the action the behavior policy chooses.
What is an episode?::An interaction sequence from an initial state to termination.
What continuation is used after termination?::Zero future return, as in the source's treasure-search implementation.

## 4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning

Source: [[04_unit_4_q_learning/02_reinforcement_learning_with_neural_networks_and_deep_q_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=152|Course book pp. 150-153]].

Why does a tabular Q representation become impractical?::The number of possible state-action pairs and sparsity of repeat visits become too large.
What does theta represent in Q(s,a;theta)?::The learned parameters of the approximate value function.
How does the Atari DQN obtain features?::Convolutional layers learn them from input images.
What are the two network architectures in Figure 20?::State plus action to one Q-value, or state to Q-values for all represented actions.
What is the source's DQN target?::Reward plus discounted maximum next-state Q estimate.
Why is the DQN target different from a fixed supervised label?::It depends on the network's evolving estimates of future values.
Why can naive neural-network Q-learning become unstable?::Changes in predictions also change training targets and can disturb earlier learning.

## 4.3 Experience Replay

Source: [[04_unit_4_q_learning/03_experience_replay]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=155|Course book pp. 153-154]].

What does an experience tuple contain?::A state, an action, the reward and the successor state.
Why store a replay buffer?::To reuse interaction data and train on more than the latest experience.
Why randomly sample from replay?::To reduce correlation among consecutive training experiences.
What does uniform replay ignore?::Differences in rarity, informativeness and remaining learning value.
What motivates prioritized replay in the book?::Experiences with large remaining prediction discrepancies offer more learning progress.
What does the priority exponent control?::The strength of the prioritization in the sampling probabilities.

## 4.4 Double Q-Learning

Source: [[04_unit_4_q_learning/04_double_q_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=157|Course book pp. 155-156]].

Why use a target-network copy?::To make the bootstrapped training target change less rapidly.
What target refresh interval does the cited original DQN example report?::Ten thousand interactions.
What causes maximization bias?::The same noisy estimates both select the largest action value and evaluate it.
Which network selects the next action in Double DQN?::The online network.
Which network evaluates that selected action?::The target network.
Are target stabilization and Double Q selection/evaluation separation identical?::No; they address moving-target instability and maximization bias respectively.

## 4.5 Delayed Sparse Rewards and Hierarchical Learning

Source: [[04_unit_4_q_learning/05_delayed_sparse_rewards_and_hierarchical_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=158|Course book pp. 156-158]].

Why is the blind cliff walk hard to learn?::A long correct action sequence is required before reward, and a wrong decision restarts the episode.
What does Vg(s) represent?::The value of state s while pursuing goal g.
What do demons do in the Horde architecture?::Learn separate goal-oriented questions about the environment.
How does a universal value function differ?::One parameterized function accepts both a state and a goal.
What does the meta-controller choose?::The next goal to pursue.
What does the lower-level controller choose?::Actions that achieve the selected goal.
Why is independent knowledge of goals not always sufficient?::Goals can depend on one another and require a particular order.

## 4.6 Value- vs. Policy-Based Learning

Source: [[04_unit_4_q_learning/06_value_vs_policy_based_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=160|Course book pp. 158-162]].

How does value-based learning obtain a policy?::Choose actions with the highest learned Q-values.
What does policy-based learning optimize directly?::Parameters of the action-selection policy.
How do deterministic and stochastic policies differ?::One chooses a fixed action for a state; the other assigns action probabilities.
What does the policy objective J represent?::Expected cumulative discounted reward under the policy.
Why does the parameter update use gradient ascent?::The objective is to maximize expected return.
What weights the source policy-gradient expression?::The action's value under the current policy.
What does REINFORCE substitute for that action value?::The observed future discounted return from the trajectory.
Why is the presented policy-gradient approach on-policy?::Its samples come from the policy currently being evaluated and improved.

## 4.7 Actor Critic Learning

Source: [[04_unit_4_q_learning/07_actor_critic_learning]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=164|Course book pp. 162-168]].

What do actor and critic learn?::The actor learns the policy; the critic learns values used to guide that policy.
Why can learned actor-critic updates fail to improve a policy?::The critic is estimated from experience rather than evaluated from a fully known model.
Why does the basic critic update have no next-action maximum?::The successor action is chosen by the current policy, as in SARSA.
Are the actor and critic learning rates necessarily identical?::No; the source uses separate rates.
What is the advantage function?::Action value minus state value.
What provides the source's sampled advantage estimate?::Reward plus discounted next-state value minus current-state value.
How do A2C and A3C differ?::A2C is synchronous and A3C asynchronous.
What does Soft Actor Critic add to reward optimization?::An entropy-related objective encouraging exploration.
How does the book describe PPO stabilization?::Use a surrogate objective with clipping or a divergence-based penalty to avoid overly large policy changes.
