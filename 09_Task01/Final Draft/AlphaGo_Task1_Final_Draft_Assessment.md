# Assessment of the Final Draft: "Learning and Search in AlphaGo and AlphaGo Zero"

| Item | Detail |
|---|---|
| Assessed file | `Final Draft/AlphaGO_Task1_Final_Draft.docx`, rendered with Word: 19 pp. in total |
| Page layout | Title page (unnumbered); II–III front matter; **main text pp. 1–14**; references p. 15; Appendix A p. 16 |
| Content size | ≈ 5,260 words of prose (Introduction 595 ≈ 11 %, Conclusion 431 ≈ 8 %); 1 figure, 2 tables, 7 equations; 10 references |
| Verification | **Every number and locator checked against the original PDFs**, including the *Nature* 2017 journal version, which was obtained this time. Only Rosin (2011) remains behind a paywall. |
| Out of scope | Title-page placeholders |

---

## 1 Verdict: how close you are

**You are at the goal level in content and formalities.** All three v7 blockers are fixed:
- **Pagination:** Roman numerals, then Arabic restarting at 1, and a real ToC field with correct page numbers.
- **Fig. 1:** inserted.
- **AI declaration:** present and referenced in the text.

In addition, the Silver et al. (2017) citations were moved to journal pages plus named Methods sections. This was the cleanest possible fix, and I verified every one of them.

| Criterion (weight) | v1 | v5 | v6 | v7 | **Final** | Remaining deductions |
|---|---:|---:|---:|---:|---:|---|
| Introduction (10 %) | 60 | 85 | 88 | 90 | **88** | The new first sentence cites the course book (see 2.1). |
| Structure (15 %) | 65 | 80 | 80 | 80 | **86** | Pagination, ToC and figure fixed. Conclusion slightly short (8 %). |
| Reasoning (40 %) | 60 | 80 | 84 | 88 | **91** | Several new precision points (see 1.1). Residual: 78 % of citations go to DeepMind's own papers. |
| Conclusion (15 %) | 50 | 85 | 85 | 90 | **88** | Clear limitations and recommendation; ≈ 60 words below 10 %. |
| Language/form (10 %) | 70 | 72 | 77 | 80 | **80** | Precise; long sentences (maximum 53 words), uniform paragraph pattern. |
| Formalities (10 %) | 75 | 65 | 75 | 65 | **85** | Mixed quote styles; inconsistent locator separators; course-book citation without a reference entry. |
| **Weighted indicative score** | **≈ 62 %** | **≈ 79 %** | **≈ 82 %** | **≈ 84 %** | **≈ 88 %** | |

These are my own indicative scores, not an official IU grade. **≈ 88 % is a solid 1.7, at the boundary to 1.3.** The quick fixes in Section 4, P1 (≈ 1 hour), should lift it to ≈ 90 % (1.3). A 1.0 additionally needs an unmistakably personal voice and leaner sentences.

**This rating assumes that the AI declaration and the figure attribution are accurate** (Section 3). If they are not, the content grade is irrelevant.

### 1.1 New strengths in the final draft (all verified)

| Addition | Where | Verified in |
|---|---|---|
| The match policy (192 filters, one orientation) reaches **55.4 %**; the 57.0 % figure belongs to the 256-filter, eight-symmetry ensemble | 3.1 ¶2 | Silver et al. (2016), Extended Data Table 3 ✓ |
| KGS: 29.4 M positions, 28.4 M train / 1 M test; rollout policy trained on ≈ 8 M Tygem positions | 3.1 ¶3, Tab. 1 | Methods "Policy network: classification", "Rollout policy" ✓ |
| REINFORCE baseline (zero at first, value network in the second pass) | 3.2 ¶2 | Methods "Policy network: reinforcement learning" ✓ |
| Pachi at 100,000 sims (direct policy test) vs 400,000 sims (tournament) | 3.2 ¶3 | p. 485; Extended Data Table 6 ✓ |
| Value-data generation: SL prefix → one random legal move → RL continuation; one sample per game | 3.3 ¶2 | Methods "Value network: regression" ✓ |
| "15,000× less computation" correctly limited to a single evaluation, not a whole search | 3.3 ¶3 | p. 486, Fig. 2b ✓ |
| Ablations, scalability and the win-rate cross-table | 3.4 ¶3–4 | Extended Data Tables 7, 8, 9 ✓ |
| Architecture test at 5 s/move: Elo can reflect prediction quality **and** affordable search | 5.2 ¶1 | Silver et al. (2017), Fig. 4 legend, p. 357 ✓ |
| SL comparator: 60.4 % KGS test vs 54.3 % GoKifu validation | 5.2 ¶2 | Extended Data Table 1 ✓ |
| (v + 1)/2 as win probability | 4.1 ¶3 | Correct derivation from ±1 coding |

