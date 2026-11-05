---
module: DLMAIRIL01 Reinforcement Learning
unit: 1
chapter: "1.2 Components of Reinforcement Learning Systems"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=34|Course book pp. 32-50]]"
printed_pages: [32, 50]
pdf_pages: [34, 52]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 1.2 Components of Reinforcement Learning Systems

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Explain Monte Carlo evaluation and incremental learning.
- Compare full-return and bootstrapped targets, including TD(lambda).
- Distinguish Q-learning from SARSA and explain continuing exploration.
- Explain how neural networks approximate values and reduce representation costs.

## 2. Detailed explanation in my own words

### 1.2.1 Monte Carlo policy evaluation

An episodic process runs from an initial state to an absorbing terminal state. To evaluate a policy $\phi$, repeatedly follow it from an initial state $x_0$, observe each episode's total cost or reward, and average those returns:

$$
\widehat V^\phi(x_0)=\frac1n\sum_{i=1}^n R_i.
$$

No transition kernel is needed for this calculation. The environment supplies sampled outcomes instead of the full mathematical model.

One episode can also evaluate states visited after its start. For a state $x_k$ on the trajectory, the rewards from that point until termination form a sample return from $x_k$. Group such returns by state and average them to estimate the whole value function, rather than restarting an experiment separately for every state.

**First-visit Monte Carlo** uses the return following the first occurrence of a state within an episode. **Every-visit Monte Carlo** uses returns following every occurrence. The book discusses differing finite-sample bias and variance: every-visit uses more observations, but random visit counts can affect its sample-mean bias. It states that both approaches become increasingly accurate with sufficient samples and that neither is uniformly preferable.

### 1.2.2 Updating an estimate without retaining its full sample

For sequential observations, the sample mean can be updated using the old mean and the new observation:

$$
\bar x_{m+1}=\bar x_m+\frac1{m+1}(x_{m+1}-\bar x_m).
$$

The general learning pattern is **old estimate + learning rate × (target − old estimate)**. The target is what the update moves toward; the learning rate controls how far it moves.

With rate one, the new estimate is just the current target. That is unstable when targets are noisy. Smaller, often diminishing rates temper random fluctuations. A visit-based rate also allows an estimate to summarize past samples without storing each observation.

For the full return $G_k$ after state $x_k$, Monte Carlo updates

$$
\widehat V^\phi(x_k)\leftarrow
\widehat V^\phi(x_k)+
\gamma\left[G_k-\widehat V^\phi(x_k)\right].
$$

The book's episodic examples use undiscounted sums; discounting can be retained when defined by the model.

A second target comes from the policy-value recursion:

$$
r_{k+1}+\beta\widehat V^\phi(x_{k+1}).
$$

The corresponding one-step update is

$$
\widehat V^\phi(x_k)\leftarrow\widehat V^\phi(x_k)+
\gamma\left[r_{k+1}+\beta\widehat V^\phi(x_{k+1})-\widehat V^\phi(x_k)\right].
$$

This is **bootstrapping**: an estimate is itself part of another estimate's target. The full-return target observes all later rewards, whereas the one-step target substitutes an estimated continuation.

### Bias, variance and consistency

For an estimator $\hat\theta$, bias is $\mathbb E[\hat\theta]-\theta$. Mean squared error combines variance and squared bias:

$$
\operatorname{MSE}(\hat\theta)=
\operatorname{Var}(\hat\theta)+
\left(\operatorname{Bias}(\hat\theta)\right)^2.
$$

The best estimator for a particular task is not necessarily the least biased or the least variable individually. It is the one with the best combined error. The book contrasts an unbiased but more variable full-return target with a biased but often lower-variance bootstrapped target. A sequence of estimates is **consistent** when its MSE tends to zero.

### 1.2.3 Temporal differences and TD(lambda)

The one-step discrepancy is the temporal difference:

$$
d_k=r_{k+1}+\beta\widehat V^\phi(x_{k+1})-\widehat V^\phi(x_k).
$$

The one-step update adds $\gamma d_k$. The source generalizes this to a weighted sum of later differences:

$$
\widehat V^\phi(x_k)\leftarrow\widehat V^\phi(x_k)
+\gamma\sum_{i=k}^{N-1}\lambda^{i-k}d_i.
$$

This is the episodic form displayed in source Eq. (1.23). The **trace-decay parameter** $\lambda\in[0,1]$ controls how much later differences influence the update. The source identifies TD(0) with the one-step bootstrap and TD(1) with the Monte Carlo endpoint; intermediate values combine their effects. Its displayed weighting should be read with the accompanying episode/discount convention, not silently replaced by another formula.

Larger $\lambda$ includes more future information; smaller $\lambda$ emphasizes immediate bootstrapped information. The book reports that practical choices are often strictly between zero and one and depend on the problem.

