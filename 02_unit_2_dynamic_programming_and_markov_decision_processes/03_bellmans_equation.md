---
module: DLMAIRIL01 Reinforcement Learning
unit: 2
chapter: "2.3 Bellman's Equation"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=81|Course book pp. 79-100]]"
printed_pages: [79, 100]
pdf_pages: [81, 102]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 2.3 Bellman's Equation

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Derive the optimal first-action/continuation recursion.
- Compare backward induction, value iteration and policy iteration.
- Explain the stagecoach and treasure-search results and complexity limits.

## 2. Detailed explanation in my own words

### 2.3.1 Bellman's principle of optimality

Define the optimal cost for each initial state:

$$
V^*(x)=\inf_{\phi\in\Phi}V^\phi(x).
$$

This is a lower bound on every policy's cost at state $x$. If one policy attains these values for all states, it is optimal. The existence of a numerical infimum alone does not automatically guarantee that an admissible policy attains it.

Now take action $a$ from state $x$ and act optimally thereafter. Call the resulting cost $Q^*(x,a)$, also written $V^*(x,a)$ in the source. The best initial decision gives

$$
V^*(x)=\min_{a\in A_x}Q^*(x,a).
$$

For deterministic transitions and a general accrual function $H$:

$$
V^*(x)=\min_{a\in A_x}H(R(x,a),V^*(q(x,a))).
$$

For stochastic discounted additive costs:

$$
V^*(x)=\min_{a\in A_x}
\left[R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y)\right].
$$

The deterministic discounted version replaces the expectation by $V^*(q(x,a))$. Minimax replaces additive combination by a maximum. Reward maximization replaces the outer minimum by a maximum.

The principle relies on the current state containing the information needed to choose an optimal continuation. It does not eliminate questions of solution existence, uniqueness, convergence or computational cost.

### 2.3.2 Backward induction

For a finite horizon, the terminal value is known. Once the final-stage values are determined, the preceding stage can use them on the right side of Bellman's equation. Continue backward until reaching the initial stage.

1. Set the terminal value, usually zero after termination.
2. Evaluate each admissible final-stage action using that value.
3. Store the optimal value and an optimizing action for each final-stage state.
4. Repeat for the previous stage, using the stored successor values.
5. Continue through every remaining stage.

The method works for the source's deterministic stagecoach and stochastic treasure-search problems. It need not enumerate complete trajectories; it compares current actions plus already optimized continuations.

#### Stagecoach: every backward stage

Start with $V^*(K)=0$.

![[99_attachments/course_book/figure_06.png]]

*Figure 6: Stagecoach problem. Section of the map of Fig. 2.1 representing the transition from Stage 5 to Stage 6.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=86|Course book pp. 84]]. Original visual from the supplied IU course book; not redrawn.

At I and J, the only action goes to K, giving values 3 and 2.

For G, compare $4+3=7$ via I with $2+2=4$ via J, so choose J. For H, compare $3+3=6$ via I with $5+2=7$ via J, so choose I.

At E, the alternatives are $7+4=11$ and $6+6=12$; choose G. At F, compare $6+4=10$ with $3+6=9$; choose H.

At the next preceding layer:

| State | Via E | Via F | Optimal value | Optimal action(s) |
|---|---|---|---|---|
| B | $4+11=15$ | $6+9=15$ | 15 | E or F |
| C | $3+11=14$ | $3+9=12$ | 12 | F |
| D | $2+11=13$ | $4+9=13$ | 13 | E or F |

![[99_attachments/course_book/figure_07.png]]

*Figure 7: Stagecoach problem. Section of the map of Fig. 2.1 representing the transition from Stage 1 to Stage 2.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=88|Course book pp. 86]]. Original visual from the supplied IU course book; not redrawn.

At A, compare $1+15=16$, $3+12=15$ and $2+13=15$. The optimal distance is **15**, achieved by three routes:

- A-C-F-H-I-K.
- A-D-E-G-J-K.
- A-D-F-H-I-K.

This is an explicit example of one optimal value and several optimal action sequences.

#### Reward modification and missing state information

The book then adds a one-time 100-dollar sale at C or H and a travel cost of twice the distance. A town alone no longer supplies all reward-relevant information: at E, a later visit to H earns the sale only if it has not already occurred at C.

