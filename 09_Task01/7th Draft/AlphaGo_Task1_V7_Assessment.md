# Assessment of Draft Version 7: "Learning and Search in AlphaGo and AlphaGo Zero"

| Item | Detail |
|---|---|
| Assessed file | `7th Draft/AlphaGo_Task1_Draft7_Substantive_Revision.docx`, rendered with Word: 17 pp. in total; main text (Introduction to Conclusion) 13 pp.; ≈ 4,820 words of prose (Introduction 501 ≈ 10 %, Conclusion 418 ≈ 9 %); 10 references; Fig. 1 = **placeholder**; 2 tables; 7 native equations; **no appendix** |
| Benchmarks | Same as for v5/v6: IU *Guidelines Written Assignment*, *Guidelines for Structuring and Formatting Academic Papers* (01/10/2025), *Zitierleitfaden* (01/10/2026), task sheet DLMAIRIL01 Task 1 |
| Verification | All changed locators re-checked against the source PDFs. Unchanged numbers were already verified for v5/v6. |
| Out of scope | Title-page placeholders |

---

## 1 Where you stand

**Content: ready for 1.3–1.7. Submission readiness: not yet, because of three formal and integrity blockers.**

The substantive revision worked. The explanations the external reviewer asked for are now in the text:
- why the stronger RL policy is the worse search prior (3.2 ¶4);
- how search overturns a prior without a gradient update (3.4 ¶2);
- the limits of "search as policy improvement" (4.2 ¶3);
- what each experiment holds constant (Intro ¶4 and 5.2 ¶5–6);
- a three-condition transfer argument (5.3 ¶5);
- a concrete, conditional recommendation for applied RL (Conclusion ¶5).

All locators flagged in v6 are fixed.

| Criterion (weight) | v1 | v5 | v6 | **v7** | Remaining deductions |
|---|---:|---:|---:|---:|---|
| Introduction (10 %) | 60 | 85 | 88 | **90** | Method paragraph now explains the four comparison types, which is excellent. Only the databases and search terms are missing (one clause). |
| Structure (15 %) | 65 | 80 | 80 | **80** | Logic and proportions are now right (≈ 10/81/9). Deductions: Fig. 1 missing, so p. 6 is half empty; the front-matter section break is lost (see 2.1). |
| Reasoning (40 %) | 60 | 80 | 84 | **88** | Evidence-weighted, with qualified claims and verified effect sizes. Residual: 76 % of citations go to the two DeepMind papers; uniform paragraph template. |
| Conclusion (15 %) | 50 | 85 | 85 | **90** | Synthesis, limitations, future research and a recommendation are all present. It could be ≈ 60 words longer to reach a full 10 %. |
| Language/form (10 %) | 70 | 72 | 77 | **80** | Precise and clear. Residual: very uniform rhythm; "accepted-manuscript pp." repeated 36×; "c_PUCT" in running text. |
| Formalities (10 %) | 75 | 65 | 75 | **65** | Hyphenation and empty paragraphs are fixed, but **page numbering is now broken**, the ToC page numbers are wrong, and the figure placeholder and missing AI declaration count here (Section 2). |
| **Weighted indicative score** | **≈ 62 %** | **≈ 79 %** | **≈ 82 %** | **≈ 84 %** | |

These are my own indicative scores, not an official IU grade. **≈ 84 % is at the 2.0/1.7 boundary.** If Fig. 1 were submitted as a placeholder, the score would drop further. **After the P1 fixes below (≈ half a day), ≈ 87–89 %, i.e. a solid 1.7 with 1.3 within reach.** 1.0 requires near-flawless formalities *and* a text that clearly reads as your own.

---

## 2 Main issues that block 1.0–1.7

### 2.1 Page numbering and ToC are broken (new regression, formal)

