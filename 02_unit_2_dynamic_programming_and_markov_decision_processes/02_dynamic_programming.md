---
module: DLMAIRIL01 Reinforcement Learning
unit: 2
chapter: "2.2 Dynamic Programming"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=61|Course book pp. 59-78]]"
printed_pages: [59, 78]
pdf_pages: [61, 80]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 2.2 Dynamic Programming

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Define the stochastic and deterministic components of an SDP.
- Distinguish lifetime, time homogeneity, cost accrual and policy information.
- Explain expected values and the controlled-Markov-chain interpretation.

## 2. Detailed explanation in my own words

### 2.2.1 Probability concepts needed for the model

A **sample space** contains possible experiment outcomes. An **event** is a subset of outcomes and has a probability between zero and one. A random variable assigns a numerical value to an outcome; its **support** is the set of values it can take.

A discrete support is finite or countably indexed. A continuous support cannot be exhaustively represented as such a sequence. A distribution specifies probabilities of outcomes or events.

The source's three-coin experiment has eight equally likely head/tail sequences. Counting heads gives support $\{0,1,2,3\}$ and probabilities $\{1/8,3/8,3/8,1/8\}$. Conditional probability is

$$
P(A\mid B)=\frac{P(A\cap B)}{P(B)},\qquad P(B)>0.
$$

Conditioning the coin example on an odd number of heads gives $P(X=3\mid X\text{ odd})=1/4$.

### Precisely defining the decision model

At a decision epoch, observe $x\in X$, select $a\in A_x$, incur cost/reward $R(x,a)$, and transition. Deterministic transitions use $q(x,a)$; stochastic transitions use $P(y\mid x,a)$. The admissible state-action space is

$$
\mathcal K=\{(x,a):x\in X,\ a\in A_x\}.
$$

For the stagecoach model, a state is a current town and an action is the next town. Admissible pairs correspond to arrows in the graph, the cost is the edge distance, and $q(x,a)=a$.

The destination K can be excluded from decision states because no travel decision follows it. Alternatively, include it with a **dummy action** $\Delta$, a zero cost and absorbing termination. The latter representation avoids an empty admissible-action set and can make the model easier to extend.

The **memoryless** property requires that transition and remaining-cost behavior depend on the current state-action pair rather than unrecorded history. If a relevant aspect of history matters, the state representation must account for it before the usual recursions can be used.

### Lifetime and time homogeneity are different properties

Finite horizon means a fixed finite number of stages; shortest path means a variable finite termination time; infinite horizon means no fixed ending. A terminal state can be absorbing and cost-free.

**Time homogeneous** means the model's transition and cost rules do not change by stage. **Time inhomogeneous** means a component does change. A finite-horizon inventory policy may need both current stock and the day index, even when physical stock alone appears to describe the system.

Including time in the state, such as $(w_j,j)$, permits a stationary-looking policy on the expanded state space. A stage index is information, not just a label, whenever the remaining horizon affects the best action.

### Cost accrual: what is being optimized?

The book expresses aggregation recursively with $H(a,b)$, combining the current-stage quantity and future accumulated quantity:

| Accrual method | Recursive combination | Performance meaning |
|---|---|---|
| Total additive | $H(a,b)=a+b$ | Sum all costs/rewards. |
| Discounted additive | $H(a,b)=a+\beta b$ | Reduce the weight of future costs/rewards. |
| Minimax cost | $H(a,b)=\max(a,b)$ | Minimize the largest single-stage cost. |
| Maximin reward | $H(a,b)=\min(a,b)$ | Maximize the smallest single-stage reward. |

For bounded costs and discount below one, the infinite sum is bounded by $M/(1-\beta)$. The horizon and aggregation rule must be chosen together so that the optimization criterion is meaningful.

The course-deviation example explains **minimax**. Minimizing the sum of absolute deviations might tolerate one catastrophic deviation in exchange for many small later ones. Minimizing the largest deviation directly targets the safety-relevant worst stage.

The transportation example explains **maximin**. For available fuel $f_k$, added fuel $g_k$ and mission distance $d_k$, define $r_k=(f_k+g_k)/d_k$. The weakest fuel-per-distance margin across missions determines whether every mission meets the required threshold, so maximize the minimum $r_k$.

### 2.2.2 Information and policy rules

Additional information cannot worsen an ideal optimal decision: the decision maker can ignore it. However, it can make the computation much larger. The goal is to retain information needed for decisions and discard unnecessary history.

A general action rule can use prior state-action history $H_j$ together with current state $x_j$. For a memoryless model, an optimal rule need not separately use that history. It can be written $a_j=\phi_j(x_j)$. If dependence on the stage is incorporated into the state, a stationary policy $\phi(x)$ becomes possible.

This reasoning connects careful state definition with computational efficiency. It does not say that arbitrary history can always be discarded.

### 2.2.3 Value functions and recursion

For deterministic dynamics under a fixed policy, discounting yields

$$
V^\phi(x)=R(x,\phi(x))+
\beta V^\phi(q(x,\phi(x))).
$$

Set $\beta=1$ for total additive cost. For a deterministic minimax criterion, use

$$
V^\phi(x)=\max\{R(x,\phi(x)),V^\phi(q(x,\phi(x)))\}.
$$

For stochastic dynamics, use the expectation of accumulated cost. A discrete expectation weights each possible value by its probability:

$$
\mathbb E[X]=\sum_x xP(X=x).
$$