Thus, the original state definition is not memoryless for this modified reward. The source solves the particular example using constrained route comparisons: two of the distance-15 routes also visit C or H and therefore attain both a sale and the shortest distance. The point is to check the state-information assumption whenever the reward definition changes.

#### Stochastic treasure search

The book's treasure is worth 13,000 dollars, boat/crew hire costs 700 dollars per hour, and search time is exponential with mean 13 hours. Hire must be chosen before the day begins and paid for even if the treasure is found early. At most five hours can be hired per day.

The state $(w,s)$ records days remaining and whether treasure has been found; the action is $a\in\{0,\ldots,5\}$. If search is still needed, finding probability is $1-e^{-a/13}$. Successful states have no further search reward.

$$
V^*(w,0)=\max_{a\in\{0,\ldots,5\}}
\left[13000(1-e^{-a/13})-700a+
e^{-a/13}V^*(w-1,0)\right].
$$

Boundary values are zero for no days remaining or already-found treasure.

| Days remaining | Hire if not found | Expected optimal value reported by source |
|---|---|---|
| 1 | 5 hours | 650.7 |
| 2 | 4 hours | 1121.5 |
| 3 | 3 hours | 1469.4 |

Chronologically, hire **3, then 4, then 5 hours**, only if still searching. More days available initially permit cautious spending without committing all search time in advance.

The recursion can be extended to larger $w$ without recomputing the already solved final days.

![[99_attachments/course_book/figure_08.png]]

*Figure 8: Output from sample python program for the Treasure Seeking problem Sec. u2.sec.treasure.example.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=93|Course book pp. 91]]. Original visual from the supplied IU course book; not redrawn.

The published 500-day output has a long region of one-hour choices and an eventual reward plateau near 3,500 dollars. The source discusses no-search choices at large horizons. Since the available zero-hour action preserves the preceding value in the displayed recurrence, do not interpret that description as proof that an extra available day must worsen the optimum.

See [[06_worked_appendices/a_treasure_seeking|Appendix A]] for its program structure.

### 2.3.3 Value iteration and fixed points

An **operator** maps a candidate value function to another value function. Applying the Bellman operator gives

$$
(TV)(x)=\min_{a\in A_x}
\left[R(x,a)+\beta\sum_yP(y\mid x,a)V(y)\right].
$$

The solution is a fixed point $V^*=TV^*$. Value iteration starts with an initial function and repeatedly computes $V^{n+1}=TV^n$. Under the book's relevant regularity conditions, these become increasingly accurate approximations of the optimum.

The scalar source example uses $f(x)=1-0.95e^{-x}$. Starting at 1 produces approximately 0.6505 and 0.5043, eventually approaching the fixed point 0.2870483.

![[99_attachments/course_book/fixed_point_p094.png]]

*Unnumbered course-book illustration, printed p. 94* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=96|Course book pp. 94]]. Original visual from the supplied IU course book; not redrawn.

The fixed point is where the function intersects the identity line. This picture illustrates why applying an update rule repeatedly can solve an equation without directly obtaining a closed-form expression.

### 2.3.4 Policy iteration: critic and actor

For a fixed policy, replace minimization by the policy's prescribed action:

$$
(T^\phi V)(x)=R(x,\phi(x))+
\beta\sum_yP(y\mid x,\phi(x))V(y).
$$

Policy evaluation finds its fixed point $V^\phi$. Policy iteration alternates:

1. **Critic:** evaluate the current policy.
2. **Actor:** choose minimizing actions using that evaluated continuation.
3. Repeat until no strict value improvement remains.

Value iteration generates successive value functions; policy iteration generates successive policies with evaluated values. Different policies can share the same optimal value. Tie handling and stopping rules therefore concern value improvement, not a requirement that one uniquely optimal policy exist.

The source notes that policy iteration can converge in few iterations in suitable finite settings, while algorithm efficiency depends on the problem; it is not automatically the best finite-horizon solver.

### 2.3.5 The curse of dimensionality

Let $N_x$ be the number of states and $N_a$ bound admissible actions per state. In a deterministic Bellman update, each action requires one successor-value lookup. In a dense stochastic update, each action requires a sum over possible successors:

