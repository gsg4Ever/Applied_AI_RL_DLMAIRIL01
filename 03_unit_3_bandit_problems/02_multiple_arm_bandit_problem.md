---
module: DLMAIRIL01 Reinforcement Learning
unit: 3
chapter: "3.2 The Multiple Arm Bandit Problem"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=120|Course book pp. 118-134]]"
printed_pages: [118, 134]
pdf_pages: [120, 136]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 3.2 The Multiple Arm Bandit Problem

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain the greedy simulation's failure and forced exploration.
- Compare epsilon-greedy, softmax and gradient preference policies.
- Understand uncertainty indices, confidence intervals and UCB1.

## 2. Detailed explanation in my own words

### The three-arm simulation

The source uses three normally distributed reward sources with common standard deviation 20 and means 25, 30 and 35. If those means were known, arm 3 would always be best. Instead, collect five initial observations from each arm and then choose the arm with the largest estimated mean.

![[99_attachments/course_book/figure_12.png]]

*Figure 12: Maximum reward selection policy discussed in Sec. 3.2 for a three-armed bandit process.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=122|Course book pp. 120]]. Original visual from the supplied IU course book; not redrawn.

The five replications produce different outcomes. In one, arm 2 becomes preferred and its estimate approaches that arm's mean. The underestimated arm 3 is not sampled and its estimate stays frozen below the selected arm's estimate. Thus a policy based only on the largest current sample mean can reliably estimate the wrong selected arm while never discovering the better source.

**Source visual caution:** the text specifies the second arm's mean as 30, while the original simulation-figure legends label Treatment 2's true mean as 20. The original images are preserved, and the notes do not silently change either supplied value. The frozen-ranking lesson does not depend on resolving that mismatch.

This illustrates why a more accurate estimate for one arm is not enough: all relevant alternatives need enough observations to compare them.

### 3.2.1 Forced exploration and epsilon-greedy

A **greedy** policy chooses the arm with the best current estimate. A **forced exploration** policy ensures that other arms continue to be sampled.

An epsilon-greedy policy selects the greedy rule with probability $1-\epsilon$ and explores with probability $\epsilon$. The source gives $\epsilon=1/5$ as an illustration, either enforced every fifth stage or implemented by a randomized decision at each stage.

A constant exploration rate keeps learning, but continues selecting inferior arms even after estimates become very accurate. **Vanishing exploration** reduces $\epsilon_j$ over time while preserving enough repeated exploration to identify the best arm:

$$
\epsilon_j\to0,\qquad\sum_{j=1}^{\infty}\epsilon_j=\infty.
$$

The source example $\epsilon_j=1/j^r$ meets the infinite-sum condition when $0<r\le1$, but not when $r>1$. Exploration should diminish without disappearing so quickly that an initial ranking error remains uncorrected.

### Softmax action selection

Softmax converts reward estimates into positive selection probabilities:

$$
\pi_j(k)=
\frac{\exp(Q_{k,j-1}/\tau)}
{\sum_{\ell=1}^{K}\exp(Q_{\ell,j-1}/\tau)},\qquad \tau>0.
$$

Unlike epsilon-greedy, this does not explicitly switch between two separate policies. Every estimate influences a single selection distribution.

**Temperature** $\tau$ determines how different the probabilities are. At large temperature, exponentials become similar and selection approaches uniform exploration. At low temperature, the largest estimated mean dominates and behavior approaches greedy selection.

![[99_attachments/course_book/figure_13.png]]

*Figure 13: Softmax policy for a three-armed bandit process, for temperature parameter τ = 1.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=126|Course book pp. 124]]. Original visual from the supplied IU course book; not redrawn.

For $\tau=1$, the source's reward differences make the rule nearly greedy and the same unreliable outcomes appear.

![[99_attachments/course_book/figure_14.png]]

*Figure 14: Softmax policy for a three-armed bandit process, using temperature parameter τ = 100.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=127|Course book pp. 125]]. Original visual from the supplied IU course book; not redrawn.

For $\tau=100$, the source simulation obtains enough exploration to identify arm 3 consistently. These are outcomes of the published example, not universal temperature recommendations.

### Gradient preferences instead of absolute reward estimates

