# Assessment of Draft Version 6: "Learning and Search in AlphaGo and AlphaGo Zero"

| Item | Detail |
|---|---|
| Assessed file | `6th Draft/AlphaGo_Task1_Draft6_Review.docx`, rendered with Word: 19 pp. in total; main text pp. 1–14; ≈ 4,630 words of prose (Introduction 478, Conclusion 370); 11 reference entries (10 scholarly + 1 AI tool); 1 figure, 2 tables, 7 equations (now native Word equations); Appendix A |
| Benchmarks | Same as for v5: IU *Guidelines Written Assignment*, *Guidelines for Structuring and Formatting Academic Papers* (01/10/2025), *Zitierleitfaden* (01/10/2026), task sheet DLMAIRIL01 Task 1 |
| Verification performed | All 10 scholarly sources checked page by page against downloaded PDFs. Exception: Rosin (2011), where only the Springer landing page was accessible (paywall). |
| Out of scope | Title page |

---

## 1 Verdict

**v6 is better than v5, and the remaining gap to 1.7 is now almost entirely formal.** Most citation errors are fixed and the missing origin sources were added. The computed PUCT example replaces the invented one, and the equations are now proper Word equations. What still costs marks: layout (empty space, empty paragraphs, static ToC, no hyphenation), one wrong locator (Williams §6, which was **my** error in the v5 assessment), and a few small consistency issues.

**There is one new strategic risk.** Appendix A now openly declares "substantial assistance … including initial drafting". This is honest, but whether it is permitted depends entirely on the IU AI policy, which I do not have (Section 5).

| Criterion (weight) | v1 | v5 | **v6** | Remaining deductions in v6 |
|---|---:|---:|---:|---|
| Introduction (10 %) | 60 | 85 | **88** | Method paragraph now names the selection logic; it could name the databases or search terms (one clause). |
| Structure (15 %) | 65 | 80 | **80** | p. 4 (Fig. 1) still ⅔ empty; p. 3 bottom ≈ 40 % empty; 7 empty paragraphs (v5: 4) create gaps on p. 9; Conclusion at 8 % is slightly below ≈ 10 %. |
| Reasoning (40 %) | 60 | 80 | **84** | DeepMind citation share still 77 %; the Williams locator is wrong; three locators slightly too broad. |
| Conclusion (15 %) | 50 | 85 | **85** | Strong. One concrete recommendation for applied RL would round it off. |
| Language/form (10 %) | 70 | 72 | **77** | Equations fixed. Still: "accepted-manuscript pp." repeated 36×; c_puct built from a Chinese tone-mark character (U+A700) that may render oddly; uniform, dense paragraph style. |
| Formalities (10 %) | 75 | 65 | **75** | References and captions fixed. Still: hyphenation off, static ToC, Appendix A never referenced in the text, spaced en dashes, mixed quote styles. |
| **Weighted indicative score** | **≈ 62 %** | **≈ 79 %** | **≈ 82 %** | |

These are my own indicative scores, not an official IU grade. **≈ 82 % is a 2.0 on common German 100-point conversions.** The fixes in Section 6, P1–P2, are a few hours of mechanical work and should bring it to ≈ 85–87 % (1.7). 1.3 additionally needs the explanatory edits (P3) and a clear answer on AI permissibility (P4).

---

## 2 Status of the v5 rework tasks

✓ done · ◐ partly done · ✗ open

