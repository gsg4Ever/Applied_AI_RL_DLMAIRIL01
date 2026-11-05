---
module: DLMAIRIL01 Reinforcement Learning
unit: 1
chapter: "1.1 Understanding Reinforcement Learning"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=14|Course book pp. 12-31]]"
printed_pages: [12, 31]
pdf_pages: [14, 33]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 1.1 Understanding Reinforcement Learning

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Distinguish supervised, unsupervised and reinforcement learning.
- Define a sequential decision model, policy, value function and Q-factor.
- Explain policy evaluation, policy improvement and Bellman's equation.
- Explain why learning from interaction can be more practical than an explicit model.

## 2. Detailed explanation in my own words

### Learning from data rather than explicit instructions

Machine learning uses observed or simulated data to improve performance instead of requiring every relevant relationship to be programmed explicitly. The book distinguishes three branches by their tasks and available information.

**Supervised learning** learns a mapping $f:X\to Y$ from labelled input-output pairs $(x_i,y_i)$. In handwritten-character recognition, $x_i$ is an image and $y_i$ its true letter. Training aims to make $f(x_i)$ agree with the label, while a separate test sample assesses the resulting classifier on data not used for learning. Quantitative prediction, such as regression, is another supervised task.

Two input-processing methods matter. **Feature selection** retains informative original variables and removes irrelevant or redundant ones. The book contrasts current credit-card balance with city of birth when predicting credit risk. **Feature extraction** constructs derived inputs: image brightness, skewness, corners, lines or circles are examples. Extraction changes the representation; selection chooses among available variables.

**Unsupervised learning** works with unlabelled observations and investigates unknown structure. Clustering groups observations so that they are similar within a group and different between groups. In the handwriting example, a separate algorithm can isolate individual characters before a classifier recognizes them. The book also connects unsupervised methods with feature selection.

**Reinforcement learning** addresses a sequential decision process: a time-ordered sequence of actions changes accumulated cost or reward. The learning problem is not to reproduce a supplied correct label, but to discover a good decision rule through interaction. The book cites games, navigation, robotics and healthcare. Its examples include TD-Gammon, AlphaZero and video-game agents; these illustrate the range of applications rather than supply extra algorithm tutorials.

### 1.1.1 Classical control and adaptive control

Classical control formulates a mathematical model and derives actions that optimize its performance. The inventory example shows why this requires both controllable decisions and an **environment** of exogenous influences.

At the start of week $k$, a retailer observes stock $y_k$, orders $w_k$, and faces demand $d_k$. Sales are

$$
s_k=\min(d_k,y_k+w_k).
$$

Ordering too little can lose current revenue and future customers; ordering too much creates storage costs. A fixed shipping charge $B$ is incurred for a nonzero order. The decision must consider these consequences together, not simply match one week's expected demand.

A control model needs quantities such as retail price, storage expense, shipping expense and a demand distribution. The last is uncertain and must be identified from data. An optimal decision for an estimated model is not necessarily optimal for the actual business.

The **certainty-equivalence** approach acts as though the estimated model were exact, derives its optimal policy, and applies that policy. An **adaptive control system** continues observing operations, improves parameter estimates and recalculates decisions. Adaptation also matters when the environment changes, for example after an advertising campaign increases demand.

Time is divided into decision epochs even if the controlled system operates continuously. A week can be one inventory stage; a chess move can be one game stage. In the toll-booth example, the arrival or departure of a vehicle creates a decision epoch at which a controller can open or close booths. Discrete decision stages can therefore support essentially real-time control.

### 1.1.2 Components of the dynamic-programming model

At stage $j$, observe state $x_j$ and select action $a_j$. The **state space** $X$ contains all possible states. The **action space** $A$ contains potential actions, but only the subset $A_x$ is admissible from state $x$.

$$
\mathcal K=\{(x,a):x\in X,\ a\in A_x\}.
$$

Here $\mathcal K$ denotes the source's state-action space, keeping it distinct from a number of stages also called $K$ elsewhere. The stage cost or reward $R(x,a)$ is defined for admissible pairs.

For deterministic dynamics, the next state is fixed:

$$
x_{j+1}=q(x_j,a_j).
$$

For stochastic dynamics, the transition kernel specifies the successor-state distribution:

$$
P(y\mid x,a)=\Pr(x_{j+1}=y\mid x_j=x,a_j=a).
$$

A deterministic transition can also be represented probabilistically: assign probability one to $q(x,a)$ and zero to other successor states. The tuple of state/action sets, rewards and transition rules is the **model**.

The source distinguishes three lifetimes:

| Lifetime | How stages end |
|---|---|
| Finite horizon | A fixed finite number of stages is specified. |
| Infinite horizon | The process continues indefinitely. |
| Shortest path / episodic | A terminal state is reached after a finite but possibly variable number of stages. |

An absorbing terminal state $x_\Delta$ incurs no further cost. It can be viewed as a process that stays there forever, so termination need not contradict an infinite-time formal representation.

