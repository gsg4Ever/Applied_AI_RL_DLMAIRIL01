---
module: DLMAIRIL01 Reinforcement Learning
unit: 4
chapter: "4.3 Experience Replay"
note_type: chapter
official_course_book_pages: "[[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=155|Course book pp. 153-154]]"
printed_pages: [153, 154]
pdf_pages: [155, 156]
status: not_reviewed
confidence_1_to_5:
last_reviewed:
next_review:
exam_relevance:
tags: [review, DLMAIRIL01]
---

# 4.3 Experience Replay

> [!info] Source boundary
> A paraphrased study summary of the supplied course book, version 001-2024-0328. Questions and review aids are derived from this same content, not official examination questions. Source-book examples are retained; no external teaching topics are added.

## 1. Learning focus

- Define an experience tuple and replay buffer.
- Explain why randomized replay makes training more stable.
- Distinguish uniform sampling from TD-error-based prioritization.

## 2. Detailed explanation in my own words

### Store experiences instead of using each only once

An interaction produces an **experience tuple** $(s,a,r,s')$. A replay buffer retains such tuples. Training samples from that collection rather than only the newest observation.

This supplies a larger training sample and allows multiple uses of informative data. The buffer grows as the agent gathers experiences; it does not require a separately labelled supervised dataset.

### Why random sampling matters

Consecutive interactions can be strongly correlated. The source's controller example changes a character's posture only slightly, so successive images are almost identical. Training on that recent local sequence makes the network repeatedly process nearly the same situation.

Randomly sampling across stored experiences reduces the correlation among the training examples presented together. It moves the training data closer to the independent-sample assumption used in neural-network training and improves stability.

Uniform replay treats stored tuples as equally likely. It does not distinguish a rare useful event from an event that is frequent or already well predicted.

### Prioritized experience replay

The source proposes favoring experiences with high expected learning progress. A large TD discrepancy indicates that the prediction is still far from the observed reward-plus-continuation target, so the example can be more informative.

For priorities $p_i$, source Eq. (4.18) defines

$$
P(i)=\frac{p_i^\alpha}{\sum_kp_k^\alpha}.
$$

Here $\alpha$ controls prioritization strength, and a small $\epsilon$ prevents a zero priority from excluding an experience completely.

**Source notation caution:** the printed preceding line writes $p_i=\Delta_i+\epsilon$, while $\Delta$ was defined earlier as a signed TD error. Sampling priorities must be nonnegative. The source therefore leaves a sign/magnitude ambiguity in that line. This summary preserves the printed expression as a source issue rather than silently presenting an external variant as book content.

The conceptual distinction remains clear: uniform replay reuses experiences equally; prioritized replay favors the ones with greater expected remaining learning value.

## 3. Key terms

| Term | Meaning in this section |
|---|---|
| Experience tuple | State, action, observed reward and successor state. |
| Replay buffer | Stored interaction data reused for training. |
| Temporal correlation | Nearby sequential observations resemble or depend on each other. |
| Uniform replay | Equal sampling treatment of stored experiences. |
| Prioritized replay | Prefer experiences expected to produce more learning progress. |
| Priority exponent | Controls how strongly priorities affect sampling. |

## 4. Important formulas / algorithms / steps

Experience: $(s,a,r,s')$. Store tuples and randomly sample them for training.

$$
P(i)=p_i^\alpha/\sum_kp_k^\alpha.
$$

Random replay reduces sequential correlations; prioritized replay uses remaining TD prediction discrepancy as its motivation. See the note's source sign/magnitude caution before using the printed priority expression.

## 5. Source-book example

In the source game-controller example, changing one body part by a tiny amount gives nearly identical successive frames. Training from randomly selected older and newer tuples avoids treating this highly correlated immediate sequence as the whole training sample.

## 6. Remarks while learning

Record your own explanation, uncertainties, and review observations here.

## 7. Open questions

- [ ] Record any unresolved question after attempting the active recall below.

## 8. Active recall

Answer before expanding the source-derived answer.

> [!question]- 1. What does an experience tuple contain?
> A state, an action, the reward and the successor state.

> [!question]- 2. Why store a replay buffer?
> To reuse interaction data and train on more than the latest experience.

> [!question]- 3. Why randomly sample from replay?
> To reduce correlation among consecutive training experiences.

> [!question]- 4. What does uniform replay ignore?
> Differences in rarity, informativeness and remaining learning value.

> [!question]- 5. What motivates prioritized replay in the book?
> Experiences with large remaining prediction discrepancies offer more learning progress.

> [!question]- 6. What does the priority exponent control?
> The strength of the prioritization in the sampling probabilities.

## 9. Exam checklist

- [ ] I can explain the section without looking at the notes.
- [ ] I can define its key terms and distinguish the related methods.
- [ ] I can reconstruct the relevant formulas or algorithm steps.
- [ ] I can explain the course-book example and its original visuals.
- [ ] I have answered the active-recall questions and recorded my confidence.

**Compact answer to practise:** Experience replay stores and reuses state-action-reward-successor tuples; randomized sampling reduces temporal correlations, and prioritized replay concentrates training on experiences expected to improve predictions most.

## 10. Source reference

- IU, *Reinforcement Learning*, DLMAIRIL01, version **001-2024-0328**, printed pp. **153-154**.
- [[Course Book/001-2024-0328_DLMAIRIL01_Course_Book.pdf#page=155|Course book pp. 153-154]].
- Source sections: 4.3, Replay Buffer, Random Sampling and Correlation, Prioritized Replay.
- Printed page + 2 = PDF viewer page for this supplied edition.
