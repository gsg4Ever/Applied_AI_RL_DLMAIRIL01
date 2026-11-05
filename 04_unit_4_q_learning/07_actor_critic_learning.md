---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.7 Actor Critic Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=164|Course book pp. 162-168]]"
printed_pages: [162, 168]
pdf_pages: [164, 170]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.7 Actor Critic Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Combine value approximation and direct policy optimization.
- Explain the source actor-critic updates and separate learning rates.
- Explain advantage estimation and the extensions named in the book.

## 2. Detailed explanation in my own words

### Combine an actor with a learned critic

The **actor** chooses actions according to policy parameters $\theta$. The **critic** estimates how valuable those actions are, using parameters $\omega$. The source compares this to an athlete improving through a coach's feedback.

![[99_attachments/course_book/figure_23.png]]

*Figure 23: Actor-Critic Setup* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=165|Course book pp. 163]]. Original visual from the supplied IU course book; not redrawn.

The architecture resembles policy iteration: evaluation supplies information for improvement. Unlike exact dynamic programming, however, rewards and transition probabilities are not fully known. A learned critic can be inaccurate, so a proposed policy change is not guaranteed to be an improvement.

![[99_attachments/course_book/table_03.png]]

*Table 3 (original course-book table)* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=166|Course book pp. 164]]. Original visual from the supplied IU course book; not redrawn.

The original table contrasts learning values and deriving actions, optimizing a policy from returns, and combining learned values with policy-gradient updates.

### Policy gradient from an approximate Q critic

The critic approximates the current policy's action values:

$$
Q_\omega(s,a)\approx Q^{\pi_\theta}(s,a).
$$

The actor uses that approximation:

$$
\Delta\theta=
\alpha\nabla_\theta\log\pi_\theta(a\mid s)Q_\omega(s,a).
$$

The basic source algorithm receives reward and a successor state, chooses the next action under the current policy, updates the actor, and updates the critic through a SARSA-style TD error:

$$
\delta=r+\gamma Q_\omega(s',a')-Q_\omega(s,a),
\qquad
\Delta\omega=\beta\delta\nabla_\omega Q_\omega(s,a).
$$

Here $\alpha$ and $\beta$ are actor and critic learning rates; $\gamma$ remains the discount. This $\beta$ is not the early-unit discount factor.

There is no successor-action maximum in this critic update, because $a'$ follows the current policy. The presented combination is therefore connected to SARSA and REINFORCE rather than simply a pair of independent Q-learning networks.

### Parallel interactions

Multiple agents can collect experience to improve efficiency. In a **synchronous** setup, they use the same policy and update together after a batch. In an **asynchronous** setup, policy changes can reach agents at different times, avoiding a wait for every interaction to finish simultaneously.

The book also notes introducing replay into actor-critic setups to improve sample efficiency. It names these ideas without supplying a new full implementation in this section.

### Advantage: how much better is this action than the state's baseline?

$$
A(s,a)=Q(s,a)-V(s).
$$

$V(s)$ represents the overall value of being in the state, while advantage measures how the chosen action compares with that baseline. The source's classroom analogy separates class-average performance from a student's relative performance.

A state-value TD error gives a sampled advantage estimate:

$$
\delta=r+\gamma V(s')-V(s).
$$

This estimates advantage from reward and a successor-value prediction; it is not a claim that one stochastic sample equals its exact expected advantage. Using this estimate avoids needing separate full networks for both Q and V in the described approach.

The source introduces **general advantage estimation** as an extension for continuous-control problems, without giving its complete formula.

### Extensions named in the course book

| Method | Description supplied by the book |
|---|---|
| A2C | Synchronous advantage actor-critic. |
| A3C | Asynchronous advantage actor-critic. |
| Soft Actor Critic | Optimize reward together with entropy to encourage exploratory behavior. |
| Proximal Policy Optimization | Stabilize policy updates using a surrogate objective, including clipping or a divergence-based penalty. |

The source motivates these extensions with variance and stability concerns. Large inconsistent policy changes can harm learning; smaller controlled changes can be more stable. No implementation details or equations beyond those present in the book are added here.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Actor | Learns the parameterized action-selection policy. |
| Critic | Learns a value estimate used to guide policy updates. |
| Actor/critic learning rates | Separate step sizes for policy and value parameters. |
| Synchronous / asynchronous | Coordinated updates / updates reaching agents at differing times. |
| Advantage | Action value minus the baseline state value. |
| Entropy objective | A randomness-related exploration objective named in the SAC discussion. |
| Surrogate objective | A replacement optimization objective used to control policy changes. |

## 4. Important formulas / algorithms / steps

$$
\Delta\theta=\alpha\nabla_\theta\log\pi_\theta(a\mid s)Q_\omega(s,a),
\qquad
\delta=r+\gamma Q_\omega(s',a')-Q_\omega(s,a).
$$

$$
A(s,a)=Q(s,a)-V(s),\qquad
\hat A=r+\gamma V(s')-V(s).
$$

Actor improves the policy; critic estimates its values. A2C is synchronous, A3C asynchronous; SAC and PPO are introduced at the qualitative level supplied by the book.

## 5. Source-book example

The book's coach analogy captures the two roles: an athlete acts and adjusts technique, while the coach estimates what is working and supplies feedback. In the source classroom analogy, V is class-average performance and advantage is performance relative to that average.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What do actor and critic learn?
> The actor learns the policy; the critic learns values used to guide that policy.

> [!question]- 2. Why can learned actor-critic updates fail to improve a policy?
> The critic is estimated from experience rather than evaluated from a fully known model.

> [!question]- 3. Why does the basic critic update have no next-action maximum?
> The successor action is chosen by the current policy, as in SARSA.

> [!question]- 4. Are the actor and critic learning rates necessarily identical?
> No; the source uses separate rates.

> [!question]- 5. What is the advantage function?
> Action value minus state value.

> [!question]- 6. What provides the source's sampled advantage estimate?
> Reward plus discounted next-state value minus current-state value.

> [!question]- 7. How do A2C and A3C differ?
> A2C is synchronous and A3C asynchronous.

> [!question]- 8. What does Soft Actor Critic add to reward optimization?
> An entropy-related objective encouraging exploration.

> [!question]- 9. How does the book describe PPO stabilization?
> Use a surrogate objective with clipping or a divergence-based penalty to avoid overly large policy changes.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Actor-critic combines direct policy updates with learned value feedback; advantage centers action quality relative to state value, and the source's synchronous, asynchronous, entropy and surrogate-objective extensions address efficiency, variance and stability.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **162-168**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=164|Course book pp. 162-168]].
- Source sections: 4.7, Actor and Critic Roles, Basic Actor-Critic Algorithm, Synchronous and Asynchronous Updates, Advantage Function, A2C and A3C, Soft Actor Critic, Proximal Policy Optimization.
- Printed page + 2 = PDF viewer page for this supplied edition.
