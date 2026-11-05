---
module: DLMAIRIL01 Reinforcement Learning
unit: appendices
chapter: "Appendix B: Towers of Hanoi"
note_type: worked_appendix
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=189|Course book pp. 187-201]]"
printed_pages: [187, 201]
pdf_pages: [189, 203]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# Appendix B: Towers of Hanoi

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Represent the puzzle as a deterministic shortest-path problem.
- Explain state enumeration, admissible moves and integer indexing.
- Connect value iteration, policy storage and published path reconstruction.

## 2. Detailed explanation in my own words

### Rules and the recursive solution

The puzzle has three pegs and $N$ disks, ordered from smallest to largest. Initially all disks are on peg 1; the aim is to place them all on peg 3.

![[99_attachments/course_book/figure_26.png]]

*Figure 26: Towers of Hanoi game platform* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=190|Course book pp. 188]]. Original visual from the supplied IU course book; not redrawn.

Only the top, smallest disk on a nonempty peg can move. It may never be placed on a smaller disk. These rules preserve size ordering within each peg.

The source's classical recursive method is:

1. Move the smallest $N-1$ disks from the starting peg to the spare peg.
2. Move the largest disk to the destination.
3. Move the $N-1$ disks from the spare peg to the destination.

This uses the fact that smaller disks can be placed on the largest disk, and a solution between one pair of pegs can be relabelled for another pair. The source distinguishes programming a previously deduced rule from having dynamic programming determine an optimal solution.

### State representation

Represent a configuration as an $N$-entry vector. Entry $i$ identifies the peg containing disk $i$, with disk indices ordered by size. Once peg membership is known, the legal within-peg order is already determined.

There are $3^N$ configurations. The initial vector is $(1,\ldots,1)$; the terminal vector is $(3,\ldots,3)$.

![[99_attachments/course_book/figure_27.png]]

*Figure 27: Towers of Hanoi game platform with four disks. The state x = 3, 1, 2, 3 is illustrated.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=193|Course book pp. 191]]. Original visual from the supplied IU course book; not redrawn.

**Source notation caution:** the illustrative vector and accompanying prose on p. 191 are not consistent. Interpret the preserved drawing using the explicit rule above: each component records a disk's peg, not a disk's vertical height.

### Actions and admissibility

The possible move types are the six ordered pairs of distinct pegs:

![[99_attachments/course_book/table_04.png]]

*Table 4 (original course-book table)* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=196|Course book pp. 194]]. Original visual from the supplied IU course book; not redrawn.

Not every move type is legal in every state. A move is excluded if the source peg is empty or its top disk is larger than the destination's top disk. Moving to an empty destination is legal.

The implementation's `topDisks` information identifies the smallest disk present on each peg so these checks can be made without storing a separate physical tower representation.

### Turn puzzle solving into optimization

Charge one unit per legal move and zero after reaching the terminal state. Minimizing accumulated cost now means finding the fewest moves:

$$
V^*(x)=\min_{a\in A_x}[1+V^*(q(x,a))]
\quad\text{for nonterminal }x,\qquad V^*(x_\Delta)=0.
$$

$q(x,a)$ is the deterministic successor. Value iteration repeatedly evaluates legal move cost plus successor value. It determines the shortest distance to completion and the next move attaining it.

### Enumerating and accessing states

| Source component | Purpose |
|---|---|
| `incState` | Increment a peg-position vector like a three-symbol odometer, left component first. |
| `pHash` | Convert a vector to its canonical integer state index. |
| `valueFunctionOld` | Fixed values from the preceding sweep. |
| `valueFunction` | New values from the current sweep. |
| `policyFunction` | Index of the selected successor state. |
| `stateMap` | Convert an integer index back to its state vector. |

For four disks, the source enumeration starts with `(1,1,1,1)`, `(2,1,1,1)`, `(3,1,1,1)`, `(1,2,1,1)`. The last vector `(3,3,3,3)` has index 80; after it the odometer wraps to the initial vector.