Softmax can be applied to general **preferences** $H_{k,j}$ rather than estimates with the units of the reward:

$$
\pi_j(k)=\frac{e^{H_{k,j}}}{\sum_{\ell=1}^Ke^{H_{\ell,j}}}.
$$

Equal initial preferences produce equal initial selection probabilities. Adding the same constant to all preferences leaves the normalized probabilities unchanged, because the common exponential factor cancels.

The gradient policy adjusts relative preferences based on the reward's difference from a baseline average of all observed rewards, $\bar r_j$.

For selected arm $k$:

$$
H_{k,j+1}=H_{k,j}+
\gamma(r_j-\bar r_j)(1-\pi_j(k)).
$$

For an unselected arm $\ell$, the counterpart moves in the opposite direction, in proportion to its selection probability:

$$
H_{\ell,j+1}=H_{\ell,j}-
\gamma(r_j-\bar r_j)\pi_j(\ell).
$$

Thus an above-baseline reward raises preference for the selected arm relative to alternatives. The quantity being adjusted is a preference, not necessarily the arm's mean reward. This captures the source's relative-reward motivation without treating a shifted reward scale as a different optimal-arm problem.

### 3.2.2 Index methods

An **index policy** calculates a numerical index for each arm separately and chooses the largest index. A mean estimate by itself is an index, but the earlier simulation demonstrates its weakness.

A more useful index combines

$$
\text{index}=\text{greedy component}+\text{uncertainty component}.
$$

The first favors arms with high estimated reward. The second favors arms whose true reward may be higher than the limited observations suggest. A poorly sampled arm can therefore be tried despite its currently low mean estimate.

### Confidence intervals and one-sided bounds

A confidence interval $[L,U]$ with confidence level $1-\alpha$ is constructed to contain the unknown parameter with the required sampling probability. If coverage exceeds the nominal level, it is conservative.

An **upper confidence bound** supplies a statement of the form $\theta\le U$; a **lower confidence bound** supplies $\theta\ge L$. A one-sided bound is not identical to taking one end of a two-sided interval at the same confidence level.

For a normally distributed sample with unknown variance:

$$
\operatorname{CI}_{1-\alpha}
=\bar X_n\pm t_{n-1;\alpha/2}\frac{S_n}{\sqrt n}.
$$

A one-sided upper bound is

$$
U_{1-\alpha}=\bar X_n+
t_{n-1;\alpha}\frac{S_n}{\sqrt n},
$$

and the lower bound uses subtraction. $S_n$ is the sample standard deviation, obtained from the sample variance with denominator $n-1$. Critical values depend on the degrees of freedom and whether coverage is one- or two-sided.

The source example has five observations, mean 34.6 and standard deviation 5.7. The 95% two-sided interval uses $t_{4;0.025}=2.7764$ and is approximately $[27.52,41.68]$. The 95% upper bound uses $t_{4;0.05}=2.1318$ and is approximately **40.0**.

### From uncertainty bounds to UCB1

Using an upper plausible reward value as an index balances estimated return and uncertainty. An arm's index decreases toward its estimated mean as its sample size grows.

The source first considers a normal-theory index of estimated mean plus a t-based uncertainty margin. It then presents the regret-oriented **UCB1** index:

$$
I_{k,j}=Q_{k,j-1}+
\sqrt{\frac{2\log(j-1)}{n_{k,j-1}}}.
$$

Here $n_{k,j-1}$ is that arm's observation count, while $j-1$ is the total number of observations over all arms. The numerator maintains pressure to reconsider under-sampled arms as overall experience grows. The denominator shrinks the uncertainty bonus when an arm has been observed often.

Unlike the normal-theory confidence index, this expression contains no sample variance or t-critical value. Designing confidence coverage and designing a low-regret policy are related motivations but not the same mathematical optimization problem.

![[99_attachments/course_book/figure_15.png]]

*Figure 15: UCB1 policy, discussed in Sec. 3.2.2.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=134|Course book pp. 132]]. Original visual from the supplied IU course book; not redrawn.

