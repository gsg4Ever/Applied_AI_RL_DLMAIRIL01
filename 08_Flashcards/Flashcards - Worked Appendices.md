# Flashcards - Worked Appendices

#flashcards/DLMAIRIL01/appendices

Source-derived cards. No imported review history; all cards start unscheduled.

## Appendix A: Treasure Seeking

Source: [[06_worked_appendices/a_treasure_seeking]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=186|Course book pp. 184-187]].

What does valueTemp contain before a new recursion step?::The optimal value for one fewer remaining search day.
Why is the continuation multiplied by exp(-a/13)?::Future searching is needed only when the treasure is not found.
Why are six candidate values sufficient at each step?::There are six possible integer rental durations from zero to five hours.
What does the policy list store?::The action attaining the best value at each remaining-day count.
How many iterations does the source program specify?::Five hundred.
What does the horizontal axis of the output mean?::Days remaining for search, not chronological vacation day.
What is the three-day chronological policy?::Rent for three, then four, then five hours if search is still needed.

## Appendix B: Towers of Hanoi

Source: [[06_worked_appendices/b_towers_of_hanoi]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=189|Course book pp. 187-201]].

Why is disk-to-peg membership sufficient to define a state?::The move rules already determine the size ordering within every peg.
How many states are represented for N disks?::Three to the power N.
What makes a potential peg-to-peg move illegal?::An empty source or placing a larger disk on a smaller top disk.
What objective does the one-unit move cost encode?::The minimum number of moves to reach the terminal configuration.
What does incState do?::Enumerate vectors with a three-symbol odometer.
What does pHash do?::Convert a state vector to its canonical integer index.
Why keep old and new value arrays?::Evaluate one sweep against a fixed preceding value function.
What does the stored policy contain?::The integer index of the minimizing successor state.
Why does the output contain one more state than moves?::A path includes its initial state as well as every successor.
What result does the source report for three disks?::Seven moves and eight states.

## Appendix C: Switchover Queue Control

Source: [[06_worked_appendices/c_switchover_queue_control]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=203|Course book pp. 201-213]].

What information is needed in the switchover state?::Both queue customer counts and the server's current queue.
What do the two cost components represent?::A switching charge and queue-dependent cost over the expected stage duration.
What is the interior total event rate?::Two times the arrival rate plus the service rate.
How is each next-event probability calculated?::Divide that event's rate by the total effective event rate.
Why do boundary transition probabilities change?::Empty queues cannot complete service and full queues cannot accept customers.
How many states are represented at capacity K?::Two times (K+1) squared.
What is the value array's index order?::Server position, queue 1 count, queue 2 count.
What does a policy matrix entry mean?::The next queue number to serve, interpreted relative to the current server position.
What does makeTransitionList provide?::Successors, transition probabilities, expected stage length and cost.
Does a policy entry equal the value function?::No; it selects a queue, while the value gives expected accumulated cost.
What does the convergence plot display?::A selected value-function entry over the programmed sweeps.

## Appendix D: Cake Eating

Source: [[06_worked_appendices/d_cake_eating]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=215|Course book pp. 213-217]].

Why must the cake-eating state include stages remaining?::The same wealth must be allocated differently depending on the remaining consumption opportunities.
What does concave utility imply about marginal utility?::It decreases as consumption increases.
How does wealth change after consumption?::The next wealth equals current wealth minus the consumed amount.
What does the interior first-order condition balance?::Current marginal utility against discounted marginal continuation value.
Why consume all wealth in the final stage?::Utility is increasing and there is no later opportunity to use retained wealth.
What is the two-stage current log-utility allocation?::Available wealth divided by one plus beta.
What is the general source allocation denominator?::One plus beta plus successive powers through beta to the k-minus-one power.
Why use calculus rather than enumerate every action?::Consumption is continuous rather than a finite list of choices.

## Appendix E: Q Learning Treasure Seeking

Source: [[06_worked_appendices/e_q_learning_treasure_seeking]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=219|Course book pp. 217-224]].

What behavior does the source agent use?::Uniformly random rental durations from zero through five hours.
Does finding the treasure early reduce the scheduled rental bill?::No; the full chosen duration is paid.
What determines a successful simulated search?::An exponential search-time sample no greater than the scheduled duration.
When does an episode terminate?::When treasure is found or the final available search day is exhausted.
What future value is used in a terminal update?::None; the target is the immediate reward.
What is the source learning rate for a visited pair?::One divided by that pair's incremented visit count.
What does Qfactor row w-minus-one represent?::A search state with w days remaining.
What does the source variable named target actually store?::The TD error, including subtraction of the current Q-value.
How should policy vector [5,4,3] be read?::Actions for one, two and three remaining days, giving chronological three, four and five.
Why can the learned policy be correct with inaccurate values?::Correct action ranking can occur before all values are numerically precise.
