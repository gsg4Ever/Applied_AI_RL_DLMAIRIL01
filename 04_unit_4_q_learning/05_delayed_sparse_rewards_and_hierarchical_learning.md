---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.5 Delayed Sparse Rewards and Hierarchical Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=158|Course book pp. 156-158]]"
printed_pages: [156, 158]
pdf_pages: [158, 160]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.5 Delayed Sparse Rewards and Hierarchical Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain why long reward-free trajectories impede learning.
- Distinguish value functions for different goals from a single universal approximation.
- Explain meta-controller versus controller roles in hierarchical learning.

## 2. Detailed explanation in my own words

### Delayed feedback

Some tasks reveal success after only a few actions; others require a long correct sequence before any positive reward. If most trajectories terminate before reaching that reward, the agent gets little guidance about which earlier actions were useful.

![[99_attachments/course_book/figure_21.png]]

*Figure 21: Blind Cliff Walk* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=159|Course book pp. 157]]. Original visual from the supplied IU course book; not redrawn.

In the **blind cliff walk**, the agent begins at the first position and must move along a chain. A wrong decision causes a fall and restart; reward appears only at the end. The agent does not know the chain length or how long success will take. This example helped motivate prioritized replay in the cited work.

### Multiple goals are different knowledge questions

![[99_attachments/course_book/figure_22.png]]

*Figure 22: Layout of a complex games with multiple sub-goals* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=159|Course book pp. 157]]. Original visual from the supplied IU course book; not redrawn.

The source's game-layout example contains keys, doors, treasure and movement constraints. Knowledge about reaching a key is not the same as knowledge about collecting a particular treasure or exiting through a door.

A **general value function** $V_g(s)$ assesses state $s$ with respect to goal $g$. In the cited **Horde** architecture, multiple sub-agents called **demons** learn different goal-oriented questions. Their value functions represent different aspects of environmental knowledge.

A **universal value function** $V(s,g;\theta)$ uses one parameterized mapping with both state and goal as inputs, rather than treating every goal as a completely separate function. The source notes that a neural network can approximate this mapping.

### Independent goal knowledge versus hierarchical behavior

Knowing how to reach several goals does not automatically identify their dependency order. Reaching an exit door is useless before acquiring the key required to open it. Collecting treasure may increase score but may not enable progress to the next level.

The presented **hierarchical DQN** separates two roles:

| Component | Decision |
|---|---|
| Meta-controller | Given the current state, choose the next goal. |
| Controller | Choose actions that accomplish the selected goal. |

After a goal is completed, the meta-controller chooses another. In the source game, it first focuses on obtaining the key, then on opening the door to the next level.

Thus, goal-conditioned value learning represents what can be accomplished, while the hierarchy organizes which accomplishment should come next.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Sparse reward | Nonzero task reward is rare. |
| Delayed reward | Feedback appears only after a long action sequence. |
| General value function | A state's value for a particular goal. |
| Universal value function | One parameterized value mapping conditioned on state and goal. |
| Demon | A goal-question-specific sub-agent in the source Horde architecture. |
| Meta-controller | Selects a goal. |
| Controller | Selects actions to attain that goal. |

## 4. Important formulas / algorithms / steps

Goal-specific value: $V_g(s)$. Universal approximation: $V(s,g;\theta)$.

Hierarchical DQN cycle: choose a goal with the meta-controller, act toward it with the controller, then choose the next goal after completion.

## 5. Source-book example

In the source game's key-and-door sequence, a controller learns actions that reach the key. The meta-controller must select this goal before the door-opening goal, because reaching the locked door without a key does not advance the level.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. Why is the blind cliff walk hard to learn?
> A long correct action sequence is required before reward, and a wrong decision restarts the episode.

> [!question]- 2. What does Vg(s) represent?
> The value of state s while pursuing goal g.

> [!question]- 3. What do demons do in the Horde architecture?
> Learn separate goal-oriented questions about the environment.

> [!question]- 4. How does a universal value function differ?
> One parameterized function accepts both a state and a goal.

> [!question]- 5. What does the meta-controller choose?
> The next goal to pursue.

> [!question]- 6. What does the lower-level controller choose?
> Actions that achieve the selected goal.

> [!question]- 7. Why is independent knowledge of goals not always sufficient?
> Goals can depend on one another and require a particular order.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Sparse delayed rewards make useful feedback difficult to obtain; goal-conditioned values represent different tasks, and hierarchical learning separates selecting goals from acting to accomplish them.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **156-158**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=158|Course book pp. 156-158]].
- Source sections: 4.5, Blind Cliff Walk, General and Universal Value Functions, Horde Architecture, Hierarchical Deep Q-Learning.
- Printed page + 2 = PDF viewer page for this supplied edition.