These distinctions are exactly what separates a 1.3 paper from a 2.0 paper: they show that you read the Methods and Extended Data, not just the abstracts.

---

## 2 Issues still found

### 2.1 Course book cited as a source (formal; fix)

The Introduction now opens with *"The module's treatment of Monte Carlo tree search in Unit 5.2 (course book, pp. 175–176) provides the starting point …"*.

- The *Zitierleitfaden* (p. 2) states: *"Skripte, Vorlesungsfolien, Webinars, etc. sind als Quellen bei wissenschaftlichen Arbeiten nicht zu verwenden"* (course scripts, lecture slides and webinars may not be used as sources).
- The citation also has no entry in the reference list, which breaks the rule that every in-text citation must appear there.
- It is also a weak opening sentence for a Master's paper.

**Fix:** delete the first sentence of ¶1. If you want to show that the course was the starting point (the task sheet asks for this), add one sentence **without a citation** to the method paragraph (¶4), e.g. *"The course introduction to model-based reinforcement learning and MCTS served as the conceptual starting point; the analysis itself relies on the scientific publications listed below."*

### 2.2 Small consistency issues (formal)

| Issue | Example | Fix |
|---|---|---|
| Mixed quotation marks around section labels | `"Problem setting"`, `“Domain knowledge”`, `‘Neural network architecture’` (Tab. 1 source line) | Use one style, e.g. curly double “…”, throughout |
| Inconsistent separator between page and section | "(Silver et al., 2016, p. 486, Methods section …)" vs "(Silver et al., 2017, p. 354; Methods section …)" | Use a comma for the same work: "p. 354, Methods section …"; keep the semicolon only between different works |
| Rosin (2011), Section 2 | 2.2 ¶2, 4.3 ¶2 | Still unverified (paywall). Check via the IU library, or cite the whole work: "(Rosin, 2011)" |
| Document properties: title "… — primary-source verification draft" | *File → Info* | Change the title to the paper title |
| Leftover style names `CaptionReview` and `BibliographyReview` | styles | Harmless; optionally rename to Word's *Caption* and *Bibliography* |

### 2.3 Wording and readability (for 1.3 → 1.0)

- **Longest sentences** (> 40 words): 3.1 ¶3 (rollout policy), 3.4 ¶3 (ablations), 5.2 ¶1 and Conclusion ¶5. Split each into two sentences.
- **Paragraph length** grew to 91 words on average (v7: 82) and is very uniform. Let 3–4 paragraphs be short (40–50 words), especially transitions such as the closing paragraphs of 3.4 and 4.3.
- **Ending pattern:** 47 of 58 paragraphs still end with a parenthetical citation. Let 4–5 paragraphs end with your own conclusion and put the citation earlier in the paragraph.
- **5.2 lost its "what each comparison holds constant" paragraph** from v7. The information is spread over 5.2 ¶1–4 and the method paragraph, so it is not wrong, but the explicit side-by-side statement was a strong marker of critical evaluation. Consider restoring it in 2–3 sentences before "Taken together …".
- **Conclusion** (431 words ≈ 8 %): add ≈ 60 words, e.g. one sentence answering each of the three sub-questions explicitly ("(1) … (2) … (3) …"). This also closes the loop with the research questions in the Introduction.

### 2.4 References: complete and correct

| Check | Result |
|---|---|
| In-text ↔ reference list | ✓ 10/10 (the course-book mention is the only orphan; see 2.1) |
| Silver et al. (2017) | ✓ Journal entry is now clean; journal pages 354–358 and Methods sections all verified against the *Nature* version |
| Silver et al. (2016) incl. Methods, Extended Data Tables 2, 3, 6, 7, 8, 9 and Fig. 2b | ✓ all verified |
| Browne pp. 1, 5–6, 27; Kocsis §2; Williams §§4–5; He pp. 771–772; Sutton & Barto pp. 58–59, 159–161, 166–168, 447–450; Tian pp. 6244, 6246–6247; Wang pp. 35655–35658 | ✓ |
| Rosin §2 | ? paywalled |
| Format (italics, 1.5 spacing, hanging indent, DOI) | ✓ |
| Breadth | 10 sources; lean but adequate. **Do not add more now.** |

---

## 3 Integrity: figure and AI declaration

### 3.1 Fig. 1

