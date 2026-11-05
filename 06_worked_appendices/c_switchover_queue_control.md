---
module: DLMAIRIL01 Reinforcement Learning
unit: appendices
chapter: "Appendix C: Switchover Queue Control"
note_type: worked_appendix
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=203|Course book pp. 201-213]]"
printed_pages: [201, 213]
pdf_pages: [203, 215]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# Appendix C: Switchover Queue Control

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Represent two queues and one switchable server as a cost-minimizing MDP.
- Calculate next-event probabilities and expected stage lengths.
- Explain the source's arrays, value updates, policy matrices and convergence output.

## 2. Detailed explanation in my own words

### Queueing notation in the source

Customers arrive, wait if service is unavailable, receive service and leave. The book introduces Kendall notation $A/B/m$, extended to $A/B/m/K/M$:

| Component | Meaning |
|---|---|
| $A$ | Arrival waiting-time distribution. |
| $B$ | Service-time distribution. |
| $m$ | Number of servers. |
| $K$ | System capacity. |
| $M$ in the final position | Finite customer population, if specified. |

For distribution symbols, **M** means exponential/memoryless, **D** deterministic and **G** general. Context therefore distinguishes distribution symbol M from the optional population parameter.

### Two finite queues share one server

Each queue has arrival rate $\lambda$ and capacity $K$. One server works at service rate $\mu$ and can stay at its current queue or switch. An arrival to a full queue is lost.

![[99_attachments/course_book/figure_28.png]]

*Figure 28: Schematic representation of the switchover queue model. Capacity is K = 7 (this includes customers both waiting and being served). The state illustrated is x = W1, W2, U = 5, 3, 1 . Queue 1 has 1 customer in service, and 4 more waiting in queue, so W1 = 5. and U = 1. Queue 2 has 3 customers waiting in queue and none being served, so W2 = 3. The arrival rates λ and serve rate μ are indicated. These are in units of customer per time unit.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=204|Course book pp. 202]]. Original visual from the supplied IU course book; not redrawn.

The conceptual state is $(W_1,W_2,U)$: both customer counts, including any customer being served, and the current server location. Decisions occur at arrival or service-completion epochs.

Actions can be represented either as **Stay/Switch** or as the **next queue number** 1/2. Queue number 1 is Stay when the server is already at queue 1, but Switch when it is at queue 2.

### Cost per decision stage

$$
R(x,a)=B\,I(a=\text{Switch})+
\tau(x,a)g(W_1,W_2).
$$

The first component charges for switching. The second accumulates queue-dependent cost over the expected time $\tau$ until the next event. In this appendix, $R$ is a **cost to minimize**, despite the letter also being used for rewards elsewhere.

### Exponential waiting times and the next event

The source uses three properties: exponential waiting times are memoryless; the minimum of independent exponential times is exponential with rate equal to their rate sum; and each event wins the race with probability equal to its rate divided by that sum.

![[99_attachments/course_book/figure_29.png]]

*Figure 29: Examples of state transition diagrams for the switchover queue model. Unless otherwise specified, W1 and W2 are assumed to be strictly between 0 and K.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=207|Course book pp. 205]]. Original visual from the supplied IU course book; not redrawn.

For nonempty queues below capacity, staying at queue 1 allows three next events:

| Event | Successor | Probability |
|---|---|---|
| Service at queue 1 completes | $(W_1-1,W_2,1)$ | $\mu/(2\lambda+\mu)$ |
| Queue 1 arrival | $(W_1+1,W_2,1)$ | $\lambda/(2\lambda+\mu)$ |
| Queue 2 arrival | $(W_1,W_2+1,1)$ | $\lambda/(2\lambda+\mu)$ |

Their expected stage length is

$$
\tau(x,\text{Stay})=\frac1{2\lambda+\mu}.
$$

Switching changes the server component and the queue from which a service completion removes a customer. At boundaries, the possible **state-changing** events differ: an empty served queue cannot complete service, and a full queue cannot accept another customer.

For example, staying at an empty queue leaves only the two arrivals, each with probability one-half when both can accept customers. If one queue is full, arrivals to it no longer change the state; use the rates of the remaining effective transitions. The original diagrams show these boundary distinctions.

### Program representation and parameters

The source program uses `K = 10`, $\mu=1$, $\lambda=0.9$, $\beta=0.99$, and 1,000 value sweeps. Its illustrated queue diagram has capacity 7; the program uses 10.

There are $2(K+1)^2$ states. Value, old-value and policy arrays have shape `(2, K+1, K+1)`, indexed by **server position first**, then the two queue lengths. The separately constructed state vector remains `[W1,W2,U]`; its server component is mapped to the first array index using `U-1`.

`makeTransitionList` supplies the effective successor states, their probabilities, stage length and cost for each state-action pair. The program's cost specialization is