### 1.2.4 Reusing experience and learning with sparse rewards

Experience acquired from the environment can be expensive or rare. **Experience replay** stores it and resamples it for further learning rather than discarding it after one update.

With **sparse rewards**, most actions receive zero feedback; a game might provide a positive reward only for its final winning action. Many unsuccessful episodes then give little indication of how to approach the goal.

The book presents three related ideas:

| Idea | How it makes experience more useful |
|---|---|
| Prioritized/selective replay | Give greater resampling weight to informative or successful/high-reward experiences. |
| Hindsight replay | Reinterpret a failed attempt as success for a different goal that was actually achieved. |
| Intrinsic reward | Reward behavior such as useful curiosity even without completing the external task. |

The source's hindsight example is a vehicle that misses the intended location but reaches a nearby one. Relabelling the achieved location as the goal creates usable goal-reaching experience; it does not claim that the original target was reached.

### 1.2.5 Policy improvement without enumerating every policy

Policy evaluation alone answers how good a given policy is. Control asks which policy is best. In principle, compare all policies, but their count grows combinatorially: the poker example permits at least $26^{K\times2{,}598{,}960}$ mappings.

The actor-critic interpretation avoids this enumeration. A critic estimates the policy value, for example with TD methods. An actor varies actions, uses their estimated Q-factors and improves the decision rule. Evaluation and improvement repeat.

### 1.2.6 Q-learning and SARSA

For optimal continuation in the minimum-cost convention,

$$
Q^*(x,a)=R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y),
\qquad V^*(y)=\min_{b\in A_y}Q^*(y,b).
$$

Substitute the second identity into the first, then replace the expected continuation by a sampled next state. This yields the source's Q-learning update:

$$
\widehat Q(x_k,a_k)\leftarrow\widehat Q(x_k,a_k)+
\gamma\left[r_{k+1}+\beta\min_{b\in A_{x_{k+1}}}
\widehat Q(x_{k+1},b)-\widehat Q(x_k,a_k)\right].
$$

The behavior action need not be the current minimizing action. The target evaluates an optimal estimated continuation even when experience is gathered by another behavior rule: **off-policy** learning.

**SARSA** uses the actual next action selected by the current policy:

$$
\widehat Q(x_k,a_k)\leftarrow\widehat Q(x_k,a_k)+
\gamma\left[r_{k+1}+\beta\widehat Q(x_{k+1},a_{k+1})
-\widehat Q(x_k,a_k)\right].
$$

Its name records the observed sequence: **state, action, reward, state, action**. It is **on-policy** because the successor action in the target follows the same policy used to generate the trajectory. Unit 4 revisits both updates in the maximum-reward convention.

### 1.2.7 Why a greedy policy still needs exploration

A greedy policy chooses the action with the currently best Q estimate. That estimate may be inaccurate. If an action is never revisited, no new evidence can correct an initially bad ranking.

To identify the true best action, all relevant Q estimates must become sufficiently accurate. The source's convergence discussion requires continuing visits to every relevant state-action pair; purely exploiting a premature estimate can prevent this.

An **epsilon-greedy** policy chooses the greedy action with probability $1-\epsilon$ and explores with probability $\epsilon$. Exploration can select randomly among admissible actions. The source allows $\epsilon$ to shrink, but slowly enough that exploratory actions continue to occur; it gives $\epsilon_k=1/k$ as an illustrative schedule.

The unit also names **prioritized sweeping**, **E3** and **R-max**. E3 mixes exploration with control of the estimated known model. R-max makes underrepresented actions attractive through optimistic rewards, or equivalently lower apparent costs. Unit 5 develops these model-based ideas.

### 1.2.8 Neural-network approximation

A tabular value representation becomes impractical for huge state spaces such as board configurations. Artificial neural networks approximate the mapping from state information to values with a set of weights instead of a separate independently stored entry for every state.

The **multilayer perceptron** in the book has input, hidden and output nodes. Edges carry weights; hidden nodes apply a nonlinear threshold function to weighted inputs. The source also permits direct input-to-output, or skip-layer, connections.

![[99_attachments/course_book/table_01.png]]

*Table 1 (original course-book table)* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=47|Course book pp. 45]]. Original visual from the supplied IU course book; not redrawn.

For a hidden node $j$, the essential computation is

$$
h_j=\varphi\!\left(\sum_iw_{ij}x_i\right),
\qquad
\varphi(u)=\frac{e^u}{1+e^u}
$$

for the threshold-function example used in the book. Output combines hidden-node contributions and any direct input contributions. A bias node provides the constant input one; the source does not apply the threshold transformation to its output node. Training determines the weights, so the network acts as a nonlinear regression model.

