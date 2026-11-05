---
module: DLMAIRIL01 Reinforcement Learning
unit: 5
chapter: "5.2 Model-Based Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=174|Course book pp. 172-176]]"
printed_pages: [172, 176]
pdf_pages: [174, 178]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 5.2 Model-Based Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Describe learning a transition/reward model and planning with it.
- Explain real experience and repeated planning in Dyna.
- Reconstruct MCTS's four stages and MBPO's short-rollout motivation.

## 2. Detailed explanation in my own words

### Learn the world before planning through it

Model-based reinforcement learning uses observed interactions to estimate the environment, then plans behavior using that estimate.

![[99_attachments/course_book/figure_24.png]]

*Figure 24: Model-based reinforcement learning* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=175|Course book pp. 173]]. Original visual from the supplied IU course book; not redrawn.

Assuming known state and action spaces, the model $\mathcal M_\theta$ contains estimated transition probabilities $P_\theta(s'\mid s,a)$ and rewards $R_\theta$. Its parameters represent current knowledge rather than a fully known environment.

Observed tuples improve the estimates. Value or policy iteration can then optimize the **estimated** decision problem. Better information can improve planning, but the resulting policy remains dependent on model accuracy.

A simple lookup model records experienced state-action results. As with value tables, this representation becomes inefficient in very large or continuous environments.

### Dyna: combine new interaction with repeated use of learned information

The source Dyna description cycles through:

1. Choose an action in the real environment and observe reward and successor.
2. Use that experience to improve the model.
3. Repeatedly use known state-action information and the model to improve value estimates.
4. Obtain new real experience and repeat.

This combines model learning and value improvement. Reusing learned transitions for planning reduces dependence on repeatedly obtaining every useful sample from the real environment. How to choose behavior actions is a separate question addressed in Section 5.3.

### Ready Policy One: obtain informative real samples

The cited **Ready Policy One** approach treats model building as active learning. Real-world samples can be expensive; optimizing behavior within a world model can be cheaper.

The aim is to add observations where reality disagrees with model predictions **and where that disagreement matters for improving the policy**. Not every model error is equally relevant to useful action selection.

### A perfect transition model does not remove search complexity

In a game with known rules, placing a piece may determine the next board exactly. Yet the consequences of a move require considering many further choices and opponent responses.

![[99_attachments/course_book/figure_25.png]]

*Figure 25: Game Tree in Tic-Tac-Toe* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=177|Course book pp. 175]]. Original visual from the supplied IU course book; not redrawn.

The source Tic-Tac-Toe tree shows possible moves, terminal outcomes, and propagation of results back to earlier decisions. Exhaustive trees quickly become infeasible in larger games. The cited Go example estimates approximately $10^{170}$ positions.

Thus, **model accuracy** and **planning tractability** are different limitations: even exact dynamics can leave a prohibitively large tree.

### Monte Carlo Tree Search

MCTS concentrates computation on promising portions of a tree instead of expanding every possible future.

| Stage | Source procedure |
|---|---|
| Selection | Follow a tree policy from the current state to a node not yet fully explored; use metrics such as visits and estimated return. |
| Expansion | Add one or more child nodes representing additional successor states. |
| Simulation | Simulate continuations to termination or a resource/depth limit, then evaluate them. |
| Backpropagation | Propagate simulation results up the tree to update selection statistics. |

Repeat until a resource or time limit is reached. Tree backpropagation updates search statistics; it is not neural-network gradient backpropagation.

The source attributes AlphaGo's success to combining MCTS with deep networks for value and policy evaluation. It does not supply a full AlphaGo implementation.

### Model Based Policy Optimization

Errors in a learned model can compound along a long predicted trajectory. Predictions become less reliable the farther the model rolls forward.

The cited **MBPO** approach starts from states previously seen in real interaction and generates **short** future trajectories using an ensemble of models. Many small rollout snippets from different experienced states are used instead of relying on one long imagined trajectory from an initial state.

This addresses how far a learned model should be trusted. The source closes by mentioning a comparison benchmark containing **18 environments** suitable for model-based algorithms; it does not prescribe one environment for this course task.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| World model | An estimated environment used to predict rewards and transitions. |
| Approximate planning | Optimize against an estimated rather than fully known model. |
| Dyna | Combine real experience, model updates and repeated value planning. |
| Active learning | Select real samples for their useful information. |
| MCTS | Selection, expansion, simulation and backpropagation through a search tree. |
| Compounding model error | Prediction errors accumulate along imagined continuations. |
| MBPO | Use model ensembles and short rollouts from previously experienced states. |

## 4. Important formulas / algorithms / steps

Model: $\mathcal M_\theta=\{P_\theta,R_\theta\}$ with known state/action spaces.

Dyna combines real experience, model learning and planning.

MCTS: **selection -> expansion -> simulation -> backpropagation**.

MBPO: sample previously encountered states, then use an ensemble for short imagined trajectories instead of one long unreliable rollout.

## 5. Source-book example

The source Tic-Tac-Toe tree makes future moves explicit and carries terminal results back toward the first choice. Go illustrates why exact rules do not make exhaustive planning practical. MBPO addresses a different issue: inaccurate learned dynamics during long imagined sequences.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does an estimated model contain?
> Transition probabilities and rewards representing current knowledge.

> [!question]- 2. Why is planning on a learned model approximate?
> Its transition and reward estimates are not fully known exact values.

> [!question]- 3. What does Dyna combine?
> Real interaction, model updates and repeated model-informed value improvement.

> [!question]- 4. Which disagreement matters to Ready Policy One?
> Disagreement between observations and model predictions in regions relevant to policy improvement.

> [!question]- 5. Why can a perfect game model still be hard to use?
> The number of future move sequences can make exhaustive planning intractable.

> [!question]- 6. What are MCTS's four stages?
> Selection, expansion, simulation and backpropagation.

> [!question]- 7. What is propagated during MCTS backpropagation?
> Simulation outcomes updating search-node statistics.

> [!question]- 8. What does the source say AlphaGo combines?
> MCTS with deep value and policy networks.

> [!question]- 9. Why does MBPO use short imagined trajectories?
> Long rollouts compound learned-model errors.

> [!question]- 10. Where do MBPO's rollout starting states come from?
> States previously encountered during real interaction.

> [!question]- 11. How many environments are in the cited model-based benchmark?
> Eighteen.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Model-based learning estimates rewards and transitions for planning; Dyna reuses learned information, MCTS limits search, and MBPO limits imagined rollout length to reduce compounded model error.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **172-176**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=174|Course book pp. 172-176]].
- Source sections: 5.2, Learned Environment Model, Dyna, Ready Policy One, Monte Carlo Tree Search, AlphaGo, Model Based Policy Optimization, Benchmarking.
- Printed page + 2 = PDF viewer page for this supplied edition.
