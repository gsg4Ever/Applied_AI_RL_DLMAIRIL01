# Cheatsheet - Unit 3

Condensed from the linked course-book notes only. This is a review aid, not additional course content.

## [[03_unit_3_bandit_problems/01_one_armed_bandit_problem|3.1 The One-Armed Bandit Problem]]

Bandit decisions must earn reward and gather information simultaneously; regret measures the reward sacrificed relative to the best-known-mean choice, and insufficient continued sampling can lock a policy into an inferior source.

$$
Q\leftarrow Q+\gamma(r-Q),\qquad
\Delta^\Phi=R^*-R^\Phi.
$$

Known-mean one-bandit choice: use the bandit if $\mu>\delta$; otherwise use the fixed alternative.

A selected arm updates its count and mean; unselected arms do not gain observations. A fixed initial sample followed by permanent commitment can preserve a wrong ranking indefinitely.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=113|Course book pp. 111-118]]

## [[03_unit_3_bandit_problems/02_multiple_arm_bandit_problem|3.2 The Multiple Arm Bandit Problem]]

Effective bandit policies combine current reward estimates with continuing exploration; epsilon-greedy and softmax force exploration, gradient methods adjust relative preferences, and uncertainty indices such as UCB1 favor both promising and under-sampled arms.

Softmax:

$$
\pi_j(k)=\frac{e^{Q_{k,j-1}/\tau}}{\sum_\ell e^{Q_{\ell,j-1}/\tau}}.
$$

Vanishing epsilon-greedy exploration requires the source condition $\sum_j\epsilon_j=\infty$.

UCB1:

$$
I_{k,j}=Q_{k,j-1}+\sqrt{\frac{2\log(j-1)}{n_{k,j-1}}}.
$$

Gradient preferences use reward minus a baseline; uncertainty indices combine estimated reward with an exploration bonus.

[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=120|Course book pp. 118-134]]