| v5 task | Status in v6 | Note |
|---|---|---|
| C1 Silver (2017) pagination | ◐ | Solved with a note inside the reference entry plus "accepted-manuscript pp." at all 36 citations. This is transparent and acceptable under IU's own-rule clause (*Zitierleitfaden*, p. 2), but clumsy. A single footnote at the first citation and plain "p." afterwards reads better. |
| C2 Browne pp. 1, 27 | ✓ | Verified. |
| C3 Transfer paragraph | ✓ | Rewritten to the model-error argument with Sutton & Barto §8.3. Locator is slightly too broad: §8.3 is **pp. 166–168** (§8.4 starts on p. 168), not 166–170. |
| C4 Lee "several months", p. 8 | ✓ | |
| C5 Williams locator | ✗ | Now "Section 6". **That was my mistake in the v5 assessment.** §6 is "REINFORCE with multiparameter distributions". The REINFORCE principle is **§4**, and **episodic** REINFORCE is **§5** (verified in the paper). Use "(Williams, 1992, Sections 4–5)". |
| C6 Kocsis & Szepesvári | ✓ | "Section 2" is a stable label; §2 is "The UCT algorithm". |
| C7 He et al. + Rosin | ✓ | He et al. pp. 770–773 is acceptable; residual learning itself is §3, pp. 771–772. Rosin "Section 2" could not be checked behind the paywall; verify via the IU library. |
| C8 Sutton & Barto §16.6 | ✓ | Used in the method paragraph and 4.2. "pp. 445–450" covers the end of the AlphaGo part; the AlphaGo Zero part is **pp. 447–450**, which is the tighter locator for the claim in 4.2. |
| C9 OpenAI and Sutton & Barto entries | ✓ | |
| C10 Quote style | ✗ | Still mixed: 6 straight `"…"`, 11 curly `“…”`, 11 single `‘…’` around section labels. |
| F1 Hyphenation | ✗ | Still off (no `autoHyphenation` in the settings). |
| F2 Reference list format | ✓ | 11 pt, 1.5 spacing, left-aligned, hanging indent. |
| F3 Captions | ✓ | "Fig. 1" / "Tab. 1" without a period, 10 pt; table body 9 pt. |
| F4 Equations | ✓ | 7 native equations render correctly. In 4.3 the running text uses "cₚᵤ꜀ₜ", built from Unicode subscript letters and U+A700 (a Chinese tone mark). Use an inline Word equation or a normal subscript. |
| F5 ToC as a field | ◐ | Order is now correct, but it is still typed text without a TOC field or right-aligned page numbers. |
| F6 Abbreviations | ✓ | CNN and MSE added, DNN and UCB1 removed, alphabetical. |
| F7 Empty space and empty paragraphs | ✗ | Worse: 7 empty paragraphs; p. 4 still ⅔ empty; p. 3 ≈ 40 % empty. |
| F8 Dashes, "programme", Fig./Figure | ✗ | "486– 487" and "23– 24" are still spaced; "programme" for software (5.2); running text says "Figure 1" / "Table 1/2" while captions say "Fig." / "Tab." |
| F9 AI note out of References | ✓ | Now Appendix A, listed in the ToC. **But IU requires every appendix to be referenced at least once in the text** (formatting guidelines, p. 6). It currently is not. |
| R1 Invented example | ✓ | Replaced by a computed PUCT example. Arithmetic verified: √100 = 10; U(A) = 0.171, U(B) = 0.049; Q + U = 0.371 vs 0.449, so B is selected. Clearly labelled as assumed inputs. |
| R2 One sentence per experiment on what is held constant | ✓ | 5.2 ¶5 now does exactly this. This is the strongest single improvement in v6. |
| R3 Plain-language loop | ✓ | 4.2 ¶2 opens with the simple logic. |
| R4 Sentence and paragraph variety | ✗ | Unchanged: 59 paragraphs, mean 78 words, SD 14; maximum sentence 46 words. |
| R5 Method paragraph | ✓ | Selection logic stated; databases and search terms would complete it. |
| A1 Rebuild in your own Word file | ✗ | Metadata still `python-docx` / "generated by python-docx" / 2013-12-23. |
| A2 Own wording | ? | Cannot be assessed from the document; style indicators are unchanged. |
| A3 Accurate AI declaration | ✓ | Appendix A is now candid (see Section 5). |

---

## 3 Source and locator verification

### 3.1 Unchanged and still correct

All Silver et al. (2016) numbers and locators (pp. 484–488, Methods section labels), all Silver et al. (2017) manuscript locators, Tian et al. (pp. 6244, 6246–6247) and Wang et al. (pp. 35655–35658) were re-checked and are correct (details in the v5 assessment, Section 3).

### 3.2 New or changed locators in v6