$$
R(x,a)=I(a=\text{Switch})+
3\tau(x,a)(W_1^2+W_2^2).
$$

### Value iteration

For each state and each next-queue action, compute

$$
Q_n(x,a)=R(x,a)+
\beta\sum_yP(y\mid x,a)V_n(y).
$$

Store the smaller of the two candidates as the next state value, and store its next-queue number as the policy. A two-entry action-value workspace is reused across states. Old and new value arrays keep one complete sweep's continuation estimates separate from its updates.

The trace records one value entry after every sweep to show approach toward a limit. Here discount is per decision stage in the displayed Bellman update; expected real stage duration separately affects the running cost.

### Read the original policy matrices

![[99_attachments/course_book/queue_policy_p211.png]]

*Original switchover-queue policy output, printed p. 211* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=213|Course book pp. 211]]. Original visual from the supplied IU course book; not redrawn.

![[99_attachments/course_book/queue_policy_p212.png]]

*Original switchover-queue policy output, printed p. 212* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=214|Course book pp. 212]]. Original visual from the supplied IU course book; not redrawn.

The output has one matrix for each starting server position. Rows and columns represent queue counts; entries 1/2 give the next queue to serve, **not** numerical cost and not a universal Stay/Switch code.

The source highlights that the policy need not switch monotonically as the other queue grows. Finite capacity limits further queue growth and can change the optimal decision. Read an entry with its row, column and current server position.

**Source caution:** p. 212's explanatory inequality signs and ranges conflict with the matrices. The original matrices are retained; this summary does not invent corrected threshold ranges.

### Convergence output

![[99_attachments/course_book/figure_30.png]]

*Figure 30: Trace array of the value iteration algorithm for the switchover queue problem.* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=215|Course book pp. 213]]. Original visual from the supplied IU course book; not redrawn.

The trace shows stabilization over the programmed sweeps. It displays a selected state-value component, not the entire policy or a measurement of the user's review progress.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Decision epoch | An event time when the server can choose Stay or Switch. |
| Queue state | Both customer counts and the server location. |
| Exponential race | The first event among independent exponential waiting times. |
| Expected stage length | Mean time until the next effective state transition. |
| Switching cost | A cost charged for changing the server's queue. |
| Next-queue policy | A stored queue number interpreted relative to current location. |
| Capacity boundary | A full queue cannot accept another customer. |

## 4. Important formulas / algorithms / steps

$$
\tau=\frac1{2\lambda+\mu},\quad
p_{\text{arrival},i}=\frac{\lambda}{2\lambda+\mu},\quad
p_{\text{service}}=\frac{\mu}{2\lambda+\mu}
$$

for the interior three-event case.

$$
V_{n+1}(x)=\min_a\left[R(x,a)+\beta\sum_yP(y\mid x,a)V_n(y)\right].
$$

Arrays use `(U-1,W1,W2)`; policy entries identify the next served queue.

## 5. Source-book example

The original queue diagram has state (5,3,1): five customers at queue 1 including the one being served, three at queue 2 and the server at queue 1. The implemented K=10 model evaluates both possible next-queue choices for every array entry and prints one policy matrix per current server position.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What information is needed in the switchover state?
> Both queue customer counts and the server's current queue.

> [!question]- 2. What do the two cost components represent?
> A switching charge and queue-dependent cost over the expected stage duration.

> [!question]- 3. What is the interior total event rate?
> Two times the arrival rate plus the service rate.

> [!question]- 4. How is each next-event probability calculated?
> Divide that event's rate by the total effective event rate.

> [!question]- 5. Why do boundary transition probabilities change?
> Empty queues cannot complete service and full queues cannot accept customers.

> [!question]- 6. How many states are represented at capacity K?
> Two times (K+1) squared.

> [!question]- 7. What is the value array's index order?
> Server position, queue 1 count, queue 2 count.

> [!question]- 8. What does a policy matrix entry mean?
> The next queue number to serve, interpreted relative to the current server position.

> [!question]- 9. What does makeTransitionList provide?
> Successors, transition probabilities, expected stage length and cost.

> [!question]- 10. Does a policy entry equal the value function?
> No; it selects a queue, while the value gives expected accumulated cost.

> [!question]- 11. What does the convergence plot display?
> A selected value-function entry over the programmed sweeps.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** The queue example builds a cost-minimizing MDP at event epochs, derives transitions from exponential races, and uses value iteration to produce next-queue policy matrices with boundary-dependent, potentially nonmonotonic decisions.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **201-213**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=203|Course book pp. 201-213]].
- Source sections: Appendix C, Queueing Introduction, Switchover Queue Control, C.2.1 State Transition Diagrams, C.3 Program Implementation, Policy Output, Convergence Trace.
- Printed page + 2 = PDF viewer page for this supplied edition.