**Deep networks** use more than one hidden layer. The poker illustration supplies 52 card-indicator inputs and hidden nodes associated with suits and ranks. Early layers summarize features of the hand; later layers use those summaries to approximate the value.

![[99_attachments/course_book/figure_02.png]]

*Figure 2: ANN architecture for automated poker application of Sec. u1.box.poker.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=50|Course book pp. 48]]. Original visual from the supplied IU course book; not redrawn.

This illustration explains how representation and feature processing can be combined. Its advantage is not only compressed storage: a function approximation can assign useful estimates without observing every individual state separately.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Monte Carlo evaluation | Estimate policy value by averaging observed episode returns. |
| First-visit / every-visit | Use one return per state per episode / all state occurrences. |
| Target | The quantity toward which an update moves the estimate. |
| Learning rate | The step size controlling the magnitude of each update. |
| Bootstrapping | Using an estimated continuation value inside the update target. |
| Temporal difference | Sampled reward plus estimated continuation minus the current estimate. |
| Trace decay | The parameter controlling the influence of later temporal differences. |
| Sparse rewards | Informative nonzero rewards occur rarely. |
| SARSA | An on-policy update using the observed successor action. |
| Function approximation | Represent values with a parameterized function instead of independent table entries. |

## 4. Important formulas / algorithms / steps

$$
\text{new estimate}=\text{old estimate}
+\text{learning rate}\,(\text{target}-\text{old estimate}).
$$

Monte Carlo target: observed episode return. TD(0) target: $r+\beta\widehat V(x')$.

Q-learning target (cost convention): $r+\beta\min_b\widehat Q(x',b)$.

SARSA target: $r+\beta\widehat Q(x',a')$, with $a'$ selected by the behavior policy.

$$
\operatorname{MSE}=\operatorname{variance}+\operatorname{bias}^2.
$$

## 5. Source-book example

In the book's episodic evaluation example, an episode produces $r_1+\cdots+r_N$. Its suffix $r_{k+1}+\cdots+r_N$ is also a return sample for a state visited at position $k$. Reusing these suffixes evaluates multiple states from one episode.

In the poker-network example above, a card input equals one when that card is in the hand. Suit/rank connections summarize the hand before later layers estimate its value. The original architecture figure is therefore part of the explanation, not a separate decoration.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. How is an episodic policy value estimated by Monte Carlo?
> Run episodes with the policy and average returns associated with each state.

> [!question]- 2. What is the difference between first-visit and every-visit evaluation?
> First-visit uses the first occurrence per episode; every-visit uses all occurrences.

> [!question]- 3. What is the general incremental update pattern?
> Old estimate plus learning rate times target minus old estimate.

> [!question]- 4. Why is learning rate one risky for noisy targets?
> It replaces the accumulated estimate entirely with the latest noisy target.

> [!question]- 5. What does bootstrapping mean?
> An estimated value is used as part of the update target.

> [!question]- 6. What are the components of mean squared error?
> Estimator variance plus squared estimator bias.

> [!question]- 7. What do TD(0) and TD(1) denote in this unit?
> The book identifies the one-step bootstrap and Monte Carlo endpoints respectively.

> [!question]- 8. What does the trace-decay parameter control?
> The influence of later temporal differences in the update.

> [!question]- 9. How does Q-learning's target differ from SARSA's?
> Q-learning uses the best estimated successor action; SARSA uses the action selected by the current policy.

> [!question]- 10. Why can a greedy policy get stuck?
> Unchosen actions receive no new evidence, so initially wrong estimates may never be corrected.

> [!question]- 11. What does epsilon-greedy combine?
> Greedy action selection with probability one minus epsilon and exploration with probability epsilon.

> [!question]- 12. How does hindsight replay use a failed episode?
> Relabel an actually achieved outcome as the goal and learn from that successful alternative task.

> [!question]- 13. What is the purpose of neural-network value approximation?
> Compact representation and useful value estimates without an independent table entry or visit for every state.

> [!question]- 14. What do the poker network's early hidden layers represent?
> Features such as suit and rank counts derived from card-indicator inputs.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Policy evaluation learns returns or bootstrapped values; Q-learning and SARSA turn these ideas into control, while continuing exploration, replay and neural-network approximation address data and representation limitations.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **32-50**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=34|Course book pp. 32-50]].
- Source sections: 1.2, 1.2.1 Policy Evaluation, 1.2.2 Reinforcement Learning and Iterative Updating, 1.2.3 TD(lambda), 1.2.4 Experience Replay and Sparse Rewards, 1.2.5 Policy Improvement, 1.2.6 Q-factors and the Control Problem, 1.2.7 Exploration versus Exploitation, 1.2.8 Artificial Neural Networks and Reinforcement Learning.
- Printed page + 2 = PDF viewer page for this supplied edition.
