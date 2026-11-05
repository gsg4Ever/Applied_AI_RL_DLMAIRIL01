---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.4 Double Q-Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=157|Course book pp. 155-156]]"
printed_pages: [155, 156]
pdf_pages: [157, 158]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.4 Double Q-Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Separate target stabilization from action-selection/evaluation bias.
- Describe online and target-network roles.
- Reconstruct the Double DQN training target.

## 2. Detailed explanation in my own words

### Stabilizing a moving training target

A basic DQN uses its own changing predictions to compute future-value targets. Prediction and target changes can form an unstable feedback loop.

The source introduces two versions of the network. The **online network** changes with training and guides interaction. The **target network** is a copy whose weights are refreshed only periodically, making its target predictions less sensitive to every recent update.

The cited original DQN setup copied weights every 10,000 interactions. This is the example's reported interval, not a universal setting. Copying at every iteration recovers the rapidly changing-target case.

### Why a separate target network is not the whole Double Q idea

The maximum operator chooses the largest **estimate**. If estimates fluctuate, it can favor a high estimation error even when true action values are equal. Using the same estimator both to choose the action and evaluate its value therefore introduces an overestimation tendency.

**Double Q-learning** addresses this selection/evaluation coupling. A target copy stabilizes predictions; separating the choosing estimator from the evaluating estimator addresses maximization bias. These are related but distinct purposes.

### Double DQN target

The online network selects the best estimated next action:

$$
a^*=\operatorname*{argmax}_aQ(s',a;\theta).
$$

The target network evaluates that selected action:

$$
y^{\rm DoubleDQN}=r+\gamma Q(s',a^*;\theta^-).
$$

$\theta$ denotes online parameters and $\theta^-$ target parameters. In the source's ordinary target-network DQN, the target network both selects and evaluates the maximizing action. Double DQN instead uses the online network for selection while retaining the target network for evaluation.

This changes the target calculation without requiring a third network in the presented implementation.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Online network | The trained network used for current action-value estimates. |
| Target network | A periodically refreshed copy used to calculate training targets. |
| Moving-target feedback | Predictions and the targets built from them change together. |
| Maximization bias | Selecting a largest noisy estimate can favor estimation error. |
| Double DQN | Online action selection combined with target-network evaluation. |

## 4. Important formulas / algorithms / steps

$$
y^{\rm DoubleDQN}=
r+\gamma Q\left(s',\operatorname*{argmax}_aQ(s',a;\theta);\theta^-\right).
$$

Online network **selects**; target network **evaluates**. Periodic target copying improves stability; decoupled selection/evaluation addresses maximization bias.

## 5. Source-book example

The source considers actions whose true Q-values may be equal but whose estimates fluctuate. Choosing the largest estimate and treating it as its own evaluation can select an upward error. Double DQN uses one network to choose and the other to evaluate the selected action.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why use a target-network copy?
> To make the bootstrapped training target change less rapidly.

> [!question]- 2. What target refresh interval does the cited original DQN example report?
> Ten thousand interactions.

> [!question]- 3. What causes maximization bias?
> The same noisy estimates both select the largest action value and evaluate it.

> [!question]- 4. Which network selects the next action in Double DQN?
> The online network.

> [!question]- 5. Which network evaluates that selected action?
> The target network.

> [!question]- 6. Are target stabilization and Double Q selection/evaluation separation identical?
> No; they address moving-target instability and maximization bias respectively.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Double DQN separates action selection by the online network from evaluation by the target network, while periodic target copying independently reduces rapid feedback in bootstrapped targets.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **155-156**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=157|Course book pp. 155-156]].
- Source sections: 4.4, Online and Target Networks, Maximization Bias, Double DQN Target.
- Printed page + 2 = PDF viewer page for this supplied edition.