| Object or computation | Source's size/order |
|---|---|
| Deterministic full value-iteration sweep | $N_xN_a$ |
| Dense stochastic full sweep | $N_x^2N_a$ |
| Value or policy table | $N_x$ |
| Reward or Q table | $N_xN_a$ |
| Dense transition table | $N_x^2N_a$ |

If each action has only a few possible successors, sparse structure can reduce the stochastic sum. This is a property to exploit when present, not a guarantee for every model.

The source's ten-queue example with capacities of 20 permits $(20+1)^{10}\approx1.67\times10^{13}$ queue configurations. Even after dynamic programming avoids full-path enumeration, exact per-state calculations can be infeasible. This remaining burden motivates approximation and reinforcement learning.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Principle of optimality | Choose the best first action plus an optimal continuation from its successor. |
| Backward induction | Solve finite-horizon stages in reverse order from terminal values. |
| Fixed point | A value/function unchanged by its defining transformation. |
| Bellman operator | Updates values by optimizing stage cost plus expected continuation. |
| Policy iteration | Alternate evaluation and improvement of a policy. |
| Curse of dimensionality | State/action representation and calculation grow rapidly with model complexity. |
| Sparse transitions | Only a small subset of potential successor probabilities are nonzero. |

## 4. Important formulas / algorithms / steps

$$
V^*(x)=\min_{a\in A_x}\left[R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y)\right].
$$

Backward induction uses known later-stage values. Value iteration uses $V^{n+1}=TV^n$. Policy iteration alternates evaluation and improvement.

Dense sweep complexity: $N_xN_a$ deterministic versus $N_x^2N_a$ stochastic. Stagecoach optimum: 15; treasure-search chronological policy: 3, 4, 5 hours if needed.

## 5. Source-book example

On the final treasure-search day, compare the six possible hiring durations using 13000(1-exp(-a/13))-700a. The source selects five hours and reports value 650.7. Insert that value as the unsuccessful-search continuation for the preceding day, yielding four hours and 1121.5; the first day then selects three hours and 1469.4.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does Bellman's principle optimize?
> A first admissible action followed by optimal continuation from the next state.

> [!question]- 2. Why begin backward induction at the terminal stage?
> The terminal continuation value is known, so preceding values can be calculated.

> [!question]- 3. What is the optimal stagecoach distance?
> Fifteen, attained by three source routes.

> [!question]- 4. Why does the one-time-sale modification break the original memoryless model?
> Future sale reward depends on whether a sale already occurred, not just the current town.

> [!question]- 5. What must the treasure-search state contain?
> Days remaining and whether the treasure has been found.

> [!question]- 6. What is the source's three-day treasure policy?
> Hire three, then four, then five hours on chronological days if still searching.

> [!question]- 7. What expected value does the source report for three remaining days?
> 1469.4 dollars.

> [!question]- 8. What is a Bellman fixed point?
> A value function V that satisfies V equals T applied to V.

> [!question]- 9. How does policy evaluation differ from policy optimization?
> Evaluation fixes the actions of one policy; optimization compares admissible actions.

> [!question]- 10. Why can optimal policies be nonunique?
> Different actions can attain the same minimum cost or maximum return.

> [!question]- 11. What are dense deterministic and stochastic sweep complexities?
> Nx times Na and Nx squared times Na, respectively.

> [!question]- 12. When can sparse transitions reduce stochastic complexity?
> When each action reaches only a few possible successors.

> [!question]- 13. What causes the source ten-queue example to become infeasible?
> Twenty-one possible lengths in each of ten queues create about 1.67 times 10^13 configurations.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Bellman's equation combines a current decision with optimal continuation; backward induction, value iteration and policy iteration solve it in different ways, but large state spaces can still make exact optimization impractical.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **79-100**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=81|Course book pp. 79-100]].
- Source sections: 2.3, 2.3.1 Bellman's Principle of Optimality, 2.3.2 Backward Induction, 2.3.3 Value Iteration, 2.3.4 Policy Iteration: The Actor-Critic Method, 2.3.5 Algorithms for the Optimal Control of MDPs.
- Printed page + 2 = PDF viewer page for this supplied edition.
