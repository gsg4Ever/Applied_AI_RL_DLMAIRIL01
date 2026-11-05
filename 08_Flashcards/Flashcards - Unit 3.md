# Flashcards - Unit 3

#flashcards/DLMAIRIL01/unit3

Source-derived cards. No imported review history; all cards start unscheduled.

## 3.1 The One-Armed Bandit Problem

Source: [[03_unit_3_bandit_problems/01_one_armed_bandit_problem]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=113|Course book pp. 111-118]].

What is a one-armed bandit in this book?::A source that produces a random reward with an unknown mean when selected.
If the bandit mean is known, when should it beat the fixed alternative?::When its mean reward exceeds the fixed reward.
What does a stage discount sequence define?::How successive rewards are weighted in the accumulated objective.
What is the incremental reward-estimate update?::Q becomes Q plus learning rate times observed reward minus Q.
Which count determines a running mean's step size?::The number of observations from that particular reward source.
What is regret?::The best achievable expected total reward minus the policy's expected total reward.
Why can fixed initial sampling followed by permanent commitment fail?::A finite-sample ranking error can persist because the rejected source is never sampled again.
What remains wrong with updating only the chosen bandit?::An initially underestimated bandit that is no longer chosen still receives no corrective data.

## 3.2 The Multiple Arm Bandit Problem

Source: [[03_unit_3_bandit_problems/02_multiple_arm_bandit_problem]]; [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=120|Course book pp. 118-134]].

Why does the source's greedy three-arm policy sometimes choose arm 2 forever?::Arm 3 is initially underestimated and then receives no new samples to correct its ranking.
What does forced exploration prevent?::Permanent neglect of alternatives based on inaccurate initial estimates.
What is the cost of a constant epsilon in the long run?::It keeps selecting inferior exploratory arms even after accurate identification.
What condition does the book give for vanishing exploration?::Epsilon tends to zero but its sum over stages remains infinite.
How does softmax temperature affect selection?::High temperature approaches uniform exploration; low temperature approaches greedy selection.
What does a gradient bandit policy learn?::Relative action preferences adjusted using reward minus a baseline.
Why does adding a common preference constant leave softmax unchanged?::The common exponential factor cancels in numerator and denominator.
What are the two components of an uncertainty-based index?::Current reward estimate and an uncertainty or exploration bonus.
How does a one-sided confidence bound differ from a two-sided interval?::It assigns coverage to one relevant tail rather than splitting it between two tails.
What is the source's 95% confidence interval for mean 34.6 and standard deviation 5.7 with n=5?::Approximately 27.52 to 41.68.
What is the corresponding one-sided 95% upper bound?::Approximately 40.0.
What does UCB1 add to the current reward estimate?::The square root of two log total prior pulls divided by that arm's prior pull count.
How do the two counts in UCB1 differ?::The numerator uses overall time; the denominator uses observations of the particular arm.
Does UCB1's displayed bonus use a sample variance or t critical value?::No; the source contrasts it with the normal-theory confidence index.
