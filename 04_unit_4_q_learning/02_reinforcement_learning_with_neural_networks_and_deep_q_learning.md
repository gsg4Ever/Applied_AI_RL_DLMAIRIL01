---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=152|Course book pp. 150-153]]"
printed_pages: [150, 153]
pdf_pages: [152, 155]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.2 Reinforcement Learning with Neural Networks and Deep Q-Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain why tabular Q-learning does not scale to complex environments.
- Describe a neural-network Q approximation and its inputs/outputs.
- Define the source's DQN target and squared-error loss.

## 2. Detailed explanation in my own words

### Why replace the Q-table?

Explicitly storing $Q(s,a)$ requires an entry for each relevant state-action pair. Large visual environments and finely varying controls can make that representation infeasible. Many entries may never receive useful experience because individual state-action combinations are rarely revisited.

![[99_attachments/course_book/figure_18.png]]

*Figure 18: Videogame on a gaming console* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=152|Course book pp. 150]]. Original visual from the supplied IU course book; not redrawn.

The source uses video-game and vehicle-control examples to illustrate this growth. Replace the independent entries by a parameterized approximation:

$$
Q(s,a;\theta)\approx Q(s,a).
$$

The parameters $\theta$ compactly represent relationships between inputs and values. Traditional approximations can use linear models with hand-crafted features, such as cat-mouse distance or obstacles. A neural network can learn features from the input representation.

### Deep networks and the Atari example

The cited Atari work takes raw image pixels as input, processes them through convolutional layers, and produces action-value estimates.

![[99_attachments/course_book/figure_19.png]]

*Figure 19: Atari video game: Space Invaders* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=153|Course book pp. 151]]. Original visual from the supplied IU course book; not redrawn.

The book presents this as an important demonstration of learned feature processing and Q-value approximation. It does not require a manually designed value-table entry for every possible image.

### Two input/output architectures

![[99_attachments/course_book/figure_20.png]]

*Figure 20: Schematic setup of Deep Q-Networks: The network learns the mapping of state-action pairs s, a to a Q-value (left) or computes a Q-value for all possible actions (right).* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=154|Course book pp. 152]]. Original visual from the supplied IU course book; not redrawn.

The upper architecture receives a state **and** an action and returns one Q estimate. The lower receives a state and returns one estimate for each possible action, allowing comparison from one state input. The source caption calls these left/right, although the supplied drawing arranges them vertically.

The lower design is especially useful when the represented actions form an enumerable output set. The book motivates approximation with very large or continuous control spaces, but this particular drawing still shows separate action outputs; it is not a supplied algorithm for maximizing over arbitrary continuous actions.

### Training target and loss

Use the Q-learning continuation to define the target:

$$
y=r+\gamma\max_bQ(s',b;\theta).
$$

Compare it with the network's current prediction for the experienced pair:

$$
L=(y-Q(s,a;\theta))^2.
$$

Training minimizes squared discrepancies, using gradient descent to change the network parameters. The task resembles supervised regression, but its target depends on estimated future values rather than a fixed independent label.

This dependence makes a naive network unstable. New training in one region can change predictions and future targets elsewhere, potentially damaging earlier learning. Experience replay and separate target estimates are introduced in the following sections to address these issues.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Q approximation | A function with parameters representing action values. |
| Features | Input information used by the approximate value model. |
| DQN | A deep neural network approximating the Q-function. |
| Network parameters | Weights and other learned quantities denoted theta. |
| Training target | Sampled reward plus discounted estimated successor value. |
| Squared-error loss | Squared difference between target and prediction. |

## 4. Important formulas / algorithms / steps

$$
Q(s,a;\theta)\approx Q(s,a),\qquad
y=r+\gamma\max_bQ(s',b;\theta),\qquad
L=(y-Q(s,a;\theta))^2.
$$

Compare a state-action input with one Q output against a state input with multiple action-Q outputs. Network approximation replaces storage of independent table entries.

## 5. Source-book example

The source Atari setup uses pixel images as states and convolutional layers to learn image features before outputting values for the available game actions. Its architecture figure contrasts one state-action-to-value mapping with a state-to-all-action-values mapping.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why does a tabular Q representation become impractical?
> The number of possible state-action pairs and sparsity of repeat visits become too large.

> [!question]- 2. What does theta represent in Q(s,a;theta)?
> The learned parameters of the approximate value function.

> [!question]- 3. How does the Atari DQN obtain features?
> Convolutional layers learn them from input images.

> [!question]- 4. What are the two network architectures in Figure 20?
> State plus action to one Q-value, or state to Q-values for all represented actions.

> [!question]- 5. What is the source's DQN target?
> Reward plus discounted maximum next-state Q estimate.

> [!question]- 6. Why is the DQN target different from a fixed supervised label?
> It depends on the network's evolving estimates of future values.

> [!question]- 7. Why can naive neural-network Q-learning become unstable?
> Changes in predictions also change training targets and can disturb earlier learning.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** A DQN approximates Q-values with learned parameters and features, avoiding independent storage of every state-action value; its bootstrapped, evolving target creates stability problems addressed by later methods.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **150-153**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=152|Course book pp. 150-153]].
- Source sections: 4.2, Function Approximation, Deep Q-Network Architectures, Training Target and Loss.
- Printed page + 2 = PDF viewer page for this supplied edition.
