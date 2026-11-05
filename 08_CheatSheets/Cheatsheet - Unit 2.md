# Cheatsheet - Unit 2

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/01_introduction_to_sequential_decision_making|2.1 Introduction to Sequential Decision Making]]

Dynamic programming exploits the fact that optimal continuations can be solved as smaller subproblems, avoiding repeated enumeration of complete decision sequences.

Route distance is the sum of its edge labels. The source graph has $24$ complete routes.

For a route required to pass through G:

$$
D^*(A,K\mid G)=D^*(A,G)+D^*(G,K).
$$

Compare the best routes through G and H, using their independent segment optima. This reduces the source's first enumeration from 24 full routes to 16 shorter segments.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=54|Course book pp. 52-59]]

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/02_dynamic_programming|2.2 Dynamic Programming]]

A dynamic-programming model must specify its information, admissible decisions, transitions, lifetime and cost aggregation; the Markov property permits state-based recursion, and a fixed MDP policy induces a Markov chain.

$$
P(A\mid B)=P(A\cap B)/P(B),\qquad
\mathbb E[X]=\sum_xxP(X=x).
$$

For a fixed policy and additive discounted stochastic costs:

$$
V^\phi(x)=R(x,\phi(x))+\beta\sum_yP(y\mid x,\phi(x))V^\phi(y).
$$

Specify **state, admissible action, cost, transition, lifetime and accrual rule** before optimizing. A fixed MDP policy induces $p_{xy}=P(y\mid x,\phi(x))$.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=61|Course book pp. 59-78]]

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/03_bellmans_equation|2.3 Bellman's Equation]]

Bellman's equation combines a current decision with optimal continuation; backward induction, value iteration and policy iteration solve it in different ways, but large state spaces can still make exact optimization impractical.

$$
V^*(x)=\min_{a\in A_x}\left[R(x,a)+\beta\sum_yP(y\mid x,a)V^*(y)\right].
$$

Backward induction uses known later-stage values. Value iteration uses $V^{n+1}=TV^n$. Policy iteration alternates evaluation and improvement.

Dense sweep complexity: $N_xN_a$ deterministic versus $N_x^2N_a$ stochastic. Stagecoach optimum: 15; treasure-search chronological policy: 3, 4, 5 hours if needed.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=81|Course book pp. 79-100]]

## [[02_unit_2_dynamic_programming_and_markov_decision_processes/04_general_utility_functions|2.4 General Utility Functions]]

Utility incorporates decision-maker valuation and risk attitude; changing the cost-accrual criterion can change the optimal policy even when the underlying routes and transitions remain unchanged.

$$
\Delta u^+=u(w+\Delta w)-u(w),\qquad
\Delta u^-=u(w)-u(w-\Delta w).
$$

Risk-averse: $\Delta u^->\Delta u^+$ in the source comparison; risk-seeking reverses the inequality.

$$
V^*(x)=\min_{a\in A_x}\max\{R(x,a),V^*(q(x,a))\}.
$$

Stagecoach minimax optimum: longest segment 3 on A-C-F-H-I-K.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=102|Course book pp. 100-108]]
