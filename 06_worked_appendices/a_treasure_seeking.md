---
module: DLMAIRIL01 Reinforcement Learning
unit: appendices
chapter: "Appendix A: Treasure Seeking"
note_type: worked_appendix
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=186|Course book pp. 184-187]]"
printed_pages: [184, 187]
pdf_pages: [186, 189]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# Appendix A: Treasure Seeking

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Connect the treasure-search Bellman recurrence to its source program.
- Explain value, policy and reusable action-value arrays.
- Read output by days remaining rather than chronological day.

## 2. Detailed explanation in my own words

### The problem represented by the program

The source program implements the treasure-search problem from Section 2.3: reward 13,000, rental cost 700 per hour, integer rental times from zero through five, and an exponentially distributed search time with mean 13 hours.

With $w$ days remaining and the treasure not yet found, evaluate each rental duration:

$$
Q(w,a)=13000(1-e^{-a/13})-700a+
e^{-a/13}V^*(w-1,0).
$$

Then

$$
V^*(w,0)=\max_{a\in\{0,\ldots,5\}}Q(w,a),\qquad
\phi^*(w,0)\in\arg\max_aQ(w,a).
$$

The probability of continued unsuccessful search is $e^{-a/13}$. Only that event carries a future search value. A found treasure or no remaining days has zero future search value.

### How the implementation stores the recursion

| Source object | Meaning |
|---|---|
| `valueFunction` | The optimal expected return for each remaining-day count. |
| `policyFunction` | The corresponding maximizing rental duration. |
| `valueActionFunction` | Six candidate action values for the current remaining-day count. |
| `valueTemp` | The previous optimal value used as the next iteration's continuation. |
| `nDays` | Number of backward-recursion iterations, set to 500 in the source. |

The six-entry action-value scratch array is reused; the program does not retain a complete separate array for every state-action combination. The growing value and policy lists retain only the best value and its action at each horizon length.

### Outer and inner loops

Start with continuation value zero, corresponding to no remaining search days. The outer loop increases the remaining-day count. The inner loop evaluates the six admissible rental durations.

After all six candidates have been evaluated, append their maximum to `valueFunction` and append the maximizing action index to `policyFunction`. This maximum becomes `valueTemp` for the next outer-loop pass.

The key computational line is exactly the recurrence above; array initialization, loops, storing results and plotting support it. The notes explain the source program rather than reproduce its entire listing.

### Published output

![[99_attachments/course_book/treasure_output_p187.png]]

*Unnumbered course-book illustration, printed p. 187* — [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=189|Course book pp. 187]]. Original visual from the supplied IU course book; not redrawn.

The plots show policy and expected return against **days remaining**, not the chronological date of the vacation. Section 2.3's three-day results are:

| Days remaining | Rental duration | Expected return |
|---|---|---|
| 1 | 5 hours | 650.7 |
| 2 | 4 hours | 1121.5 |
| 3 | 3 hours | 1469.4 |

For a three-day vacation, execute the policy in chronological order: three hours first, four if another day is needed, then five if still unsuccessful.

The longer-horizon source plots show a return plateau and eventual zero-hour decisions. Since zero hours is available, an extra permitted day need not lower the attainable value; do not read the plateau as a proof that a longer available horizon must be harmful.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Backward recursion | Build a solution from smaller remaining horizons. |
| Scratch action-value array | Reusable candidate values for one current state. |
| Value array | Stored optimal expected returns. |
| Policy array | Stored maximizing actions. |
| Remaining-day index | Number of usable search days including the current one. |

## 4. Important formulas / algorithms / steps

$$
Q(w,a)=13000(1-e^{-a/13})-700a+e^{-a/13}V^*(w-1,0).
$$

Evaluate six actions, store their maximum and its action, then reuse that maximum as the next iteration's continuation.

## 5. Source-book example

The program's third remaining-day calculation gives a three-hour initial rental and expected return 1469.4. Its stored first, second and third entries refer to one, two and three days remaining; the chronological decisions are read in reverse remaining-day order.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does valueTemp contain before a new recursion step?
> The optimal value for one fewer remaining search day.

> [!question]- 2. Why is the continuation multiplied by exp(-a/13)?
> Future searching is needed only when the treasure is not found.

> [!question]- 3. Why are six candidate values sufficient at each step?
> There are six possible integer rental durations from zero to five hours.

> [!question]- 4. What does the policy list store?
> The action attaining the best value at each remaining-day count.

> [!question]- 5. How many iterations does the source program specify?
> Five hundred.

> [!question]- 6. What does the horizontal axis of the output mean?
> Days remaining for search, not chronological vacation day.

> [!question]- 7. What is the three-day chronological policy?
> Rent for three, then four, then five hours if search is still needed.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** The source treasure program implements backward induction using a six-entry action-value workspace and growing optimal-value/policy arrays, with output indexed by days remaining.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **184-187**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=186|Course book pp. 184-187]].
- Source sections: Appendix A, Introduction, A.1 Python Implementation, A.2 Output.
- Printed page + 2 = PDF viewer page for this supplied edition.
