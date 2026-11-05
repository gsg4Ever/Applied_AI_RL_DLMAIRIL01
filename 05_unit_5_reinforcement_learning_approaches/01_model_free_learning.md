---
module: DLMAIRIL01 Reinforcement Learning
unit: 5
chapter: "5.1 Model-Free Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=173|Course book pp. 171-172]]"
printed_pages: [171, 172]
pdf_pages: [173, 174]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 5.1 Model-Free Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Distinguish predicting a policy's values from controlling its actions.
- Reconstruct every-visit Monte Carlo evaluation.
- Explain why TD methods can update before an episode ends.

## 2. Detailed explanation in my own words

### Learn directly from interaction

A model-free method does not first estimate an explicit transition kernel and reward model. It learns values or behavior from experience tuples $(s,a,r,s')$.

**Prediction** estimates the value function for a specified policy. **Control** improves action selection toward a better return. Evaluating one fixed policy therefore does not by itself solve the control problem.

### Every-visit Monte Carlo policy evaluation

The source uses the expected-return interpretation of a state value. A sample mean of observed returns estimates that expectation.

1. Choose the policy $\pi$ to evaluate.
2. Initialize a state-value function and an empty return list for each state.
3. Generate a complete episode under $\pi$.
4. For every occurrence of every state in the episode, determine its subsequent discounted return.
5. Append that return to the state's list and update its value to the list's mean.
6. Generate more episodes and repeat.

If $G_j(s)$ are the recorded returns for visits to state $s$,

$$
V(s)=\frac1{N(s)}\sum_{j=1}^{N(s)}G_j(s).
$$

**Every visit** means every occurrence is included, even if a state appears repeatedly within the same episode. A state's value is the average of its future returns, not the average of only its immediate rewards.

No transition-probability calculation is needed, and the mechanism producing rewards need not be known. However, the return must be available: the presented procedure waits for a full terminating episode. Long episodes can make evaluation expensive; a nonterminating task does not provide the complete episodes required by this procedure.

### Temporal differences do not wait for a full return

TD methods also learn without a transition model, but they combine an observed reward with an estimated future value. They can update after each interaction instead of waiting to observe the whole future trajectory.

The source revisits Q-learning:

$$
Q(s,a)\leftarrow Q(s,a)+
\alpha[r+\gamma\max_bQ(s',b)-Q(s,a)].
$$

SARSA instead uses the action $a'$ selected under the current policy in the successor state. This gives the on-policy versus off-policy distinction discussed in Unit 4.

The section illustrates Q-learning with greedy behavior. The general Q-learning update does not require exclusively greedy behavior: exploration strategies are discussed in Section 5.3 and fully random behavior appears in Appendix E.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Model-free prediction | Estimate values under a given policy without an explicit model. |
| Model-free control | Improve action choice directly from experience. |
| Every-visit evaluation | Use returns from every state occurrence in each episode. |
| Return | Cumulative, possibly discounted, future reward. |
| Monte Carlo / TD | Use completed returns / use reward plus an estimated continuation. |

## 4. Important formulas / algorithms / steps

Every-visit Monte Carlo: generate a complete episode, calculate each visit's return, and average returns by state.

$$
V(s)=\frac1{N(s)}\sum_jG_j(s).
$$

TD learning can update after a single interaction, using a bootstrapped successor value.

## 5. Source-book example

The source algorithm generates a policy-controlled episode and gathers a return for every occurrence of each state. Its game-over example illustrates why termination makes the complete future return available; a very long route to game-over delays that evaluation.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does a model-free method avoid building first?
> An explicit environment model of transition probabilities and rewards.

> [!question]- 2. What is the difference between prediction and control?
> Prediction evaluates a policy; control improves action selection.

> [!question]- 3. What does every visit mean in Monte Carlo evaluation?
> Include the return from each occurrence of a state, including repeated visits in one episode.

> [!question]- 4. What is averaged to estimate a state value?
> The subsequent returns associated with visits to that state.

> [!question]- 5. Why does the presented Monte Carlo procedure need termination?
> It must observe a complete episode to obtain its full returns.

> [!question]- 6. How can TD update earlier?
> It bootstraps a continuation estimate after the next reward and state.

> [!question]- 7. How does SARSA's successor target differ from Q-learning's?
> SARSA uses the policy-selected next action; Q-learning uses the maximum next-state Q-value.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Model-free learning uses experience directly: Monte Carlo prediction averages complete episode returns, while TD learns from reward-plus-continuation estimates and can support stepwise control.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **171-172**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=173|Course book pp. 171-172]].
- Source sections: 5.1, Prediction and Control, Every-Visit Monte Carlo Evaluation, Temporal-Difference Learning.
- Printed page + 2 = PDF viewer page for this supplied edition.