If a stage reward is itself random, its model cost $R(x,a)$ can be its conditional expected value. Conditioning on the next state gives the fixed-policy recursion

$$
V^\phi(x)=R(x,\phi(x))
+\beta\sum_yP(y\mid x,\phi(x))V^\phi(y).
$$

The simple expected-value recursion works because expectation is linear for additive costs. It does **not** automatically justify moving expectation through a maximum:

$$
\max\{\mathbb E[X],\mathbb E[Y]\}
\le \mathbb E[\max\{X,Y\}].
$$

Therefore, deterministic minimax formulas cannot simply be reused with expected costs without considering the stochastic aggregation problem.

### 2.2.4 Markov chains and controlled Markov processes

A discrete-time **Markov chain** has the memoryless transition property: conditional on the present state, the distribution of the next state does not depend on earlier states. The probabilities $P_{ij}$ form a transition matrix with rows summing to one.

For the source's healthy/infected model,

$$
P=\begin{pmatrix}1-\alpha&\alpha\\ b&1-b\end{pmatrix}.
$$

Here $b$ represents the recovery-transition parameter called $\beta$ in that example, to distinguish it from an SDP discount factor. A healthy subject becomes infected with probability $\alpha$; an infected subject becomes healthy with probability $b$. The original diagram makes these transitions explicit.

![[99_attachments/course_book/figure_05.png]]

*Figure 5: State transition diagram for infection model.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=79|Course book pp. 77]]. Original visual from the supplied IU course book; not redrawn.

The source's **MDP** is a time-homogeneous infinite-horizon decision model with stochastic transitions and discounted cost, $(\mathcal K,R,P,\beta)$. Fixing a stationary policy $\phi$ removes the decision freedom and produces a Markov chain:

$$
p_{xy}=P(y\mid x,\phi(x)).
$$

An MDP can therefore be viewed as a family of controlled Markov chains, with policy choice determining which chain operates.

The book generally considers discrete state-action spaces, not necessarily finite. It also notes that continuous state/action problems can require calculus or discretization on a grid. The worked cake-eating example supplies a continuous case; the queue example supplies a stochastic MDP.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Support | Set of possible values of a random variable. |
| Conditional probability | Probability of one event given another event has occurred. |
| Dummy action | A zero-cost terminal action used to complete a model representation. |
| Time homogeneity | Transition and cost rules do not change with the stage. |
| Accrual method | Rule combining stage quantities into the performance criterion. |
| Minimax / maximin | Minimize the largest cost / maximize the smallest reward. |
| History | Information recorded from previous states and actions. |
| Markov chain | A stochastic state sequence with memoryless transitions. |
| MDP under a fixed policy | A Markov chain whose transition matrix is induced by the selected actions. |

## 4. Important formulas / algorithms / steps

$$
P(A\mid B)=P(A\cap B)/P(B),\qquad
\mathbb E[X]=\sum_xxP(X=x).
$$

For a fixed policy and additive discounted stochastic costs:

$$
V^\phi(x)=R(x,\phi(x))+\beta\sum_yP(y\mid x,\phi(x))V^\phi(y).
$$

Specify **state, admissible action, cost, transition, lifetime and accrual rule** before optimizing. A fixed MDP policy induces $p_{xy}=P(y\mid x,\phi(x))$.

## 5. Source-book example

The three-coin example has probabilities 1/8, 3/8, 3/8 and 1/8 for zero through three heads. Knowing that the head count is odd restricts the relevant outcomes to one or three heads; the probability of three heads becomes (1/8)/(3/8+1/8)=1/4.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does a random variable's support contain?
> All numerical values the random variable can take.

> [!question]- 2. What are the core SDP model components?
> States, admissible actions, cost/reward and a deterministic or stochastic transition rule.

> [!question]- 3. Why add a dummy action to a terminal state?
> Allow an absorbing zero-cost terminal representation without an empty action set.

> [!question]- 4. How do time homogeneity and finite horizon differ?
> Homogeneity concerns whether model rules change by stage; horizon concerns process lifetime.

> [!question]- 5. Why can a stage index be included in a state?
> Remaining time may affect optimal decisions, so the state must contain that information.

> [!question]- 6. How does minimax cost differ from total cost?
> It minimizes the worst single-stage cost rather than the sum.

> [!question]- 7. What does the maximin fuel example optimize?
> The smallest available-fuel-per-distance margin across missions.

> [!question]- 8. Why is irrelevant history undesirable?
> It can increase computational complexity without improving the ideal decision.

> [!question]- 9. Why does the expected-value recursion suit additive costs?
> Expectation is linear, so expected stage and continuation contributions can be combined.

> [!question]- 10. Can expectation generally be moved through a maximum?
> No; the maximum of expectations generally differs from the expectation of the maximum.

> [!question]- 11. What does fixing an MDP policy produce?
> A Markov chain with policy-induced transition probabilities.

> [!question]- 12. What is the source coin example's probability of three heads given an odd count?
> One quarter.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** A dynamic-programming model must specify its information, admissible decisions, transitions, lifetime and cost aggregation; the Markov property permits state-based recursion, and a fixed MDP policy induces a Markov chain.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **59-78**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=61|Course book pp. 59-78]].
- Source sections: 2.2, 2.2.1 Dynamic Programming Models, 2.2.2 Policies and Actions, 2.2.3 Value Functions, 2.2.4 Markov Decision Processes.
- Printed page + 2 = PDF viewer page for this supplied edition.