Using indices allows one-dimensional value and policy arrays of length $3^N$, rather than indexing them directly with an $N$-component vector.

### Updating the values and extracting a path

The source code initializes values to zero, keeps the terminal value zero, and evaluates nonterminal states using the old sweep. Illegal action candidates receive `bigM = 3**nDisk`, so they do not win the minimum. A fixed-size candidate-action list can be reused.

The policy stores a **successor index**, not simply a peg-pair label. Iteration stops when the integer values no longer change.

Starting at the initial index, follow `policyFunction` repeatedly and use `stateMap` to decode each index. The number of moves is `valueFunction[0]`; the reconstructed path includes one additional state because it contains both endpoints.

### The published three-disk result

For `nDisk = 3`, the program reports **seven moves and eight displayed states**:

| Displayed state | Disk-peg vector, smallest disk first |
|---|---|
| 1 | `(1,1,1)` |
| 2 | `(3,1,1)` |
| 3 | `(3,2,1)` |
| 4 | `(2,2,1)` |
| 5 | `(2,2,3)` |
| 6 | `(1,2,3)` |
| 7 | `(1,3,3)` |
| 8 | `(3,3,3)` |

This table translates the source's printed tower output into the same state encoding; it is not a new example. `makeTowerPic` provides the source's text-based tower display.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Configuration state | The peg containing each disk. |
| Admissible action | A move obeying top-disk and size-order rules. |
| Shortest-path value | Minimum remaining number of moves. |
| Canonical index | Unique integer identifying an enumerated state. |
| Old/new sweep arrays | Separate preceding and updated value estimates. |
| Successor policy | Policy storage containing the next state's index. |

## 4. Important formulas / algorithms / steps

$3^N$ states; six possible peg-to-peg move types, restricted by admissibility.

$$
V^*(x)=\min_{a\in A_x}[1+V^*(q(x,a))],\qquad V^*(x_\Delta)=0.
$$

Enumerate with `incState`, access by `pHash`, reconstruct through `policyFunction` and `stateMap`. Three-disk output: seven moves, eight states.

## 5. Source-book example

The published three-disk path starts with all disks on peg 1 and ends with all on peg 3. The smallest disk first moves to peg 3, permitting the next disk to move to peg 2; following the stored successor indices yields the seven-move solution shown above.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why is disk-to-peg membership sufficient to define a state?
> The move rules already determine the size ordering within every peg.

> [!question]- 2. How many states are represented for N disks?
> Three to the power N.

> [!question]- 3. What makes a potential peg-to-peg move illegal?
> An empty source or placing a larger disk on a smaller top disk.

> [!question]- 4. What objective does the one-unit move cost encode?
> The minimum number of moves to reach the terminal configuration.

> [!question]- 5. What does incState do?
> Enumerate vectors with a three-symbol odometer.

> [!question]- 6. What does pHash do?
> Convert a state vector to its canonical integer index.

> [!question]- 7. Why keep old and new value arrays?
> Evaluate one sweep against a fixed preceding value function.

> [!question]- 8. What does the stored policy contain?
> The integer index of the minimizing successor state.

> [!question]- 9. Why does the output contain one more state than moves?
> A path includes its initial state as well as every successor.

> [!question]- 10. What result does the source report for three disks?
> Seven moves and eight states.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** The Hanoi implementation converts legal disk moves into a deterministic shortest-path problem, enumerates configurations by integer indices, and follows the converged successor policy to reconstruct the published minimum-move path.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **187-201**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=189|Course book pp. 187-201]].
- Source sections: Appendix B, Rules, B.2.1 General Recursive Solution, B.2.2 Dynamic Programming Solution, B.3 Program Implementation, State and Action Representations, Value Iteration, Optimal Path Output.
- Printed page + 2 = PDF viewer page for this supplied edition.