- The document now has **one section only**. The section break between the front matter and the Introduction was lost.
- Result in the rendered PDF:
  - Contents and lists are numbered **2, 3** in Arabic numerals (required: II, III in Roman numerals);
  - the Introduction starts on **page 4** (required: page 1);
  - References are on page 17.
- The typed ToC still says "1 Introduction 1 … References 15", so **every ToC page number is now wrong**, and a marker sees this on the first page they open.
- **Fix:** insert *Layout → Breaks → Section break (next page)* before "1 Introduction". In the second section, unlink the footer from the previous one and set *Page numbers → Format → Start at 1, Arabic numerals*; keep Roman numerals for section 1. Then replace the typed ToC with *References → Table of contents* (a field) and update it (F9).

### 2.2 Fig. 1 is a placeholder (content and formal)

- The text, the list of figures and 2.2 ¶1 refer to Fig. 1, but the page shows "FIGURE INSERTION POINT …", and p. 6 is about half empty.
- **Fix:** insert your own reconstructed figure. The source line is already correct for an own figure ("Source: Own representation based on …"). Since the figure is now your own and not AI-generated, the OpenAI reference correctly disappeared from the list. **Do not reuse the earlier AI-rendered PNG** (`word/media/image1.png` / `image2.png` are still embedded in the file without being displayed; delete them by re-saving from a clean document).

### 2.3 AI use is no longer declared anywhere (integrity)

- v6 had Appendix A; v7 removed both it and the OpenAI reference. If AI tools were used in preparing this paper (and the earlier versions document that they were), **a paper with no declaration is the highest risk of all versions**. The file itself still shows generation traces:
  - creation date `2013-12-23T23:15:00Z`, the python-docx template default (the "generated by python-docx" description is gone, but this date remains);
  - `Application = Microsoft Macintosh Word`, Words = 0, Pages = 1;
  - custom styles `CaptionReview` and `BibliographyReview`;
  - two hidden PNGs from the AI-generated figure.
- The text profile is unchanged: 59 paragraphs, mean 82 words, SD 15; 48 of 59 paragraphs end with a parenthetical citation. Turnitin's AI indicator will very likely flag it.
- **Fix:** see Section 5 for the appendix wording, and Section 4 for the file clean-up.

### 2.4 Smaller items that still cost points

| Item | Where | Fix |
|---|---|---|
| Mixed quote styles around Methods section labels | 2.1, 2.2, 3.1, 3.4, 4.3, 5.1, Tab. 1 source line | One style throughout, e.g. "…" |
| "Figure 1", "Table 1/2" in running text vs "Fig."/"Tab." in captions | 2.2 ¶1, 3.1 ¶1, 5.1 ¶2 | Use "Fig. 1" / "Tab. 1" consistently |
| "accepted-manuscript pp." 36× | throughout | Optional: one footnote at the first Silver (2017) citation, then plain "p." |
| "c_PUCT" written with an underscore | 4.3 ¶2–3 | Insert as an inline equation (c with subscript puct) |
| Rosin (2011), Section 2 | 2.2, 4.3 | Still unverified (paywalled); check via the IU library |
| Name spelling | title page and file author show "Gülkan Sen"; v6 showed "Gökhan Sen" | Check the spelling of your name |

---

## 3 Remaining requirements check

### 3.1 Task fulfilment (task sheet DLMAIRIL01, Task 1)

| Requirement | Where | Status |
|---|---|---|
| Describe how AlphaGo works | Ch. 2–3 | ✓ |
| Which deep neural networks are used for which task | 3.1, Tab. 1 | ✓ explicit inventory |
| How deep learning was combined with MCTS to achieve the performance | 3.3–3.4 (λ ablation, 494/495, raw vs search) | ✓ mechanism and evidence |
| Compare AlphaGo and AlphaGo Zero | Ch. 4–5, Tab. 2 | ✓ including Lee and Master and an attribution analysis |
| Course book as starting point; own research and citations | Intro ¶4; Sutton & Barto (course literature) | ✓ |