| Citation | Verified | Status | Fix |
|---|---|---|---|
| Browne et al., 2012, pp. 1, 27 | MCTS success in computer Go (p. 1); top programs at "good amateur" level (p. 27) | ✓ | — |
| Kocsis & Szepesvári, 2006, Section 2 | §2 "The UCT algorithm" | ✓ | — |
| Rosin, 2011, Section 2 (2×) | Paywalled; only the landing page (vol. 61, pp. 203–230) was confirmed | ? | Check §2 via the IU library. |
| Williams, 1992, Section 6 | §6 = multiparameter distributions | ✗ | Sections 4–5 |
| He et al., 2016, pp. 770–773 | §3 "Deep residual learning", pp. 771–772 | ◐ | pp. 771–772 is more precise. |
| Sutton & Barto, 2018, Section 16.6 | §16.6 "Mastering the Game of Go", pp. 441–450 | ✓ | — |
| Sutton & Barto, 2018, pp. 445–450 | AlphaGo Zero subsection starts p. 447 | ◐ | pp. 447–450 |
| Sutton & Barto, 2018, Section 8.3, pp. 166–170 | §8.3 pp. 166–168 | ◐ | pp. 166–168 |
| Silver et al., 2017, accepted-manuscript p. 8 (Lee "several months") | p. 8 | ✓ | — |

Sutton & Barto page numbers were taken from the open 2020 PDF of the 2nd edition. Check once against the print edition.

### 3.3 Uncited paragraphs

Three paragraphs contain no citation:
- the Chapter 2 signpost, which is fine;
- the 3.4 ¶2 bridge, which is fine because it only forward-references Section 4.3;
- the computed PUCT illustration, which is fine because it is your own calculation. It could cite Eq. 7's source (Silver et al., 2017, manuscript p. 26) for the rule being applied.

Every source-dependent paragraph is cited.

---

## 4 Reference list: completeness

| Check | Result |
|---|---|
| Every in-text source in the list, and vice versa | ✓ (11/11) |
| DOI or URL present | ✓; Sutton & Barto is cited as the print edition without URL, which is consistent |
| Format (11 pt, 1.5, left-aligned, 1.27 cm hanging indent, alphabetical) | ✓ |
| Silver (2017) entry | ◐ The free-text note in parentheses is not APA style. Better: keep the plain journal entry and move the explanation into a footnote at the first in-text citation. |
| OpenAI entry | ✓ format; whether it belongs in the list depends on the AI policy (IU §2.3.7 requires it for AI-generated images, and Fig. 1 is AI-assisted). |
| Breadth | 10 scholarly sources, 4 after 2017 counting Sutton & Barto (2018), 5 independent of DeepMind. Citation share: Silver et al. 63 of 82 citations = **77 %** (v5: 82 %). Lean but defensible for a 15-page paper because every source now carries a specific function. |
| Missing | Nothing essential. Optional for independence: Anthony et al. (2017), Expert Iteration, cited once in 4.2 next to Sutton & Barto. Do not add more. |

---

## 5 AI-generation and integrity signals

### 5.1 File level (unchanged from v5)

| Signal | v6 |
|---|---|
| `dc:creator = python-docx`, `description = generated by python-docx`, created/modified 2013-12-23 | **still present** |
| `Application = Microsoft Macintosh Word`, Words = 0, Pages = 1 | still present |
| Custom styles `CaptionReview`, `BibliographyReview`, `Equation` | still present |
| No TOC field | still present |

### 5.2 Text level

| Indicator | v5 | v6 |
|---|---|---|
| Paragraph length mean / SD | 77 / 13 | 78 / 14 |
| Paragraphs ending with a citation | 48/58 (83 %) | 47/59 (80 %) |
| Contrastive hedges ("rather than", "not a/an…", "does not") | 34 | 38 |
| Colons and semicolons | 67 | 71 |
| Meta-labels such as "(not a reported AlphaGo position)" and "These are assumed inputs …" | yes | yes, now justified because they flag your own calculation |
| Unicode workaround "cₚᵤ꜀ₜ" (tone-mark character as subscript c) | — | **new**; typical of generated text, since no human types U+A700 |

The style profile is essentially unchanged. Turnitin's AI indicator will very likely flag large parts of the text.

### 5.3 The declaration (main strategic risk)

Appendix A states that the manuscript was developed "with substantial assistance from ChatGPT … including initial drafting, structure, language revision, diagram scripting and document preparation".