- The image file is new (different file hash from v5–v7), but its **layout, colours, wording and footnote ("Separate policies, value model and rollout") are identical to the diagram that v6 declared as "rendered with AI-assisted Python (OpenAI)"**.
- The caption now reads "Own representation based on …" with no AI note.
- The *Zitierleitfaden* (§2.2.5, pp. 21, 25) requires that AI involvement in creating a figure be stated in the source line under the figure (prompt plus tool).
- **If** the image was again produced or re-rendered with AI help, the source line must say so, e.g. *"Source: Own representation based on Silver et al. (2016, pp. 484–486) and Silver et al. (2017, pp. 354–355); diagram code created with the assistance of ChatGPT (OpenAI, 2026)."* The tool then also belongs in the reference list. **If** you redrew it yourself (e.g. in PowerPoint), the current caption is correct.
- Content check of the diagram: correct. Arrows and labels match the papers. One optional refinement: AlphaGo Zero's evaluator/gating step (Methods, "Evaluator") is not shown; this is acceptable for a schematic.

### 3.2 Appendix A

The current text says ChatGPT was used to clarify concepts, review drafts, suggest revisions and improve wording. Check it against what actually happened over the eight versions:

| What happened (documented in earlier versions and files) | Covered by the current Appendix A? |
|---|---|
| Concept clarification, draft review, revision suggestions, wording | ✓ |
| **Initial drafting of text** (v6's own appendix said "substantial assistance … including initial drafting") | ✗ not mentioned |
| **Diagram creation** (v6 caption: "AI-assisted Python diagram code") | ✗ not mentioned |
| **GitHub Copilot** (draft assessments, source and locator verification, the v2 rework) | ✗ not mentioned |
| Document preparation with scripts (python-docx traces in v5–v7) | ✗ not mentioned |

**If you rewrote the text yourself since v6, the narrower wording can be true. Then add one sentence saying so** (see 3.3). If substantial passages still originate from AI drafts, the current appendix **understates** the use. An understated declaration is a bigger risk than an honest one, because the earlier versions and your chat histories document the process.

### 3.3 Suggested wording (adapt to what is true)

> **Appendix A: Statement on the use of AI-assisted tools**
>
> I used AI-based tools as learning and writing aids while preparing this assignment.
>
> - **ChatGPT (OpenAI, [model], [period]):** clarifying reinforcement-learning concepts relevant to AlphaGo and AlphaGo Zero; [generating initial text drafts and structural proposals, which I subsequently revised and rewrote]; suggesting revisions and improving clarity and precision of wording; [assistance with the code used to render Fig. 1].
> - **GitHub Copilot ([period]):** reviewing successive drafts against the IU assessment criteria and checking citations and page references against the original publications.
>
> I selected the sources, verified every factual statement and page reference against the original publications, and revised the final text myself. AI tools were not used as a source of information. I take full responsibility for the analysis, wording and references.

Keep only the bracketed parts that apply. **Read the IU guideline on AI-supported systems (myCampus) before finalising.** If it prescribes a template, use that. If it does not permit a use listed above, the remedy is to rework the affected parts yourself, not to omit them from the declaration.

---

## 4 Final to-do list

### P1: Before submission (≈ 1 h)

- [ ] Delete the course-book citation in Intro ¶1; add the uncited "starting point" sentence to ¶4 (2.1).
- [ ] Bring the Fig. 1 source line and Appendix A in line with what actually happened (3.1–3.3).
- [ ] Use one quotation style for section labels; use a comma between page and section for the same work.
- [ ] Verify Rosin §2 via the IU library, or drop "Section 2".
- [ ] Correct the document title in *File → Info → Properties*.
- [ ] Update all fields (Ctrl+A, F9) after the edits, re-check that the main text is still ≤ 15 pp., and export the PDF.

### P2: Optional polish (1.3 → 1.0)

- [ ] Split the four longest sentences; vary paragraph length; end 4–5 paragraphs with your own inference.
- [ ] Restore a 2–3-sentence "what each comparison holds constant" summary in 5.2.
- [ ] Conclusion: one explicit sentence per sub-question (+ ≈ 60 words).

### P3: Personal readiness

- [ ] Explain aloud, without notes: why the SL policy is the better search prior; how MCTS can overrule the network (your PUCT example); why Zero's gain cannot be attributed to removing human data alone; what "without human knowledge" does not mean.

---

## 5 Bottom line

| | v1 | v5 | v6 | v7 | **Final** | Final after P1 |
|---|---:|---:|---:|---:|---:|---:|
| Indicative score | ≈ 62 % | ≈ 79 % | ≈ 82 % | ≈ 84 % | **≈ 88 %** | ≈ 90 % |
| Indicative grade | 3.0 | 2.0/2.3 | 2.0 | 2.0/1.7 | **1.7** | **1.3** |

The paper is now scientifically accurate, fully referenced and formally sound. You have reached the 1.0–1.7 target range. The last hour of work is mostly about removing the course-book citation and making sure the AI declaration and figure attribution say exactly what happened.