### 3.2 References: correctness and completeness

| Check | Result |
|---|---|
| In-text sources ↔ reference list | ✓ 10/10, no orphans |
| Locators fixed since v6 | ✓ Williams Sections 4–5; He et al. pp. 771–772; Sutton & Barto pp. 166–168 and 447–450 |
| All numbers (Silver 2016/2017, Tian, Wang) | ✓ verified (v5/v6 assessments, Section 3) |
| Formatting (11 pt, 1.5 spacing, left-aligned, 1.27 cm hanging indent, alphabetical, DOI/URL) | ✓ |
| Silver (2017) entry | ◐ The parenthetical note inside the entry is not APA style; a footnote is cleaner. Acceptable as is. |
| Breadth | 10 scholarly sources; 5 independent of DeepMind; 4 after 2017. **Lean but sufficient** for 13 pages because each source has a specific function. Optional single addition for independence: Anthony et al. (2017), Expert Iteration, in 4.2 ¶2. |
| AI tool reference | Correctly removed if Fig. 1 is your own; AI used only as a writing or structuring aid is not cited as a source (*Zitierleitfaden*, pp. 4–5) but is declared (Section 5). |

### 3.3 Description, explanation and argumentation

- **Strengths (keep):** the four-type evidence hierarchy (Intro ¶4 and 5.2 ¶5–6); the qualified policy-improvement claim (4.2 ¶3); the computed PUCT example; the transfer conditions with an engineering recommendation.
- **Residual weaknesses (optional, for 1.3 → 1.0):**
  1. Every paragraph follows the same pattern (claim → detail → qualification → citation). Let 4–5 paragraphs end with **your own inference** instead of a citation, and merge or split some so that paragraph lengths vary (some at 40 words, some at 120).
  2. Split the 4–5 sentences longer than 35 words (maximum 46).
  3. 2.1 ¶3 and 2.2 ¶3 make the same learning-vs-planning point. Merge them and use the space for one sentence on why Go was hard for MCTS alone (Browne et al., 2012, p. 27).

---

## 4 Prioritised to-do list

### P1: Blockers (≈ half a day)

- [ ] **F14** Restore the section break: Roman numerals for the front matter, Arabic numbering restarting at 1 with the Introduction (2.1).
- [ ] **F9** Replace the typed ToC with a Word TOC field and update it.
- [ ] **F15** Insert your own Fig. 1 and check every arrow and label against Silver et al. (2016, pp. 484–486) and Silver et al. (2017, manuscript pp. 3–6).
- [ ] **A3** Add the AI declaration appendix (Section 5), reference it once in the text, and list it in the ToC.
- [ ] **A1** Rebuild the file cleanly: create a new blank Word document from your own template, paste with *Keep text only* or copy styles, and run *File → Info → Check for issues → Inspect document → Document properties and personal information → Remove all*. Then re-enter yourself as author. This removes the 2013 template dates and the hidden PNGs.

### P2: Polish (≈ 1 h)

- [ ] **C10** One quote style; "Fig."/"Tab." in running text.
- [ ] **F12** "c_PUCT" as an inline equation.
- [ ] **C12** Verify Rosin (2011) §2 via the IU library.
- [ ] **C1b** Optional: footnote for the manuscript pagination.

### P3: Own voice (decisive for 1.0–1.3 and for the declaration to be true)

- [ ] **A2** Rewrite the text section by section in your own words and check each claim against the source pages. Use the self-test from the v5/v6 assessments (four concepts, explained aloud without notes).

---

## 5 Hint for the AI appendix

### 5.1 Rules that apply

- The *Zitierleitfaden* (pp. 4–5) distinguishes three uses of AI:
  - AI as a **tool** (translation, linguistic smoothing) does **not** need to be cited as a source;
  - AI as an **information source** is **not citable**;
  - AI as an **object of study** is cited.