- **Honesty:** this matches the metadata and style evidence, and it is far better than the understated v5 note.
- **Permissibility:** the *Zitierleitfaden* (pp. 4–5) only says that AI used as a tool for translation or linguistic smoothing need not be cited, and it refers everything else to the separate IU *Richtlinie für die Nutzung KI-gestützter Systeme* on myCampus. That guideline decides whether AI-drafted content is acceptable in an examination that must be "independent preparation" (task sheet, p. 3: "Independent preparation is part of the examination work"). **If the guideline does not allow AI drafting, a candid declaration does not cure it; the work could be assessed as not independently produced.**
- **Action:** read the guideline now. If you are unsure, ask the tutor or the examination office *before* submission. Then either (a) keep the declaration because the use is permitted, or (b) rewrite the text substantively yourself, so that AI use shrinks to what is permitted (typically language checking and diagram tooling), and update Appendix A truthfully.
- In both cases, reference Appendix A once in the text (e.g. at the end of the method paragraph: "AI assistance is documented in Appendix A").

---

## 6 Remaining rework tasks

### P1: Citations (≈ 30 min)

- [ ] **C5** Williams in 3.2 ¶2: "Section 6" → **"Sections 4–5"**, i.e. "Williams (1992, Sections 4–5) establishes …".
- [ ] **C11** Tighten locators: Sutton & Barto §8.3 → pp. 166–168; 4.2 → pp. 447–450; He et al. → pp. 771–772.
- [ ] **C12** Check Rosin (2011) §2 via the IU library.
- [ ] **C1b** Optional: replace the 36× "accepted-manuscript pp." with one footnote at the first Silver (2017) citation, and remove the note from the reference entry.
- [ ] **C10** One quote style for section labels; "Figure 1" → "Fig. 1", "Table 1/2" → "Tab. 1/2" in the running text.

### P2: Formalities and layout (≈ 1–2 h)

- [ ] **F1** Automatic hyphenation on.
- [ ] **F5** Replace the typed ToC with Word's TOC field (right-aligned page numbers, dot leaders).
- [ ] **F7** Delete the 7 empty paragraphs. Fix p. 3–4: let Fig. 1 float to the top of p. 4 and let 3.1 start below it, or place Fig. 1 after the first paragraph of 2.2 so that text fills p. 3.
- [ ] **F8** "486–487", "23–24" without spaces; "programme" → "program" (5.2 ¶4).
- [ ] **F11** Reference Appendix A once in the text.
- [ ] **F12** Replace "cₚᵤ꜀ₜ" in 4.3 with an inline equation or a normal subscript.
- [ ] **F13** Conclusion: add ≈ 60–80 words (to ≈ 10 %), e.g. one concrete recommendation for applied RL (where a reliable simulator exists, use search-generated targets; where not, validate under model error, linked back to 5.3).

### P3: Readability (selective, no extra pages)

- [ ] **R4** Split the 5–6 longest sentences (> 35 words). Vary paragraph length, with some short 2–3-sentence paragraphs at transitions. Let some paragraphs end with your own inference rather than with a citation.
- [ ] **R6** 4.1 ¶2: the residual formula appears twice (inline and as Eq. 5); keep only Eq. 5.

### P4: Authorship and AI policy (decisive; non-delegable)

- [ ] **A0** Read the IU AI guideline and, if in doubt, ask the tutor or examination office (5.3).
- [ ] **A1** Rebuild the file in your own Word document; *File → Info → Inspect Document* removes the python-docx properties.
- [ ] **A2** Rewrite in your own words, section by section, against the verified source pages.
- [ ] **A3** Update Appendix A so that it matches the final process exactly.

---

## 7 Self-test (unchanged; still recommended)

Explain each point aloud without notes:

1. Why AlphaGo Fan uses different models for different functions, and why the stronger RL policy is the weaker search prior.
2. How MCTS changes an individual decision. Use your own PUCT example from 4.3 and the 3,055 vs 5,185 Elo comparison.
3. Why Zero's gain cannot be attributed to removing human data alone (the three comparison types in 5.2 ¶5).
4. What "without human knowledge" does and does not mean.

---

## 8 Bottom line

| | v1 | v5 | v6 | v6 after P1–P2 |
|---|---:|---:|---:|---:|
| Indicative score | ≈ 62 % | ≈ 79 % | **≈ 82 %** | ≈ 85–87 % |
| Indicative grade | 3.0 | 2.0/2.3 | **2.0** | **1.7** |

The scientific content is ready. The remaining deductions are formal and mechanical, plus one wrong locator that originated in my own v5 advice. **The decisive open question is no longer quality but permissibility:** the AI declaration in Appendix A must be consistent with the IU AI guideline before you submit.
