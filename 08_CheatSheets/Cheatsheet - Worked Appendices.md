# Cheatsheet - Worked Appendices

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[06_worked_appendices/a_treasure_seeking|Appendix A: Treasure Seeking]]

The source treasure program implements backward induction using a six-entry action-value workspace and growing optimal-value/policy arrays, with output indexed by days remaining.

$$
Q(w,a)=13000(1-e^{-a/13})-700a+e^{-a/13}V^*(w-1,0).
$$

Evaluate six actions, store their maximum and its action, then reuse that maximum as the next iteration's continuation.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=186|Course book pp. 184-187]]

## [[06_worked_appendices/b_towers_of_hanoi|Appendix B: Towers of Hanoi]]

The Hanoi implementation converts legal disk moves into a deterministic shortest-path problem, enumerates configurations by integer indices, and follows the converged successor policy to reconstruct the published minimum-move path.

$3^N$ states; six possible peg-to-peg move types, restricted by admissibility.

$$
V^*(x)=\min_{a\in A_x}[1+V^*(q(x,a))],\qquad V^*(x_\Delta)=0.
$$

Enumerate with `incState`, access by `pHash`, reconstruct through `policyFunction` and `stateMap`. Three-disk output: seven moves, eight states.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=189|Course book pp. 187-201]]

## [[06_worked_appendices/c_switchover_queue_control|Appendix C: Switchover Queue Control]]

The queue example builds a cost-minimizing MDP at event epochs, derives transitions from exponential races, and uses value iteration to produce next-queue policy matrices with boundary-dependent, potentially nonmonotonic decisions.

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

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=203|Course book pp. 201-213]]

## [[06_worked_appendices/d_cake_eating|Appendix D: Cake Eating]]

Cake eating is a continuous-state/action finite-horizon allocation problem; backward induction balances marginal utilities and yields the source's geometric-denominator consumption rule for logarithmic utility.

$$
V(w,k)=\max_{0\le c\le w}[u(c)+\beta V(w-c,k-1)].
$$

$$
u'(c)=\beta V_w'(w-c,k-1),\qquad
c_k=\frac{w_k}{\sum_{i=0}^{k-1}\beta^i}
$$

for the source's logarithmic utility. With one stage left, consume all remaining wealth.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=215|Course book pp. 213-217]]

## [[06_worked_appendices/e_q_learning_treasure_seeking|Appendix E: Q Learning Treasure Seeking]]

The source treasure Q-learner learns from uniformly random simulated episodes, uses terminal-aware targets and reciprocal visit counts, and recovers the exact policy while its published value estimates remain approximate.

Nonterminal target: $r+\max_bQ(w-1,b)$. Terminal target: $r$.

$$
Q(w,a)\leftarrow Q(w,a)+
\frac{\text{target}-Q(w,a)}{n(w,a)}.
$$

Source vector `[5,4,3]` means one/two/three days remaining; chronological policy is three/four/five hours if needed.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=219|Course book pp. 217-224]]
