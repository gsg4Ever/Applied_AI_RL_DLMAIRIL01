# Flashcards - Unit 2

#flashcards/DLMAIRIL01/unit2

Source-derived cards. No imported review history; all cards start unscheduled.

## 2.1 Introduction to Sequential Decision Making

Source: [[02_unit_2_dynamic_programming_and_markov_decision_processes/01_introduction_to_sequential_decision_making]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=54|Course book pp. 52-59]].

What is a sequential decision process?::A process in which a sequence of actions influences accrued cost or reward.
What is constructive enumeration?::List every candidate solution explicitly and evaluate it.
How many complete routes are in the source stagecoach map?::Twenty-four, from three times two times two times two times one choices.
Why does brute-force enumeration scale poorly?::The number of complete action sequences multiplies across stages.
Why can the continuation from G be optimized independently?::The remaining route distances depend on the current town, not on the route previously taken.
What does the constraint in D*(A,K given G) mean?::The candidate route must pass through town G.
What is the first decomposition's route-count saving?::Six plus six plus two plus two shorter segments instead of twenty-four full routes.

## 2.2 Dynamic Programming

Source: [[02_unit_2_dynamic_programming_and_markov_decision_processes/02_dynamic_programming]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=61|Course book pp. 59-78]].

What does a random variable's support contain?::All numerical values the random variable can take.
What are the core SDP model components?::States, admissible actions, cost/reward and a deterministic or stochastic transition rule.
Why add a dummy action to a terminal state?::Allow an absorbing zero-cost terminal representation without an empty action set.
How do time homogeneity and finite horizon differ?::Homogeneity concerns whether model rules change by stage; horizon concerns process lifetime.
Why can a stage index be included in a state?::Remaining time may affect optimal decisions, so the state must contain that information.
How does minimax cost differ from total cost?::It minimizes the worst single-stage cost rather than the sum.
What does the maximin fuel example optimize?::The smallest available-fuel-per-distance margin across missions.
Why is irrelevant history undesirable?::It can increase computational complexity without improving the ideal decision.
Why does the expected-value recursion suit additive costs?::Expectation is linear, so expected stage and continuation contributions can be combined.
Can expectation generally be moved through a maximum?::No; the maximum of expectations generally differs from the expectation of the maximum.
What does fixing an MDP policy produce?::A Markov chain with policy-induced transition probabilities.
What is the source coin example's probability of three heads given an odd count?::One quarter.

## 2.3 Bellman's Equation

Source: [[02_unit_2_dynamic_programming_and_markov_decision_processes/03_bellmans_equation]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=81|Course book pp. 79-100]].

What does Bellman's principle optimize?::A first admissible action followed by optimal continuation from the next state.
Why begin backward induction at the terminal stage?::The terminal continuation value is known, so preceding values can be calculated.
What is the optimal stagecoach distance?::Fifteen, attained by three source routes.
Why does the one-time-sale modification break the original memoryless model?::Future sale reward depends on whether a sale already occurred, not just the current town.
What must the treasure-search state contain?::Days remaining and whether the treasure has been found.
What is the source's three-day treasure policy?::Hire three, then four, then five hours on chronological days if still searching.
What expected value does the source report for three remaining days?::1469.4 dollars.
What is a Bellman fixed point?::A value function V that satisfies V equals T applied to V.
How does policy evaluation differ from policy optimization?::Evaluation fixes the actions of one policy; optimization compares admissible actions.
Why can optimal policies be nonunique?::Different actions can attain the same minimum cost or maximum return.
What are dense deterministic and stochastic sweep complexities?::Nx times Na and Nx squared times Na, respectively.
When can sparse transitions reduce stochastic complexity?::When each action reaches only a few possible successors.
What causes the source ten-queue example to become infeasible?::Twenty-one possible lengths in each of ten queues create about 1.67 times 10^13 configurations.

## 2.4 General Utility Functions

Source: [[02_unit_2_dynamic_programming_and_markov_decision_processes/04_general_utility_functions]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=102|Course book pp. 100-108]].

Why might expected monetary payoff be insufficient?::Decision makers can have different valuations and tolerances for losses.
What does a utility curve's slope represent?::Marginal utility of an additional unit.
How does a thirsty customer's marginal utility change?::It falls after the first drink because additional drinks have less value.
Which utility shapes represent risk-aversion, neutrality and seeking?::Strictly concave, linear and strictly convex respectively.
How does concavity compare equal-sized gains and losses?::The utility loss is larger than the corresponding utility gain.
What does the minimax stagecoach criterion minimize?::The greatest distance of any single segment along the route.
Which source route is minimax-optimal?::A-C-F-H-I-K, with a longest segment of three.
Why can total-distance-optimal routes differ under minimax?::Their equal sums can hide different largest segment distances.