- What is *permitted* and *how it must be declared* is defined in the separate IU *Richtlinie für die Nutzung KI-gestützter Systeme* on myCampus. I do not have that document. Secondary descriptions say IU welcomes responsible use for research, idea generation, structuring and translation, but not for having the work written. **Read the official version before you finalise the wording**; if it prescribes a form or template, use that instead of the examples below.
- An appendix must be labelled "Appendix A", listed in the ToC, and **referred to at least once in the text** (formatting guidelines, p. 6). With only one appendix, no separate list of appendices is needed. Page numbering continues in Arabic numerals.
- **The declaration must describe what actually happened.** An understated declaration is a greater risk than an honest one. Keep your chat histories in case you are asked about them.

### 5.2 Where to reference it

At the end of the method paragraph (Intro ¶4), add for example:

> "The use of AI-based tools during the preparation of this paper is documented in Appendix A."

### 5.3 Suggested structure

**Appendix A: Declaration on the use of AI-based tools**

| Tool (provider, version) | Phase and purpose | Extent | Author's own contribution and verification |
|---|---|---|---|
| e.g. ChatGPT (OpenAI, model …), period … | e.g. feedback on structure, review of drafts against the IU criteria | e.g. suggestions, which were accepted, modified or rejected by the author | e.g. all claims checked against the original sources; final wording by the author |
| e.g. GitHub Copilot (GitHub/Microsoft) | e.g. assessment of drafts, formatting checks, locator verification | … | … |
| e.g. DeepL / Microsoft Editor | e.g. language and spelling check | … | … |

Then add a short closing statement (2–4 sentences).

### 5.4 Example wordings (choose and adapt the variant that is true)

**Variant 1: AI used for feedback, structure and language (the author wrote the text):**

> "AI-based tools were used in a supporting role during the preparation of this paper. ChatGPT (OpenAI, [model], [period]) and GitHub Copilot ([period]) were used to obtain feedback on drafts against the IU assessment criteria, to suggest structural improvements and to check formatting and citation consistency. [DeepL/Microsoft Editor] was used for language checking. All research, source selection, interpretation of the cited studies and the final wording are my own. Every factual statement and page reference was checked against the original publications listed in the reference list. AI tools were not used as a source of information."

**Variant 2: AI also produced draft text (honest disclosure of substantial use):**

> "AI-based tools were used substantially during the preparation of this paper. ChatGPT (OpenAI, [model], [period]) generated initial text drafts and structural proposals on the basis of my instructions and the sources I provided. GitHub Copilot ([period]) was used to assess successive drafts against the IU criteria and to verify page references. I selected the sources, checked all statements and figures against the original publications, revised and rewrote the text over several versions, and take full responsibility for the content and its scientific accuracy. AI tools were not used as a source of information."

**Variant 2 only works if the IU guideline permits this kind of use.** If it does not, the solution is not to choose Variant 1 but to make Variant 1 true: rewrite the text yourself (P3) until AI use is limited to what the guideline permits.

**Avoid in either variant:**
- vague formulas such as "minor linguistic assistance" if more happened;
- listing the AI tool as a scientific source in the reference list (unless the guideline requires a reference entry for declared tools);
- pasting full chat transcripts unless the guideline asks for them.

---

## 6 Bottom line

| | v1 | v5 | v6 | v7 | v7 after P1 |
|---|---:|---:|---:|---:|---:|
| Indicative score | ≈ 62 % | ≈ 79 % | ≈ 82 % | **≈ 84 %** | ≈ 87–89 % |
| Indicative grade | 3.0 | 2.0/2.3 | 2.0 | **2.0/1.7** | **1.7 (1.3 possible)** |

You are close. The argument, the evidence and the references are now at the level of the target grade. What stands between this draft and 1.7 is mechanical (page numbering, ToC, figure) plus one integrity step: an accurate AI declaration that matches the IU guideline and a text you can defend as your own.
