---
module: DLMAIRIL01 Reinforcement Learning
unit: 3
chapter: "3.1 The One-Armed Bandit Problem"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=113|Course book pp. 111-118]]"
printed_pages: [111, 118]
pdf_pages: [113, 120]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 3.1 The One-Armed Bandit Problem

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain an unknown random reward versus a known fixed alternative.
- Maintain reward estimates and action counts incrementally.
- Define total reward and regret and explain the failure of fixed initial sampling.

## 2. Detailed explanation in my own words

### One uncertain source of reward

A one-armed bandit is a conceptual reward source: pulling its arm produces a random reward with mean $\mu$. If its mean is unknown, samples $r_1,\ldots,r_n$ can estimate it:

$$
\hat\mu=\frac1n\sum_{i=1}^n r_i.
$$

The problem becomes a sequential decision problem when each stage offers a choice between that uncertain source and another reward source. The book first uses a known fixed reward $\delta$ as the alternative.

If $\mu$ were known, choose the bandit whenever $\mu>\delta$ and otherwise choose the fixed reward, with either action optimal at equality. The unknown-mean case is difficult because sampling the bandit both earns reward and supplies information needed to make later decisions.

The source usually assumes independent identically distributed rewards with a fixed mean. It also notes that changing reward distributions require adaptive decision rules.

### Accumulated reward and horizon

Let $\rho_j$ weight the reward at stage $j$:

$$
R^\Phi=\sum_{j=1}^{\infty}\rho_j\mathbb E[r_j].
$$

For a fixed finite horizon of $M$ stages, use $\rho_j=1$ through stage $M$ and zero later. For an infinite discounted horizon, use $\rho_j=\beta^{j-1}$ with discount below one and bounded expected rewards. The geometric-series argument then bounds total expected reward.

An indicator records whether a bandit or fixed action is chosen at a stage. The action sequence therefore determines how often unknown mean $\mu$ versus known reward $\delta$ contributes to the objective.

### 3.1.1 Incremental reward estimates

An old sample mean and a new observation suffice to update the mean:

$$
Q\leftarrow Q+\gamma(r-Q).
$$

With $\gamma=1/n$ on the $n$th observation of that reward source, the estimate is the ordinary running sample mean. More general step-size choices are possible; the learning rate controls adaptation and fluctuation.

Crucially, the observation count belongs to the selected arm. A source not pulled at a stage receives no new reward observation and cannot update its mean from another source's reward.

### 3.1.2 Policy, information and action frequencies

The bandit policy chooses the next source using previous action-reward pairs. The history can be summarized by each arm's pull count and reward estimate:

$$
n_{k,j}=\sum_{i=1}^{j}I(a_i=k),\qquad
Q_{k,j}=\frac1{n_{k,j}}\sum_{i=1}^{j}r_iI(a_i=k).
$$

When a count is zero, the displayed average is not yet available; an initialization/sampling rule is needed before using it. The book's multiple-arm simulation supplies initial samples for precisely this purpose.

The general policy can depend on the entire history, but the algorithms in this unit use these count/estimate summaries. The goal is not only to identify a good arm eventually: it is to maximize the accumulated reward while learning.

### Regret expresses the price of imperfect decisions

For several sources, let $\mu^*=\max_k\mu_k$. An oracle that always selects a best-mean source earns

$$
R^*=\sum_j\rho_j\mu^*.
$$

**Regret** compares this ideal with the policy's expected accumulated reward:

$$
\Delta^\Phi=R^*-R^\Phi\ge0.
$$

Maximizing expected reward and minimizing regret are equivalent under the same horizon and weights. Sampling a genuinely inferior source sacrifices reward, but not sampling uncertain alternatives may prevent discovering the best source.

### Why two apparently reasonable solutions fail

**Naive solution 1:** sample the bandit for a fixed initial number of stages $N$, estimate its mean, and permanently choose whichever source appears better.

The initial sampling can be costly if the bandit is inferior. More importantly, a wrong ranking after only $N$ samples determines all later actions. A permanently chosen fixed alternative supplies no evidence to correct an underestimated bandit.

**Naive solution 2:** after the initial sample, keep updating the bandit's estimate whenever the policy still chooses it. If its initial estimate was too high, later bandit rewards may correct that error and cause a switch.

This only fixes one side of the problem. If the initial estimate was too low and the policy chooses the fixed source forever, it still collects no further bandit samples. Thus, a useful learning policy must deliberately maintain opportunities to revisit uncertain alternatives.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Bandit arm | A reward source producing a random outcome when selected. |
| Reward mean | Expected reward from one source. |
| Fixed reward alternative | A source with a known constant payoff. |
| Action frequency | Number of observations obtained from a particular arm. |
| Bandit policy | Rule selecting an arm from available history or its summaries. |
| Regret | Best achievable expected reward minus the policy's expected reward. |
| Frozen ranking | A choice based on estimates that receive no further corrective samples. |

## 4. Important formulas / algorithms / steps

$$
Q\leftarrow Q+\gamma(r-Q),\qquad
\Delta^\Phi=R^*-R^\Phi.
$$

Known-mean one-bandit choice: use the bandit if $\mu>\delta$; otherwise use the fixed alternative.

A selected arm updates its count and mean; unselected arms do not gain observations. A fixed initial sample followed by permanent commitment can preserve a wrong ranking indefinitely.

## 5. Source-book example

In the source's one-bandit-versus-fixed-reward example, permanently accepting the fixed reward after an underestimated initial bandit sample prevents any correction. Continuing to update only the selected source solves overestimation of the bandit, but not underestimation that stops its sampling.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What is a one-armed bandit in this book?
> A source that produces a random reward with an unknown mean when selected.

> [!question]- 2. If the bandit mean is known, when should it beat the fixed alternative?
> When its mean reward exceeds the fixed reward.

> [!question]- 3. What does a stage discount sequence define?
> How successive rewards are weighted in the accumulated objective.

> [!question]- 4. What is the incremental reward-estimate update?
> Q becomes Q plus learning rate times observed reward minus Q.

> [!question]- 5. Which count determines a running mean's step size?
> The number of observations from that particular reward source.

> [!question]- 6. What is regret?
> The best achievable expected total reward minus the policy's expected total reward.

> [!question]- 7. Why can fixed initial sampling followed by permanent commitment fail?
> A finite-sample ranking error can persist because the rejected source is never sampled again.

> [!question]- 8. What remains wrong with updating only the chosen bandit?
> An initially underestimated bandit that is no longer chosen still receives no corrective data.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Bandit decisions must earn reward and gather information simultaneously; regret measures the reward sacrificed relative to the best-known-mean choice, and insufficient continued sampling can lock a policy into an inferior source.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **111-118**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=113|Course book pp. 111-118]].
- Source sections: 3.1, 3.1.1 Iterative Update Rules for Reward Estimates, 3.1.2 Policies for Bandit Problems, Naive Solution 1, Naive Solution 2.
- Printed page + 2 = PDF viewer page for this supplied edition.
