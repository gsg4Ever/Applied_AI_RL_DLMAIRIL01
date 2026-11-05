---
module: DLMAIRIL01 Reinforcement Learning
unit: appendices
chapter: "Appendix E: Q Learning Treasure Seeking"
note_type: worked_appendix
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=219|Course book pp. 217-224]]"
printed_pages: [217, 224]
pdf_pages: [219, 226]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# Appendix E: Q Learning Treasure Seeking

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Separate the random-behavior agent from the treasure-search simulator.
- Explain terminal and nonterminal targets and visit-based step sizes.
- Compare the published learned policy and values with exact backward induction.

## 2. Detailed explanation in my own words

### Same task, a different way of learning its solution

The treasure is worth 13,000; the boat costs 700 per scheduled hour, with zero through five integer hours available per day. The search time is exponential with mean 13 hours. The rental is paid for the scheduled duration even if the treasure is found earlier.

For three remaining days, the exact dynamic-programming solution from Section 2.3 and Appendix A is chronological rentals **3, 4, 5 hours if needed**.

Appendix E learns this task from simulated interactions rather than using the transition probabilities in every value update.

### Agent versus environment

The state contains days remaining $w$ and whether the treasure is already found. The agent chooses an integer action $a\in\{0,\ldots,5\}$ with equal probability. Its behavior is deliberately exploratory rather than following the current greedy policy.

The simulator draws $Z$ exponentially with mean 13. If $Z\le a$, search succeeds. The sampled reward is

$$
r=
\begin{cases}
13000-700a,&Z\le a,\\
-700a,&Z>a.
\end{cases}
$$

An unsuccessful search transitions to $(w-1,0)$; a successful one to $(w-1,1)$. Terminate when treasure is found or no days remain, then restart at $(3,0)$.

Although the **simulator** knows its distribution, the **agent's learning update** consumes sampled reward and successor information instead of calculating an explicit expected transition sum.

### The Q-learning update

The source uses a visit-dependent learning rate:

$$
\eta(x,a)=\frac1{n(x,a)}.
$$

For an unsuccessful, nonfinal search:

$$
Q(w,a)\leftarrow Q(w,a)+\frac1{n(w,a)}
\left[r+\max_bQ(w-1,b)-Q(w,a)\right].
$$

At a terminal step:

$$
Q(w,a)\leftarrow Q(w,a)+\frac1{n(w,a)}
[r-Q(w,a)].
$$

There is no continuation after success or the last usable day. The concrete code uses an undiscounted continuation, unlike discounted examples elsewhere. The visit count is increased before dividing by it.

**Implementation reading detail:** the source variable named `target` stores the bracketed **TD error**, not the reward-plus-future target on its own. Distinguish the variable label from its actual expression.

### Program objects and loop

| Source setting/object | Meaning |
|---|---|
| Seed 13215 | Published pseudorandom-sequence initialization. |
| `nStages = 3` | Maximum search days per episode. |
| `Qfactor` | Shape `(3,6)`, initialized to 2000 for each candidate value. |
| `visitCount` | Shape `(3,6)`, initialized to zero. |
| `nReplications = 1000000` | Number of simulated episodes specified by the book. |
| `endSearch` | Flag indicating terminal success or exhaustion of days. |

Q-array row `w-1` means $w$ days remaining. At each step choose a random duration, simulate search, calculate reward, increment the visited pair's count and update its Q-value. Then terminate or reduce $w$.

After all replications, extract each row's maximum as its value estimate and the maximizing column as its policy. These notes describe the supplied listing and its reported output; they do not rerun the million-episode program.

### Published result and indexing

The source prints policy vector `[5,4,3]`. Its rows correspond to one, two and three **remaining** days:

| Days remaining | Learned action | Published learned value, rounded | Exact value, rounded |
|---|---|---|---|
| 1 | 5 | 656.2 | 650.7 |
| 2 | 4 | 1137.5 | 1121.5 |
| 3 | 3 | 1511.4 | 1469.4 |

The full source output is approximately 656.1925, 1137.4760 and 1511.3770. Reading rows in chronological execution order gives the initial three-hour choice, followed by four and then five if needed.

The final printed policy equations use inconsistent day labels. Interpret them together with the program's remaining-day row order; do not reverse the chronological policy based on those labels alone.

### Policy can be right before values are precise

The learned actions match the exact policy, but the values are not exact. Selecting the largest action estimate needs the correct ordering, not perfectly accurate numerical estimates for every action.

The source closes by emphasizing slow Q-value convergence, motivating the learning modifications discussed in the teaching units. Correct policy output is therefore not evidence that all estimated returns have converged exactly.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Behavior policy | The source's uniformly random rental selection. |
| Simulator | Produces search outcomes, rewards and successor states. |
| Terminal TD target | Immediate reward without future continuation. |
| Visit-based step size | One divided by visits to the experienced pair. |
| Remaining-day row | Q-array row w-minus-one for w days remaining. |
| Policy versus value accuracy | Correct action ranking can precede precise value estimates. |

## 4. Important formulas / algorithms / steps

Nonterminal target: $r+\max_bQ(w-1,b)$. Terminal target: $r$.

$$
Q(w,a)\leftarrow Q(w,a)+
\frac{\text{target}-Q(w,a)}{n(w,a)}.
$$

Source vector `[5,4,3]` means one/two/three days remaining; chronological policy is three/four/five hours if needed.

## 5. Source-book example

The book's million-episode output chooses the exact rental policy but estimates the three-day value as about 1511.4 instead of 1469.4. This demonstrates the source's distinction between an already correct maximizing action and incomplete numerical value convergence.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What behavior does the source agent use?
> Uniformly random rental durations from zero through five hours.

> [!question]- 2. Does finding the treasure early reduce the scheduled rental bill?
> No; the full chosen duration is paid.

> [!question]- 3. What determines a successful simulated search?
> An exponential search-time sample no greater than the scheduled duration.

> [!question]- 4. When does an episode terminate?
> When treasure is found or the final available search day is exhausted.

> [!question]- 5. What future value is used in a terminal update?
> None; the target is the immediate reward.

> [!question]- 6. What is the source learning rate for a visited pair?
> One divided by that pair's incremented visit count.

> [!question]- 7. What does Qfactor row w-minus-one represent?
> A search state with w days remaining.

> [!question]- 8. What does the source variable named target actually store?
> The TD error, including subtraction of the current Q-value.

> [!question]- 9. How should policy vector [5,4,3] be read?
> Actions for one, two and three remaining days, giving chronological three, four and five.

> [!question]- 10. Why can the learned policy be correct with inaccurate values?
> Correct action ranking can occur before all values are numerically precise.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** The source treasure Q-learner learns from uniformly random simulated episodes, uses terminal-aware targets and reciprocal visit counts, and recovers the exact policy while its published value estimates remain approximate.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **217-224**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=219|Course book pp. 217-224]].
- Source sections: Appendix E, Treasure-Search Model, Agent-Environment Interaction, Q-Learning Updates, Computer Implementation, Published Output and Exact Comparison.
- Printed page + 2 = PDF viewer page for this supplied edition.