For stage costs $R(x_j,a_j)$, the discounted accumulated cost is

$$
R_{\rm discount}=\sum_{j=1}^{N}\beta^{j-1}R(x_j,a_j),
$$

or the corresponding infinite sum. For finite/shortest-path problems, $\beta=1$ gives total undiscounted cost. For bounded nonnegative costs $R(x,a)\le M$ and $0\le\beta<1$, the geometric-series bound is

$$
R_{\rm discount}\le \frac{M}{1-\beta}.
$$

Discounting therefore makes the infinite accumulated criterion finite under the book's boundedness assumptions.

### 1.1.3 Policies, evaluation and improvement

A **policy** selects actions. A stationary deterministic policy function $\phi(x)\in A_x$ applies the same state-to-action rule at every stage. The objective is to minimize expected cost, or maximize expected reward. Changing rewards to their negatives converts a maximum-reward problem into a minimum-cost problem.

The **memoryless** property means that the current state-action pair supplies the information needed for future transitions and remaining cost; an appropriate policy must respect this information structure. The book's MDP is an infinite-horizon, discounted, stochastic, memoryless model described by $(\mathcal K,R,P,\beta)$.

For a fixed policy $\phi$, its value $V^\phi(x)$ is the expected accumulated cost from initial state $x$. Separate the first stage from the remaining stages:

$$
V^\phi(x)=R(x,\phi(x))+
\beta\sum_{y\in X}P(y\mid x,\phi(x))V^\phi(y).
$$

This is **policy evaluation**, not yet optimization. The policy operator $T^\phi$ replaces the right-hand value function by a candidate function, creating a new function. The evaluation equation becomes the fixed-point equation $V^\phi=T^\phi V^\phi$. Repeated updates

$$
V^{n+1}=T^\phi V^n
$$

approximate the value of the fixed policy under the convergence conditions discussed in the book. An operator maps functions to functions; its fixed point is a function unchanged by the operator.

A **Q-factor** asks a more specific question: what is the expected cost if action $a$ is taken now and policy $\phi$ is followed thereafter?

$$
Q^\phi(x,a)=R(x,a)+
\beta\sum_yP(y\mid x,a)V^\phi(y).
$$

Choosing an action that minimizes this quantity produces a policy-improvement step:

$$
\phi'(x)\in\operatorname*{argmin}_{a\in A_x}Q^\phi(x,a).
$$

The old policy's action is among the available choices, so the minimizing choice cannot have a higher one-step-plus-continuation cost. Repeating the improved choice at every state yields a policy whose value is no worse than the old policy's value.

The optimal value is $V^*(x)=\inf_\phi V^\phi(x)$. If a policy attains it at every state, that policy is optimal. Optimality requires that no alternative first action followed by the optimal continuation can improve the result:

$$
V^*(x)=\min_{a\in A_x}
\left[R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y)\right].
$$

This is **Bellman's optimality equation**. It differs from policy evaluation by minimizing over actions instead of fixing $\phi(x)$.

**Value iteration** repeatedly applies the optimality operator and generates value-function estimates. **Policy iteration** instead alternates evaluation of a current policy (the critic) with improvement of that policy (the actor). Equal optimal costs can be achieved by different actions, so an optimal value can be unique without the optimal policy being unique.

### 1.1.4 Why explicit dynamic programming becomes difficult

The automated-poker example exposes two separate obstacles.

First, exact tables can be enormous. Five-card hands from a 52-card deck yield $\binom{52}{5}=2{,}598{,}960$ combinations. Including remaining rounds and bets makes the state space larger. Selecting up to three cards to discard gives at least

$$
\binom50+\binom51+\binom52+\binom53=26
$$

possible card-discard actions. If there are $K$ relevant rounds, a reward table needs at least $K\times2{,}598{,}960\times26$ entries. A dense transition table is larger still, with a state-size-squared factor. Specialized structure can reduce this burden, but it cannot be assumed.

Second, even if storage were available, the correct reward and transition tables still have to be specified. The game's formal rules do not make the full relationship between an action and eventual winnings easy to derive, especially in an interacting environment.

### 1.1.5 The agent-environment platform

![[99_attachments/course_book/figure_01.png]]

*Figure 1: Agent-environment interaction model of reinforcement learning, adapted from figure 3.1 of (Sutton & Barto, 2018a).* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=31|Course book pp. 29]]. Original visual from the supplied IU course book; not redrawn.

The **agent** observes the current state and previous reward, selects an action, and can retain history. The **environment** takes the action and produces the new state and reward. It may be a simulator or the actual control domain.

The underlying model can exist without being represented explicitly inside the agent. Learning can target $V^\phi(x)$ or $Q(x,a)$ directly from observed outcomes. Storing a state-value approximation requires objects of size roughly $|X|$; an action-value table requires roughly $|X||A_x|$. This is cheaper than a dense transition kernel requiring a state-size-squared factor. Approximation by neural networks is developed in the next section.

