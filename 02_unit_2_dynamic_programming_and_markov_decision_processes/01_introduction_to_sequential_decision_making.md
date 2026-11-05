---
module: DLMAIRIL01 Reinforcement Learning
unit: 2
chapter: "2.1 Introduction to Sequential Decision Making"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=54|Course book pp. 52-59]]"
printed_pages: [52, 59]
pdf_pages: [54, 61]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 2.1 Introduction to Sequential Decision Making

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Recognize the common decision structure across the source's applications.
- Formulate the stagecoach routing example and understand enumeration.
- Explain how decomposing a route reduces repeated work.

## 2. Detailed explanation in my own words

### 2.1.1 One framework for many applications

A sequential decision process links decisions made now with later outcomes and an accumulated performance measure. Dynamic programming supplies a common structure for optimization across different domains.

In **operations research**, the source lists resource allocation, search, scheduling, supply-chain management, inventory, queues, utility expansion and project planning. These problems can often be assessed using revenue, cost, distance or probability of success.

In **economics**, the same structure supports savings and investment choices, models of retirement behavior, policy assessment and game theory. Such applications can seek qualitative principles rather than a particular numerical policy.

In **artificial intelligence**, sequential choices occur in games, navigation and other control tasks. Reinforcement learning builds on dynamic-programming ideas but can obtain useful decision rules from observed interactions when exact modeling is impractical.

The remainder of the unit first defines the model, then formalizes optimization with Bellman's equation, develops solution algorithms, and broadens performance measures using utility.

### 2.1.2 The stagecoach problem

The source map is a directed graph of eleven towns A-K. A journey starts at A and ends at K. Each directed edge is an available route labelled with distance; the objective is to find the minimum-distance complete journey.

![[99_attachments/course_book/figure_03.png]]

*Figure 3: Stagecoach problem map.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=58|Course book pp. 56]]. Original visual from the supplied IU course book; not redrawn.

The route A-D-F-G-I-K has edge distances $2,4,6,4,3$, hence total distance $19$. Replacing its final part by G-J-K yields distances $2,4,6,2,2$ and total $16$. Being able to compare two routes is not yet a method for finding the best route among all possibilities.

**Constructive enumeration** lists every possible route, calculates its distance and selects the minimum. This is the brute-force solution. The graph's layer structure makes the count straightforward:

![[99_attachments/course_book/figure_04.png]]

*Figure 4: Stagecoach problem. Map of Fig. 2.1 is shown partitioned into Stages k = 1, …, 6.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=59|Course book pp. 57]]. Original visual from the supplied IU course book; not redrawn.

| State layer | Towns |
|---|---|
| 1 | A |
| 2 | B, C, D |
| 3 | E, F |
| 4 | G, H |
| 5 | I, J |
| 6 | K |

There are five decision stages between the six layers. The numbers of available choices multiply to

$$
3\times2\times2\times2\times1=24.
$$

This is the **rule of product**: when each task has a fixed number of choices, multiply the counts to obtain the number of complete choice sequences. The source's prose contains an inconsistent fourth-stage count, but its map and displayed final product use two choices, I or J.

For 24 routes, enumeration is possible. For many more stages and choices, the number of full routes grows exponentially. The backgammon state-count example demonstrates why naive enumeration cannot scale to complex games.

### 2.1.3 Divide and conquer

The cost of a future route segment does not depend on the route used to reach its start. For example,

$$
D(\text{A-D-F-G-I-K})
=D(\text{A-D-F-G})+D(\text{G-I-K})=12+7.
$$

At G, the choice of continuation can be optimized independently of how G was reached. This is the key information-saving observation: the current location suffices for the remaining routing problem.

Write $D^*(A,K\mid G)$ for the shortest route constrained to pass through G. Then

$$
D^*(A,K\mid G)=D^*(A,G)+D^*(G,K).
$$

Every complete route passes through G or H, so

$$
D^*(A,K)=\min\{
D^*(A,G)+D^*(G,K),\
D^*(A,H)+D^*(H,K)\}.
$$

Instead of enumerating all 24 full routes, the book's split enumerates six A-G routes, six A-H routes, two G-K routes and two H-K routes: **16 shorter segments**. Each segment also requires fewer arithmetic operations than a full route. Thus even this partial decomposition is more efficient.

Dynamic programming develops this recursive decomposition further. It solves simpler remaining problems and uses their values inside earlier decisions, rather than repeatedly recalculating all complete paths.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Directed graph | Nodes represent towns and directed edges represent available route segments. |
| Constructive enumeration | An explicit list of every candidate solution. |
| Rule of product | Multiply fixed task-choice counts to count complete sequences. |
| Constraint | A condition restricting which candidate solutions are permitted. |
| Divide and conquer | Decompose a complex problem into simpler subproblems. |
| Remaining distance | Cost of the continuation from the current town to the destination. |

## 4. Important formulas / algorithms / steps

Route distance is the sum of its edge labels. The source graph has $24$ complete routes.

For a route required to pass through G:

$$
D^*(A,K\mid G)=D^*(A,G)+D^*(G,K).
$$

Compare the best routes through G and H, using their independent segment optima. This reduces the source's first enumeration from 24 full routes to 16 shorter segments.

## 5. Source-book example

The two source routes A-D-F-G-I-K and A-D-F-G-J-K share the first segment of distance 12. Their remaining distances are 7 and 4 respectively, so the totals are 19 and 16. Reusing the shared segment is the first step toward a recursive solution.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What is a sequential decision process?
> A process in which a sequence of actions influences accrued cost or reward.

> [!question]- 2. What is constructive enumeration?
> List every candidate solution explicitly and evaluate it.

> [!question]- 3. How many complete routes are in the source stagecoach map?
> Twenty-four, from three times two times two times two times one choices.

> [!question]- 4. Why does brute-force enumeration scale poorly?
> The number of complete action sequences multiplies across stages.

> [!question]- 5. Why can the continuation from G be optimized independently?
> The remaining route distances depend on the current town, not on the route previously taken.

> [!question]- 6. What does the constraint in D*(A,K given G) mean?
> The candidate route must pass through town G.

> [!question]- 7. What is the first decomposition's route-count saving?
> Six plus six plus two plus two shorter segments instead of twenty-four full routes.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Dynamic programming exploits the fact that optimal continuations can be solved as smaller subproblems, avoiding repeated enumeration of complete decision sequences.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **52-59**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=54|Course book pp. 52-59]].
- Source sections: 2.1, 2.1.1 Applications of Dynamic Programming, 2.1.2 Introduction to Dynamic Programming: The Stagecoach Problem, 2.1.3 Divide and Conquer Algorithms.
- Printed page + 2 = PDF viewer page for this supplied edition.
