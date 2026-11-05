---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.1 Q-Learning and Time-difference Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=142|Course book pp. 140-150]]"
printed_pages: [140, 150]
pdf_pages: [142, 152]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.1 Q-Learning and Time-difference Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Build Q-values from one-step and multi-step optimal continuations.
- Replace a known transition model with observed experiences.
- Explain the Q-learning and SARSA updates and their policy distinction.

## 2. Detailed explanation in my own words

### From the final action to a multi-step Q-function

This unit uses the **maximum-reward** convention. With one step left,

$$
Q_1(s,a)=r(s,a),\qquad
V_1(s)=\max_aQ_1(s,a),\qquad
\pi_1(s)\in\arg\max_aQ_1(s,a).
$$

The value is a numerical return; the policy is an action. With two steps left, the first reward must be combined with the best discounted return after the stochastic transition:

$$
Q_2(s,a)=r(s,a)+\gamma\sum_{s'}P(s'\mid s,a)V_1(s').
$$

Repeating the argument gives

$$
Q_{k+1}(s,a)=r(s,a)+\gamma\sum_{s'}P(s'\mid s,a)
\max_bQ_k(s',b).
$$

State-value iteration instead updates

$$
V_{k+1}(s)=\max_a\left[r(s,a)+
\gamma\sum_{s'}P(s'\mid s,a)V_k(s')\right].
$$

Under the relevant convergence conditions, the limiting values satisfy Bellman's optimality equation. An explicit model permits either state-value or action-value iteration: initialize estimates, repeatedly apply the recursion, and stop when changes are sufficiently small.

### What changes when transition probabilities are unknown?

The agent can no longer calculate an exact probability-weighted sum over possible successors. It can still act and observe $(s,a,r,s')$. Repeated experiences from the same state-action pair supply sampled rewards and successors.

The book first presents a sample average of targets:

$$
\frac1n\sum_{i=1}^n
\left[r_i+\gamma\max_bQ(s'_i,b)\right].
$$

The same incremental-mean identity introduced earlier updates this average without repeatedly summing all old observations. It motivates a learning rule using one stored Q-function and one new experience at a time.

### Q-learning

$$
Q(s,a)\leftarrow Q(s,a)+
\alpha\left[r+\gamma\max_bQ(s',b)-Q(s,a)\right].
$$

The target is the immediate sampled reward plus the discounted best estimated continuation. The learning rate $\alpha$ controls how much the current experience changes the accumulated estimate. The bracketed term is the **temporal-difference error**.

The source algorithm is:

1. Initialize Q-values.
2. Begin at an initial state.
3. Choose an admissible action.
4. Execute it and observe reward and successor state.
5. Update the experienced state-action entry.
6. Continue from the successor until a terminal state, then start another episode.

The next-state maximum belongs to the **target**; it is not a requirement that all behavior actions be greedy. Exploration is needed to discover actions that an initially inaccurate table would otherwise ignore.

A terminal state ends the current episode, such as game-over. Its future continuation is zero. This distinction becomes explicit in the treasure-search implementation in Appendix E.

### Temporal differences

Define

$$
\Delta=r+\gamma\max_bQ(s',b)-Q(s,a).
$$

Then the update is $Q\leftarrow Q+\alpha\Delta$. Instead of replacing an entire learned table after each interaction, learning makes incremental corrections where observations were obtained. Multi-step TD ideas connect to the TD(lambda) discussion in Unit 1.

### SARSA

SARSA uses the **actual successor action** chosen by the current policy instead of the maximum over successor actions:

$$
Q(s,a)\leftarrow Q(s,a)+
\alpha\left[r+\gamma Q(s',a')-Q(s,a)\right].
$$

Observe state $s$, take $a$, receive $r$, reach $s'$, and select $a'$ using the same policy. After updating, continue with that selected action.

This makes SARSA **on-policy**. Q-learning is **off-policy** because its target is based on a maximizing continuation rather than necessarily the next action selected by the behavior policy.

The comparison concerns the complete discounted continuation, not simply which method selects a large immediate reward. Both learn action values from interactions; their targets answer different continuation questions.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| State-value function | Expected return from a state under a policy. |
| Action-value function | Expected return after a specified initial action and continuation. |
| TD target | Observed reward plus a bootstrapped continuation estimate. |
| TD error | The target minus the current estimate. |
| Learning rate alpha | Step size applied to the observed discrepancy. |
| Discount gamma | Weight assigned to later returns in this unit. |
| Terminal state | A state ending the current episode. |
| On-policy / off-policy | Target uses the current policy's chosen successor action / a different target continuation. |

## 4. Important formulas / algorithms / steps

$$
Q(s,a)\leftarrow Q(s,a)+\alpha
[r+\gamma\max_bQ(s',b)-Q(s,a)].
$$

SARSA replaces $\max_bQ(s',b)$ with $Q(s',a')$. Here $\alpha$ is learning rate and $\gamma$ is discount, unlike the early-unit symbol choices.

## 5. Source-book example

In the source cat-and-mouse game, the mouse observes the board, chooses a movement, receives feedback and observes the new board. If the cat's transitions are unknown, the mouse records these experiences and updates the value of the movement it tried rather than calculating from an unavailable full transition model.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What is Q1 for the last remaining action?
> The expected immediate reward r(s,a).

> [!question]- 2. How do a Q-value, state value and policy differ?
> Q values a particular first action; V gives a state's value; the policy chooses an action.

> [!question]- 3. What replaces unknown transition probabilities in Q-learning?
> Sampled rewards and successor states from interactions.

> [!question]- 4. What is Q-learning's target?
> Observed reward plus discounted maximum estimated next-state Q-value.

> [!question]- 5. What is the TD error?
> The update target minus the current Q estimate.

> [!question]- 6. What does the learning rate control?
> The size of the estimate change caused by one experience.

> [!question]- 7. What makes SARSA on-policy?
> Its next action is selected by the same policy used to generate the experience.

> [!question]- 8. Why is Q-learning off-policy?
> Its target uses a maximizing next-state value rather than necessarily the action the behavior policy chooses.

> [!question]- 9. What is an episode?
> An interaction sequence from an initial state to termination.

> [!question]- 10. What continuation is used after termination?
> Zero future return, as in the source's treasure-search implementation.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Q-learning replaces model-based expectations with sampled TD targets; SARSA changes the target to the next action selected by the current policy, producing the on-policy versus off-policy distinction.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **140-150**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=142|Course book pp. 140-150]].
- Source sections: 4.1, Q-Factors, State Value Iteration, Action Value Iteration, Handling Unknown Transition Probabilities, Q-Learning, Time-Difference Learning and SARSA.
- Printed page + 2 = PDF viewer page for this supplied edition.