### 1.1.6 Learning behavior versus application behavior

The source introduces **exploration** as trial-and-error behavior that collects information and **exploitation** as use of the currently learned best decisions. A simulated game opponent must both learn and provide effective opposition; an inventory policy trained in simulation may focus on learning before deployment.

Unit 1 uses this online-performance distinction to motivate on-policy versus off-policy learning. Unit 4 later states the action/target distinction explicitly: SARSA evaluates the successor action selected by the current policy, whereas Q-learning uses a maximizing action-value target. Keep both explanations connected to their actual update equations rather than interpreting “off-policy” as a prohibition on good actions.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Sequential decision process | A sequence of decisions affecting accrued cost or reward. |
| Feature selection | Retaining informative original inputs and removing irrelevant/redundant inputs. |
| Feature extraction | Constructing derived inputs from original data. |
| Certainty equivalence | Optimizing an estimated model as if its parameters were exact. |
| Admissible pair | A state together with an action permitted from that state. |
| Policy value | Expected accumulated cost or return under a specified policy. |
| Q-factor | Value of a specified first action followed by a policy. |
| Bellman operator | A transformation of a candidate value function using the decision model. |
| Exploration / exploitation | Learning through trials / using currently preferred decisions. |

## 4. Important formulas / algorithms / steps

**Model:** state space, admissible actions, stage cost/reward, transition rule and lifetime/discounting.

**Evaluation:** fix $\phi$, then solve $V^\phi=T^\phi V^\phi$.

**Improvement:** $\phi'(x)\in\arg\min_{a\in A_x}Q^\phi(x,a)$ for costs.

**Optimality:** solve $V^*=T^*V^*$; replace minima by maxima for reward maximization.

**Policy iteration:** evaluate the policy, improve its actions, and repeat until no strict value improvement remains.

## 5. Source-book example

The book's policy-improvement calculation uses state $x=3$, discount $\beta=0.9$, stage costs $R(3,1)=53$ and $R(3,2)=35$, and current continuation values $V'(4)=46.4$, $V'(5)=14.7$, $V'(2)=23.5$.

Action 1 reaches states 4 and 5 with equal probability:

$$
Q(3,1)=53+0.9\frac{46.4+14.7}{2}=80.495.
$$

Action 2 reaches state 2:

$$
Q(3,2)=35+0.9(23.5)=56.15.
$$

Since this is cost minimization, the improved policy selects **action 2**. Immediate cost alone is not the evaluation rule; the discounted expected continuation is part of each comparison.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What distinguishes reinforcement learning from supervised learning?
> RL learns sequential decisions from interaction rewards rather than labelled correct input-output pairs.

> [!question]- 2. How do feature selection and feature extraction differ?
> Selection keeps informative existing inputs; extraction constructs derived inputs.

> [!question]- 3. What is certainty-equivalence control?
> Compute an optimal rule for the estimated model while treating that estimate as exact.

> [!question]- 4. What makes a state-action pair admissible?
> The action belongs to the set of actions allowed from that state.

> [!question]- 5. How do deterministic and stochastic transitions differ?
> A transition function specifies one successor; a kernel specifies probabilities of successors.

> [!question]- 6. What are the three SDP lifetimes in the book?
> Finite horizon, infinite horizon and shortest path/episodic termination.

> [!question]- 7. Why discount bounded infinite-horizon costs?
> A discount below one bounds the sum by a convergent geometric series.

> [!question]- 8. What does a policy value function evaluate?
> Expected total cost or return from a state while following a specified policy.

> [!question]- 9. What does a Q-factor evaluate?
> A selected first action followed by a given or optimal continuation policy.

> [!question]- 10. How does Bellman optimality differ from fixed-policy evaluation?
> Optimality minimizes or maximizes over admissible actions; evaluation keeps the policy fixed.

> [!question]- 11. How do value iteration and policy iteration differ?
> Value iteration updates values directly; policy iteration alternates policy evaluation and improvement.

> [!question]- 12. What are the two explicit-model obstacles in the poker example?
> Huge state/action tables and difficulty specifying accurate reward and transition models.

> [!question]- 13. What does the environment output after an action?
> A reward and a successor state.

> [!question]- 14. Which action wins the source's state-3 cost comparison?
> Action 2: its Q-factor is 56.15 versus 80.495 for action 1.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Reinforcement learning optimizes sequential decisions by learning from agent-environment interaction; dynamic programming supplies value, Q-factor and Bellman principles, while learning and approximation address explicit-model and table-size obstacles.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **12-31**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=14|Course book pp. 12-31]].
- Source sections: 1.1, 1.1.1 Classical Control Theory, 1.1.2 The Basics of Dynamic Programming, 1.1.3 Control of an SDP, 1.1.4 Reinforcement Learning and Dynamic Programming, 1.1.5 The Reinforcement Learning Platform, 1.1.6 On- and Off-Policy Reinforcement Learning.
- Printed page + 2 = PDF viewer page for this supplied edition.