The source illustrates UCB1 on its bandit example. Its discussion of optimal-regret results belongs to the cited theory and its assumptions; the formula is not a blanket guarantee for every possible reward process.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Forced exploration | Explicitly preserve sampling of alternatives to the current best estimate. |
| Vanishing exploration | Reduce exploration while retaining enough repeated sampling. |
| Temperature | Softmax scaling that controls how strongly the best estimate dominates. |
| Preference | A relative score used to form an action probability. |
| Baseline reward | Average reward used for relative preference updates. |
| Index policy | Select the arm with the largest independently calculated arm index. |
| Confidence interval | A two-sided interval with specified sampling coverage. |
| Upper confidence bound | A one-sided bound on a plausible upper parameter value. |
| UCB1 | Reward estimate plus a count- and total-time-dependent uncertainty bonus. |

## 4. Important formulas / algorithms / steps

Softmax:

$$
\pi_j(k)=\frac{e^{Q_{k,j-1}/\tau}}{\sum_\ell e^{Q_{\ell,j-1}/\tau}}.
$$

Vanishing epsilon-greedy exploration requires the source condition $\sum_j\epsilon_j=\infty$.

UCB1:

$$
I_{k,j}=Q_{k,j-1}+\sqrt{\frac{2\log(j-1)}{n_{k,j-1}}}.
$$

Gradient preferences use reward minus a baseline; uncertainty indices combine estimated reward with an exploration bonus.

## 5. Source-book example

For the source normal-sample example:

$$
34.6\pm 2.7764\frac{5.7}{\sqrt5}
\approx[27.52,41.68].
$$

The corresponding 95% one-sided upper bound is

$$
34.6+2.1318\frac{5.7}{\sqrt5}\approx40.0.
$$

The two upper numbers differ because a two-sided interval splits the excluded probability between both tails, whereas a one-sided upper bound uses the single relevant tail.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why does the source's greedy three-arm policy sometimes choose arm 2 forever?
> Arm 3 is initially underestimated and then receives no new samples to correct its ranking.

> [!question]- 2. What does forced exploration prevent?
> Permanent neglect of alternatives based on inaccurate initial estimates.

> [!question]- 3. What is the cost of a constant epsilon in the long run?
> It keeps selecting inferior exploratory arms even after accurate identification.

> [!question]- 4. What condition does the book give for vanishing exploration?
> Epsilon tends to zero but its sum over stages remains infinite.

> [!question]- 5. How does softmax temperature affect selection?
> High temperature approaches uniform exploration; low temperature approaches greedy selection.

> [!question]- 6. What does a gradient bandit policy learn?
> Relative action preferences adjusted using reward minus a baseline.

> [!question]- 7. Why does adding a common preference constant leave softmax unchanged?
> The common exponential factor cancels in numerator and denominator.

> [!question]- 8. What are the two components of an uncertainty-based index?
> Current reward estimate and an uncertainty or exploration bonus.

> [!question]- 9. How does a one-sided confidence bound differ from a two-sided interval?
> It assigns coverage to one relevant tail rather than splitting it between two tails.

> [!question]- 10. What is the source's 95% confidence interval for mean 34.6 and standard deviation 5.7 with n=5?
> Approximately 27.52 to 41.68.

> [!question]- 11. What is the corresponding one-sided 95% upper bound?
> Approximately 40.0.

> [!question]- 12. What does UCB1 add to the current reward estimate?
> The square root of two log total prior pulls divided by that arm's prior pull count.

> [!question]- 13. How do the two counts in UCB1 differ?
> The numerator uses overall time; the denominator uses observations of the particular arm.

> [!question]- 14. Does UCB1's displayed bonus use a sample variance or t critical value?
> No; the source contrasts it with the normal-theory confidence index.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Effective bandit policies combine current reward estimates with continuing exploration; epsilon-greedy and softmax force exploration, gradient methods adjust relative preferences, and uncertainty indices such as UCB1 favor both promising and under-sampled arms.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **118-134**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=120|Course book pp. 118-134]].
- Source sections: 3.2, 3.2.1 Exploitation vs. Exploration Trade-off, Softmax Action Selection, Gradient Policy, 3.2.2 Index Methods, Confidence Intervals and Confidence Bounds, Index Methods Based on Upper Confidence Bounds, UCB1.
- Printed page + 2 = PDF viewer page for this supplied edition.
