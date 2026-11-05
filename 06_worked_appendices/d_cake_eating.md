---
module: DLMAIRIL01 Reinforcement Learning
unit: appendices
chapter: "Appendix D: Cake Eating"
note_type: worked_appendix
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=215|Course book pp. 213-217]]"
printed_pages: [213, 217]
pdf_pages: [215, 219]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# Appendix D: Cake Eating

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Formulate sequential consumption with wealth and stages remaining.
- Apply Bellman's equation with a continuous action.
- Reconstruct the logarithmic-utility allocations from the source.

## 2. Detailed explanation in my own words

### A finite stock and diminishing marginal utility

The source calls a fixed stock of wealth $W$ a **cake**. A single decision maker consumes portions over a finite number of stages and receives utility from each portion. Utility is increasing, differentiable and concave: another unit of consumption has less marginal benefit when much has already been consumed.

The objective is

$$
R=\sum_{j=1}^K\beta^{j-1}u(x_j),
$$

where $x_j$ is chronological stage-$j$ consumption. The source contrasts the concave case with convex utility, which favors concentration rather than spreading the cake.

### Remaining-stage state

Let $w_k$ be available wealth with $k$ stages remaining, and choose consumption $c_k$ satisfying $0\le c_k\le w_k$. The next wealth is

$$
w_{k-1}=w_k-c_k.
$$

The state is $(w,k)$: wealth alone is insufficient because the optimal allocation also depends on how long that wealth must last. Initial wealth is $w_K=W$.

Both wealth and consumption can vary continuously. This differs from enumerating the six treasure-search actions.

### Bellman's equation

$$
V(w,k)=\max_{0\le c\le w}
[u(c)+\beta V(w-c,k-1)].
$$

Current utility is added to discounted optimal utility from the unconsumed remainder. With no stages left, no further utility is collected.

For an interior optimum, differentiate with respect to $c$:

$$
u'(c)=\beta V_w'(w-c,k-1).
$$

This balances the marginal utility of consumption now with the discounted marginal continuation value of retaining wealth.

### Last stage

With one stage remaining, increasing utility makes consuming all remaining wealth optimal:

$$
c_1=w_1,\qquad V(w_1,1)=u(w_1).
$$

This is a boundary solution; it is not found by setting an interior derivative to zero.

### Logarithmic utility

The source chooses $u(w)=\log w$, so $u'(w)=1/w$ for positive consumption.

With two stages remaining,

$$
\frac1{c_2}=\frac{\beta}{w_2-c_2},
\qquad
c_2=\frac{w_2}{1+\beta},\qquad c_1=\beta c_2.
$$

With three stages remaining,

$$
c_3=\frac{w_3}{1+\beta+\beta^2}.
$$

The continuation's wealth derivative, rather than its irrelevant additive constant, is what is needed for the next recursion.

### General allocation

The pattern gives

$$
c_k=\frac{w_k}{1+\beta+\beta^2+\cdots+\beta^{k-1}}.
$$

Read $k$ as **stages remaining**. Chronological first consumption is $c_K$, then $c_{K-1}$ from the updated wealth, continuing to $c_1$. An increasing remaining-day index in the derivation is not forward chronological time.

**Source caution:** intermediate constants and one stage label in the printed expansion have typographical inconsistencies. The notes retain the final source allocation rule and derivative argument, without copying an unnecessary erroneous constant.

### The extension mentioned by the source

An additional return $t_k$ can modify the wealth recursion:

$$
w_{k-1}=w_k-c_k+t_k.
$$

The source mentions that this can support more sophisticated, potentially infinite-horizon investment models. Those models are not developed further in this summary because the supplied appendix does not give their full derivations.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Cake | The fixed wealth available for sequential consumption. |
| Concave utility | Increasing consumption has diminishing marginal benefit. |
| Remaining-stage state | Wealth together with the number of usable stages. |
| Marginal utility | Derivative of utility with respect to consumption. |
| Interior optimum | A candidate allocation strictly inside its admissible interval. |
| Continuous action | Consumption can be any admissible real amount. |

## 4. Important formulas / algorithms / steps

$$
V(w,k)=\max_{0\le c\le w}[u(c)+\beta V(w-c,k-1)].
$$

$$
u'(c)=\beta V_w'(w-c,k-1),\qquad
c_k=\frac{w_k}{\sum_{i=0}^{k-1}\beta^i}
$$

for the source's logarithmic utility. With one stage left, consume all remaining wealth.

## 5. Source-book example

For the source's two-stage log-utility case, choose w2/(1+beta) now, retaining beta times that amount for the last stage. The three-stage denominator becomes 1+beta+beta squared; both follow the same backward marginal-utility balance.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why must the cake-eating state include stages remaining?
> The same wealth must be allocated differently depending on the remaining consumption opportunities.

> [!question]- 2. What does concave utility imply about marginal utility?
> It decreases as consumption increases.

> [!question]- 3. How does wealth change after consumption?
> The next wealth equals current wealth minus the consumed amount.

> [!question]- 4. What does the interior first-order condition balance?
> Current marginal utility against discounted marginal continuation value.

> [!question]- 5. Why consume all wealth in the final stage?
> Utility is increasing and there is no later opportunity to use retained wealth.

> [!question]- 6. What is the two-stage current log-utility allocation?
> Available wealth divided by one plus beta.

> [!question]- 7. What is the general source allocation denominator?
> One plus beta plus successive powers through beta to the k-minus-one power.

> [!question]- 8. Why use calculus rather than enumerate every action?
> Consumption is continuous rather than a finite list of choices.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Cake eating is a continuous-state/action finite-horizon allocation problem; backward induction balances marginal utilities and yields the source's geometric-denominator consumption rule for logarithmic utility.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **213-217**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=215|Course book pp. 213-217]].
- Source sections: Appendix D, Introduction, D.4.1 Dynamic Programming Formulation, Logarithmic Utility, Optimal Allocation Rule, Return-on-Investment Extension.
- Printed page + 2 = PDF viewer page for this supplied edition.
