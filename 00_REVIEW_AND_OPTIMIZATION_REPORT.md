# Source fidelity and notation review

## What was preserved

Five teaching units with their 18 official numbered sections, all source subsection topics, worked appendices A-E, the source's examples and named methods, and all original numbered visuals. Study aids restate these notes and do not add course topics.

## What was intentionally not copied

Whole paragraphs and full Python listings are not reproduced verbatim. The appendices explain program organization, data structures, update logic and published output, with direct PDF references. Bibliographic front/back matter remains accessible in the PDF. Separately required readings are outside the supplied-book summary.

## Source printing and notation cautions

- **Symbols change by unit.** Early units use $\beta$ for discounting and $\gamma$ for step size; later units use $\gamma$ for discounting and $\alpha$ for step size. In the actor-critic update, $\beta$ is a second learning rate.
- **Minimum/maximum versus argmin/argmax.** A value function returns a numerical cost or return; a policy returns an action. Some source lines interchange these symbols or indices. Notes follow the meaning established by the surrounding derivation and keep the distinction explicit.
- **On-policy wording differs within the book.** Unit 1 explains the distinction through learning versus online performance; Unit 4 more precisely contrasts the action actually chosen by the current policy (SARSA) with a maximizing Q-learning target. Read the relevant section together with its equations.
- **TD($\lambda$).** The source's Eq. (1.23) writes powers of $\lambda$ without an additional discount factor in those weights. The notes identify this as the book's displayed episodic form and do not silently insert a different textbook convention.
- **Prioritized replay.** Printed p. 154 writes priority $p_i=\Delta_i+\epsilon$, although the earlier TD error is signed. This leaves a sign/magnitude ambiguity because sampling priorities must be nonnegative. The notes expose the source issue rather than silently substituting a formula from outside the book.
- **Hanoi state vector.** The illustrative vector and prose on p. 191 disagree. The original figure remains intact; the notes explain the source's explicit disk-to-peg encoding.
- **Bandit simulation legends.** The text specifies the second arm's mean as 30, while the original simulation images label Treatment 2's mean as 20. Images are unchanged and this disagreement is noted beside them.
- **Treasure-search narrative.** The book reports eventual no-search days and a reward plateau for its 500-day recursion. Choosing the available zero-hour action can retain the preceding value, so this is not evidence that having an additional available day must reduce the optimum. Notes describe the published output without adding a new result.
- **Appendix C output.** The queue-policy prose on p. 212 has inconsistent inequality signs and ranges compared with the actual matrices. Original matrix images are preserved; notes do not manufacture corrected thresholds from that prose.
- **Appendix E day labels.** The final printed policy labels are inconsistent with the text's remaining-day convention. The displayed program vector `[5, 4, 3]` is indexed by **one, two, three days remaining**; chronological rental decisions are **3, 4, 5** hours if search is still required.
- **Utility expansion.** The cake-eating derivation includes typographical slips in intermediate constants and stage indices. The notes use the source's final allocation rule, retain the derivative argument, and omit irrelevant expanded constants.

These cautions address how to read the supplied source; they are not a supplement of outside reinforcement-learning topics. Source uncertainty is left visible rather than asserted as a new fact.

## Study structure

The reference vault's unit folders, overview notes, YAML review properties, ten-part chapter structure, source links, flashcards, review workflow and cheat sheets are retained. No previous review dates, confidence scores or exam-priority predictions are imported.

Printable HTML review sheets mirror the reference's visual study format. Their formulas are rendered with local KaTeX, using bundled fonts, without loading external content in the browser.
