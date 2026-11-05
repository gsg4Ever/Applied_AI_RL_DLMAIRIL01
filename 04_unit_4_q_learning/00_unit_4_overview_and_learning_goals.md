---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
note_type: unit_overview
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
tags: [review, DLMAIRIL01]
---

# Unit 4: Q-Learning

## Learning goals from the course book

- Define the Q-function.
- Explain the use of neural networks in reinforcement learning.
- Explain improvements to neural-network Q-learning.
- Describe policy-gradient methods.
- Combine value-based and policy-based learning in actor-critic approaches.

## Introduction and connections

The opening cat-and-mouse game gives the agent eight possible movement directions. The mouse aims to reach cheese while avoiding the cat; the board, obstacles, cat and cheese form the observed environment. If the cat's behavior is unknown, the mouse learns by repeatedly playing rather than planning from a fully known transition model.

![[99_attachments/course_book/figure_16.png]]

*Figure 16: Cat and Mouse Game* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=138|Course book pp. 136]]. Original visual from the supplied IU course book; not redrawn.

The interaction cycle is: observe state, select an admissible action, observe reward and successor state, then repeat. In Unit 4, the book switches to $s,a,\pi,\gamma,\alpha$: state, action, policy, discount factor and learning rate.

![[99_attachments/course_book/figure_17.png]]

*Figure 17: Elements of the reinforcement environment* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=139|Course book pp. 137]]. Original visual from the supplied IU course book; not redrawn.

For stochastic transitions, the expected immediate reward is

$$
r(s,a)=\sum_{s'}r(s,a,s')P(s'\mid s,a).
$$

Return accumulates rewards over a trajectory; $V^\pi(s)$ is its expectation under policy $\pi$. The unit addresses both unknown transition probabilities and the impractical size of explicit state-action tables.

## Official sections

- [[04_unit_4_q_learning/01_q_learning_and_time_difference_learning|4.1 Q-Learning and Time-difference Learning]]
- [[04_unit_4_q_learning/02_reinforcement_learning_with_neural_networks_and_deep_q_learning|4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning]]
- [[04_unit_4_q_learning/03_experience_replay|4.3 Experience Replay]]
- [[04_unit_4_q_learning/04_double_q_learning|4.4 Double Q-Learning]]
- [[04_unit_4_q_learning/05_delayed_sparse_rewards_and_hierarchical_learning|4.5 Delayed Sparse Rewards and Hierarchical Learning]]
- [[04_unit_4_q_learning/06_value_vs_policy_based_learning|4.6 Value- vs. Policy-Based Learning]]
- [[04_unit_4_q_learning/07_actor_critic_learning|4.7 Actor Critic Learning]]

## Learning features

- [[08_Flashcards/Flashcards - Unit 4|Source-derived flashcards]]
- [[08_CheatSheets/Cheatsheet - Unit 4|Compact review sheet]]
- [[07_exam_preparation/04_active_recall_seed_questions|Active recall by section]]
- [[07_exam_preparation/01_deep_learning_workflow|Personal review tracker]]

## Source

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=137|Course book pp. 135-168]]. Goals and introduction are paraphrased; the unit notes cover the full range shown.
