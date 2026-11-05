---
module: DLMAIRIL01 Reinforcement Learning
unit: 2
chapter: "2.4 General Utility Functions"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=102|Course book pp. 100-108]]"
printed_pages: [100, 108]
pdf_pages: [102, 110]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 2.4 General Utility Functions

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain why expected monetary payoff alone need not capture preferences.
- Relate utility shape to marginal value and risk attitude.
- Distinguish minimum total distance from minimax distance in the source example.

## 2. Detailed explanation in my own words

### Why a larger expected payoff can still be undesirable

An objective measure such as money or distance does not necessarily capture a decision maker's willingness to accept risk. The source contrasts a certain payoff with a riskier action:

![[99_attachments/course_book/table_02.png]]

*Table 2 (original course-book table)* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=102|Course book pp. 100]]. Original visual from the supplied IU course book; not redrawn.

Action 1 pays 500 under either event; Action 2 pays -1000 or 3000, each with probability one half. Expected payoffs are 500 and 1000 respectively. Maximizing expected money selects Action 2, yet a decision maker may reject its loss risk. Repeated decisions and a one-time decision may also lead to different preferences.

### 2.4.1 Utility and marginal utility

A utility function $u(x)$ represents how valuable an amount of a commodity is to a particular decision maker. The nominal price and the utility need not agree.

The source's thirsty customer may value a first drink at one dollar but accept only 0.50 for a second and 0.20 for a third. Additional drinks become less useful after thirst is reduced.

A retailer faces a different situation. To sell at one dollar with a required profit margin, the retailer might accept a purchase cost of 0.25 per unit near zero stock. As stock grows relative to expected demand, the marginal benefit of an extra bottle also declines.

![[99_attachments/course_book/figure_09.png]]

*Figure 9: Utility functions for thirsty customer and retailer for the soft drink example of Sec. 2.4.1. The gray lines represent constant marginal utility of $1.00 and $0.25 per bottle.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=104|Course book pp. 102]]. Original visual from the supplied IU course book; not redrawn.

The graph's slope expresses **marginal utility**, not total utility. Both curves increase, but their slopes decline. The customer and retailer have different valuations even though they refer to the same commodity.

### 2.4.2 Concavity, convexity and risk attitude

For a **concave** function, a chord connecting two curve points lies below or on the curve. For a **convex** function, it lies above or on the curve. Strict versions exclude equality except at endpoints. A linear function is both non-strictly concave and convex.

For the smooth examples in this section, negative curvature corresponds to strict concavity and positive curvature to strict convexity. The classification used by the book is:

| Utility class | Shape | Preference represented |
|---|---|---|
| Risk-averse | Strictly concave | Diminishing marginal utility; comparable losses matter more than gains. |
| Risk-neutral | Linear | Constant marginal utility. |
| Risk-seeking | Strictly convex | Increasing marginal utility; potential gains receive greater emphasis. |

![[99_attachments/course_book/figure_10.png]]

*Figure 10: Examples of risk-averse, risk-neutral and risk-seeking utility functions.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=106|Course book pp. 104]]. Original visual from the supplied IU course book; not redrawn.

At wealth $w$, compare utility gained from increasing wealth by $\Delta w$ with utility lost when wealth decreases by the same amount:

$$
\Delta u^+=u(w+\Delta w)-u(w),\qquad
\Delta u^-=u(w)-u(w-\Delta w).
$$

For concavity, the loss effect exceeds the corresponding gain effect; for convexity, the gain effect is larger. This links geometric shape with the source's interpretation of risk preferences.

The cake-eating problem in [[06_worked_appendices/d_cake_eating|Appendix D]] applies diminishing marginal utility to allocation over time.

### 2.4.3 The stagecoach example with minimax cost

The original route criterion minimizes the sum of distances. The new criterion assumes that long segments between towns are especially undesirable, while unlimited rest is possible at a town. Optimize the **longest segment** rather than total travel distance:

$$
V^*(x)=\min_{a\in A_x}
\max\{R(x,a),V^*(q(x,a))\}.
$$

The outer minimum chooses a route; the inner maximum combines its current segment with the worst later segment. These are different operations and represent a different performance goal.

Start with terminal value zero. At I and J, the last segments give values 3 and 2.

![[99_attachments/course_book/figure_11.png]]

*Figure 11: Stagecoach problem with minimax cost criterion. Section of the map of Fig. 2.1 representing the calculations for Stages 4 and 5.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=108|Course book pp. 106]]. Original visual from the supplied IU course book; not redrawn.

At G, compare $\max(4,3)=4$ via I with $\max(2,2)=2$ via J, so choose J. At H, compare $\max(3,3)=3$ via I with $\max(5,2)=5$ via J, so choose I.

Continuing backward gives the unique minimax-optimal route **A-C-F-H-I-K**, with largest segment **3**. Its total distance is also 15, but the other two minimum-total-distance routes do not share its minimax optimum.

Thus, an optimal policy is meaningful only relative to its chosen criterion. Equal total costs need not imply equal worst-stage costs, and monetary expectation need not imply equal utility.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Utility | Value of an amount to a particular decision maker. |
| Marginal utility | Change in utility associated with another unit. |
| Concave | The chord between curve points lies below or on the curve. |
| Convex | The chord lies above or on the curve. |
| Risk-averse / neutral / seeking | Concave / linear / convex utility in the source classification. |
| Minimax distance | The smallest achievable largest route-segment distance. |

## 4. Important formulas / algorithms / steps

$$
\Delta u^+=u(w+\Delta w)-u(w),\qquad
\Delta u^-=u(w)-u(w-\Delta w).
$$

Risk-averse: $\Delta u^->\Delta u^+$ in the source comparison; risk-seeking reverses the inequality.

$$
V^*(x)=\min_{a\in A_x}\max\{R(x,a),V^*(q(x,a))\}.
$$

Stagecoach minimax optimum: longest segment 3 on A-C-F-H-I-K.

## 5. Source-book example

The source payoff table gives Action 1 expected payoff 500 and Action 2 expected payoff 1000. Nevertheless, the risk of losing 1000 under Action 2 can make the certain Action 1 preferable to a particular decision maker. This motivates modeling utility rather than equating preference with expected money.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why might expected monetary payoff be insufficient?
> Decision makers can have different valuations and tolerances for losses.

> [!question]- 2. What does a utility curve's slope represent?
> Marginal utility of an additional unit.

> [!question]- 3. How does a thirsty customer's marginal utility change?
> It falls after the first drink because additional drinks have less value.

> [!question]- 4. Which utility shapes represent risk-aversion, neutrality and seeking?
> Strictly concave, linear and strictly convex respectively.

> [!question]- 5. How does concavity compare equal-sized gains and losses?
> The utility loss is larger than the corresponding utility gain.

> [!question]- 6. What does the minimax stagecoach criterion minimize?
> The greatest distance of any single segment along the route.

> [!question]- 7. Which source route is minimax-optimal?
> A-C-F-H-I-K, with a longest segment of three.

> [!question]- 8. Why can total-distance-optimal routes differ under minimax?
> Their equal sums can hide different largest segment distances.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Utility incorporates decision-maker valuation and risk attitude; changing the cost-accrual criterion can change the optimal policy even when the underlying routes and transitions remain unchanged.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **100-108**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=102|Course book pp. 100-108]].
- Source sections: 2.4, 2.4.1 Utility Functions, 2.4.2 Classification of Utility Function by Risk, 2.4.3 Minimax Criterion: The Stagecoach Problem Revisited.
- Printed page + 2 = PDF viewer page for this supplied edition.
