# Assessment of Draft Version 5: "Learning and Search in AlphaGo and AlphaGo Zero"

| Item | Detail |
|---|---|
| Assessed file | `5th Draft/AlphaGo_Task1_Version5_Download.docx`, rendered with Word: 19 pp. in total; main text pp. 1–14; ≈ 4,490 words of prose; 9 reference entries (8 scholarly + 1 AI tool); 1 figure, 2 tables, 7 equations |
| Benchmarks | IU *Guidelines Written Assignment* (criteria and weights); *Guidelines for Structuring and Formatting Academic Papers* (01/10/2025); *Zitierleitfaden* (01/10/2026); task sheet DLMAIRIL01 Task 1 |
| Verification performed | All 8 scholarly sources were downloaded and every page locator checked against them (Section 3). Kocsis & Szepesvári and Williams are only available as preprint/tech-report versions, so their journal pages could not be confirmed. |
| Out of scope | Title page (to be completed by the author later) |

---

## 1 Verdict: development towards 1.0–1.7?

**Yes, a clear development, but not yet in the 1.0–1.7 band.** The scientific argument is now at the right level. Most of the remaining deductions come from formal and citation errors that are cheap to fix, plus a source base that is thinner than in v2.

| Criterion (weight) | First draft (v1) | Version 5 | Main remaining deductions |
|---|---:|---:|---|
| Introduction (10 %) | 60 | 85 | The method paragraph names no search strategy or selection criteria. |
| Structure (15 %) | 65 | 80 | Fig. 1 page is ⅔ empty (p. 4); 4 empty paragraphs leave gaps (e.g. p. 9); static ToC in the wrong order. |
| Reasoning (40 %) | 60 | 80 | 82 % of citations still go to the two DeepMind papers; several imprecise locators; invented numbers in the "illustrative example"; the transfer paragraph has no fitting source. |
| Conclusion (15 %) | 50 | 85 | Strong. A concrete recommendation for applied RL could be sharper. |
| Language/form (10 %) | 70 | 72 | Equations are plain text with underscores (`L_SL`, `p_σ`, `c_puct`); broken symbol "𝑣 𝑝𝜌 (s)"; very dense prose in Ch. 4–5. |
| Formalities (10 %) | 75 | 65 | No hyphenation; references justified, 10 pt, 1.2 spacing; captions 9 pt with "Fig. 1." / "Tab. 1."; abbreviation list inconsistent; Silver (2017) locators conflict with the journal pages listed. |
| **Weighted indicative score** | **≈ 62 %** | **≈ 79 %** | |

These are my own indicative scores, not an official IU grade. **≈ 79 % sits at the 2.0/2.3 boundary on common German 100-point conversions.** Fixing Section 6 P1–P2 is realistic and lifts the paper into the mid-80s, the typical 1.7 band. 1.3 or better additionally needs the explanatory edits in Ch. 4–5 and a few targeted origin sources.

**What v5 does well (and must be kept):**
- Evidence-weighted thesis: architecture, target source and decision-time search are separated by their degree of experimental control (5.2).
- Effect sizes throughout (3,055 vs 5,185 Elo; +600/+600 Elo; λ = 0.5; 494/495; the 0.01 value-loss weight of the SL comparator).
- The Fan → Lee → Master → Zero progression (Tab. 2) with correct caveats on match conditions.
- The external critique (Tian 2019, Wang 2023) is used precisely and with the right limits.

---

## 2 Comparison with the external recommendations

| External recommendation | My finding | Agreement |
|---|---|---|
| 1. Full source verification is the most important remaining task. | Done here (Section 3). **All Silver et al. (2016) numbers are correct.** Silver et al. (2017), Tian and Wang are correct in substance. However, I found **5 locator or attribution errors** and **1 systematic citation error** (the Silver 2017 pagination) that the external review did not catch. | Agree, and now largely resolved. Apply the fixes in Section 6. |
| 2. Independent authorship; review the AI disclosure against the IU policy. | Agree, and the problem is more concrete than stated: the DOCX carries **machine-generation metadata** (Section 5.1), and the disclosure under-describes the AI involvement. | Agree, and stronger. |
| 3. Title page. | Out of scope by your instruction. | — |
| 4. Explanatory density in Ch. 4–5; fix through selective editing. | Agree. The concrete targets are in Section 6, P3. | Agree |
| "Freeze v5; do not create another version." | Freeze the **argument**, yes. But the formal and citation corrections are not optional polish: they affect two criteria (20 %) and a marker will see them on the first page of the references. | Partly agree |
| "No more references." | Agree: no padding. **But 2–3 origin sources are needed** because v5 makes claims whose original source is missing: residual learning (Eq. 5), PUCT and the history of MCTS. v5 also dropped sources that v2 had (He et al., Coulom, Rosin, Auer). One "free" gain: Sutton & Barto §16.6 (pp. 441–450) is an independent textbook treatment of AlphaGo and Zero, and the book is **already in the reference list**. | Partly disagree |
| Be able to explain three concepts independently. | Strongly agree. I would add a fourth (Section 7). | Agree |

---

## 3 Source and locator verification

✓ = verified in the source; ◐ = substance correct, locator imprecise; ✗ = wrong or unsupported; ? = could not be verified.

### 3.1 Silver et al. (2016), *Nature* 529, 484–489 (all numbers verified)

| Claim in v5 | Cited | Verified location | Status |
|---|---|---|---|
| b ≈ 250, d ≈ 150; evaluation difficult | p. 484 | p. 484 | ✓ |
| SL 57.0 %; rollout 24.2 %, 2 µs vs 3 ms | p. 485 | p. 485 | ✓ |
| RL > 80 % vs SL; 85 % vs Pachi (100,000 sims); opponent pool | p. 485 | p. 485 | ✓ |
| SL prior better in search ("diverse beam") | pp. 486–487 | p. 486 | ✓ (p. 486 suffices) |
| MSE 0.19/0.37 → 0.226/0.234 | p. 486 | p. 486 | ✓ |
| Value net ≈ rollouts with 15,000× less computation | p. 486 | p. 486 | ✓ |
| Most-visited move | Methods / p. 486 | p. 486 | ✓ |
| 1,202 CPUs / 176 GPUs; 48 CPUs / 8 GPUs | pp. 487–488 | p. 487 | ✓ |
| 494/495; 77 % distributed vs single | pp. 487–488 | p. 488 | ✓ |
| Value-only beats all programs; λ = 0.5 best, ≥ 95 % | p. 488, Fig. 4b | p. 488 | ✓ |
| Fan Hui 5–0, no handicap; "a decade away" | p. 488 | p. 488 | ✓ |
| Methods sections "Problem setting", "Search algorithm", "Features…", "Neural network architecture", "Evaluation" | section labels | all exist | ✓ |

### 3.2 Silver et al. (2017), checked against the UCL accepted manuscript

| Claim | Cited | Verified | Status |
|---|---|---|---|
| Lee 4–1; Master 60–0; Lee value net from search self-play, 12 layers × 256 | pp. 21–22 | pp. 21–22 | ✓ |
| Lee "trained over several months" | pp. 6, 10, 21–24 (5.1 ¶4) | **p. 8** | ◐ add p. 8 |
| Perfect information / alternating Markov games | p. 20 | p. 20 | ✓ |
| 17 planes; history and komi | pp. 22–23, 27 | p. 27 | ✓ |
| 4.9 M games / 3 days; 29 M / 40 days | pp. 6, 10 | pp. 6, 10 | ✓ |
| 362 policy logits; tanh value head | pp. 28–29 | pp. 28–29 | ✓ |
| Policy-improvement operator; approximate policy iteration | pp. 3–6, 19 | pp. 3, 19 | ✓ |
| 1,600 sims; τ = 1 for 30 moves; Dir(0.03), ε = 0.25; 55 % / 400 games | p. 24 | p. 24 | ✓ |
| PUCT formula; thread locked during evaluation | pp. 25–27 / p. 26 | p. 26 | ✓ |
| Transposition table (larger run) | pp. 25–27 | pp. 23, 27 | ✓ |
| SL comparator: value loss weighted 0.01 | pp. 8, 24–25 | p. 25 | ✓ |
| Elo ladder; raw network 3,055; 89–11 | p. 12 | p. 12 | ✓ |
| Self-play bias correction of Elo | p. 30 | p. 30 | ✓ |

**✗ Systematic citation error:** the reference entry now gives *Nature 550*(7676), **354–359** plus the DOI, but every in-text locator (pp. 3–30) refers to the **42-page accepted manuscript**. A marker who checks "Silver et al., 2017, p. 27" against a 6-page journal article finds a non-existent page. **Fix:** add a footnote at the first citation, e.g. "Page numbers for Silver et al. (2017) refer to the authors' accepted manuscript (UCL Discovery), whose Methods section is not paginated in the journal version". Alternatively, restructure the reference so that the manuscript is the cited version.

### 3.3 Other sources

| Source / claim | Cited | Verified | Status |
|---|---|---|---|
| Browne et al.: MCTS "provided a powerful approach to computer Go before AlphaGo" (Intro ¶1) | pp. 3–6 | pp. 3–4 are the table of contents and background. The statement is on **p. 1** and **p. 27** ("top computer Go programs all use MCTS and play at the strength of a good amateur player") | ✗ change to pp. 1, 27 |
| Browne et al.: four-phase cycle | pp. 5–6 | §3.1, pp. 5–6 | ✓ |
| Kocsis & Szepesvári: UCT | pp. 283–286 | In the preprint, UCT is defined in §2 = journal pp. **284–286** if the pagination is identical | ? verify against Springer version; p. 283 is the introduction |
| Williams: REINFORCE | pp. 233–234 | Only a tech-report version with its own pagination was accessible. REINFORCE is defined in §4; **episodic** REINFORCE (what AlphaGo uses) is in §6 | ? verify journal pages; cite §6 for the episodic case |
| Sutton & Barto: value functions | pp. 58–59 | §3.5 starts p. 58 | ✓ |
| Sutton & Barto: planning, Dyna | pp. 159–163 | Ch. 8 p. 159; §8.2 p. 161 | ✓ |
| Sutton & Barto: MCTS | pp. 185–188 | §8.11 p. 185 | ✓ |
| Sutton & Barto in the **transfer paragraph** (5.3 ¶5: model error, partial observability, costly interaction) | pp. 159–163, 185–188 | These pages cover Dyna and MCTS, not model error. §8.3 "When the Model Is Wrong" starts **p. 166** | ✗ change to p. 166ff.; the partial-observability claim needs its own source |
| Tian et al.: AGZ total compute unknown (self-play workers not reported) | pp. 6246–6247 | p. 6246 | ✓ |
| Tian et al.: 20–0 prototype, hybrid process, ≈ 80,000 rollouts | pp. 6244, 6247 | pp. 6244, 6247 | ✓ |
| Wang et al.: > 97 % vs KataGo; adversary loses to amateurs | pp. 35655–35658 | p. 35655 (fn. 1), p. 35656 | ✓ |

Page numbers for Sutton & Barto were taken from the openly available 2020 PDF of the 2nd edition (printed page = PDF page − 22). Check them once against a print copy if your library has one.

---

## 4 Reference list: completeness and missing elements

### 4.1 Entry-level errors

| Entry | Problem | Fix |
|---|---|---|
| Silver et al. (2017) | Journal pages plus "Accepted manuscript: URL" appended; in-text locators refer to the manuscript (see 3.2). | Keep the DOI entry and add the footnote, or cite the manuscript as the consulted version. |
| Sutton & Barto (2018) | Year 2018, but the URL points to `RLbook2020.pdf` (the corrected online version). | Either drop the URL (print edition) or keep it and state "(2nd ed., online version 2020)" consistently. |
| OpenAI (2026) | APA software format is incomplete: no version or model identifier, no date of use. IU (§2.3.7) requires the AI tool to be named under the figure **and** in the reference list, with the prompt. | `OpenAI. (2026). ChatGPT ([model/version], [date of use]) [Large language model]. https://chatgpt.com/` |
| Kocsis & Szepesvári; Williams | Page locators not verifiable from open versions. | Check via the IU library (Springer). |
| All entries | Justified alignment produces visible gaps (e.g. "Accepted manuscript:"). | Left-align (Zitierleitfaden p. 26: "einseitig linksbündig"). |

### 4.2 Missing elements in the text

1. **No footnote explaining the Silver (2017) pagination** (see 3.2).
2. **Abbreviation list:** DNN and UCB1 are listed but never used; CNN (4×) and MSE (2×) are used but not listed. The PUCT expansion has no source (Rosin is missing).
3. **The "AI-assisted preparation note" sits as a level-2 heading under "References".** The reference list cannot have subsections. Move it to wherever the IU AI-use policy requires (declaration or appendix) and reword it truthfully (Section 5).
4. **The ToC is static text without page alignment or a TOC field.** It lists "List of figures / List of tables" *after* Chapter 6 with Roman numerals and omits the list of abbreviations. Rebuild it with Word's TOC field.
5. **Lists of figures and tables are optional** with only one figure and two tables (formatting guidelines, p. 5). Keep or remove them, but order them correctly.

### 4.3 Missing literature (targeted, not padding)

| Priority | Source | Why it is needed in v5 as written |
|---|---|---|
| **A** | **Sutton & Barto (2018), §16.6 "Mastering the Game of Go", pp. 441–450** | Already in the list. It provides an independent textbook account of Fan and Zero and lowers the 82 % DeepMind citation share without adding a new entry. |
| **A** | He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. *CVPR*, 770–778. https://doi.org/10.1109/CVPR.2016.90 | Eq. 5 and the residual "skip-addition principle" (4.1) are currently cited only to Silver 2017. The original source is required. |
| **A** | Rosin, C. D. (2011). Multi-armed bandits with episode context. *Annals of Mathematics and Artificial Intelligence, 61*(3), 203–230. https://doi.org/10.1007/s10472-011-9258-6 **or** Coulom (2007), *Computers and Games*, 72–83, https://doi.org/10.1007/978-3-540-75538-8_7 | PUCT (Eq. 7, abbreviation list) and the origin of MCTS. Choose one if the page budget is tight. |
| B | Dulac-Arnold, G., et al. (2021). Challenges of real-world reinforcement learning. *Machine Learning, 110*, 2419–2468. https://doi.org/10.1007/s10994-021-05961-4 | The transfer paragraph (5.3 ¶5) currently has no fitting source. |
| B | Anthony, Tian & Barber (2017), Expert Iteration (NeurIPS 30) | Supports the "search as policy improvement / apprentice" framing in 4.2 independently of DeepMind. |

The result would be **11–13 references**: lean, but with every claim traced to an origin and the DeepMind share below 70 %.

---

## 5 AI-generation and integrity signals

Text-based AI detection is probabilistic, so none of the textual signals below proves anything. **The file-level signals in 5.1, however, are hard evidence** that a script produced the document, and anyone who opens *File → Info → Properties* can see them.

### 5.1 File and metadata signatures (high risk; remove before submission)

| Signal | Where | Why it matters |
|---|---|---|
| `dc:creator = python-docx`, `dc:description = "generated by python-docx"` | `docProps/core.xml` | Literally states that a program generated the document. |
| `created = modified = 2013-12-23T23:15:00Z` | `docProps/core.xml` | The python-docx template default timestamp, an unmistakable fingerprint. |
| `Application = Microsoft Macintosh Word`, AppVersion 14, Words = 0, Pages = 1 | `docProps/app.xml` | Template leftovers that are inconsistent with a 19-page document. |
| Custom style names `CaptionReview`, `BibliographyReview`, `Equation` | `styles.xml` | Names typical of generated build scripts, not of Word's built-in styles (Caption, Bibliography). |
| No TOC field, no OMML equations, static ToC | `document.xml` | Consistent with programmatic generation rather than authoring in Word. |
| File name `…Version5_Download.docx` | — | Suggests a download from a chat tool. |

The PDF you export from Word gets fresh metadata (Word 365), so Turnitin will not see the DOCX properties. But if the DOCX is ever requested, or the PDF is produced from this file without re-authoring, the trace remains. **Action:** create a new document from your own Word template, paste the text in, rebuild styles, equations and the ToC natively, and run *File → Info → Check for Issues → Inspect Document* to remove the properties. This is also the moment to rewrite the text in your own words (5.3).

### 5.2 Textual signals (moderate; typical of LLM prose)

| Indicator | v5 value | Comment |
|---|---|---|
| Paragraph length uniformity | 58 paragraphs, mean 77 words, SD 13 (CV 0.17) | Human academic prose usually varies far more. |
| Paragraphs ending with a parenthetical citation | 48 of 58 (83 %) | A formulaic "claim, claim, claim (Source, pp.)" template. |
| Contrastive hedges ("rather than", "not a/an …", "does not / cannot") | 34 | Lower than v1 (68), still a recognisable pattern. |
| Colons and semicolons | 67 in 4,490 words | Dense list-like syntax. |
| Self-labelled sentence types | "Illustrative decision example (not experimental AlphaGo data)…", "The counts are illustrative, not computed from a particular PUCT search" | Meta-commentary typical of generated text. It also introduces invented numbers (0.70/0.30; 46/74 visits). |
| Stock phrases | "evidence-weighted", "design bundle", "disciplined interaction", "evidence boundaries", "operationally", "materially" | Individually fine, but clustered they read as generated. |
| Figure caption | "Diagram rendered with AI-assisted Python (OpenAI, 2026); prompt: …" | Transparent, which is good, but it confirms AI involvement to the marker. |

### 5.3 Integrity risk in the disclosure

The note says AI supported "diagram-code generation and language/structural editing". If the argument, structure and wording were in fact largely generated across several chat sessions, this **understates** the AI's role. The *Zitierleitfaden* (pp. 4–5) refers you to the separate IU AI policy on myCampus for what is permitted and how to declare it. **Read that policy and make the declaration factually accurate.** An understated declaration is a larger risk than an honest one. You must also be able to defend every sentence orally.

---

## 6 Rework tasks for v5 (prioritised)

### P1: Citation correctness (do first; ≈ 1–2 h)

- [ ] **C1** Add a footnote at the first Silver (2017) citation explaining that locators refer to the accepted manuscript. Footnote in Arial 10.
- [ ] **C2** Intro ¶1: change "Browne et al., 2012, pp. 3–6" to **pp. 1, 27** and, if you like, use the p. 27 statement ("good amateur" level before AlphaGo).
- [ ] **C3** 5.3 ¶5 (transfer): replace Sutton & Barto pp. 159–163, 185–188 with **p. 166ff. (§8.3)** for model error, and add a source for partial observability and costly interaction (Dulac-Arnold et al., 2021), or cut those two claims.
- [ ] **C4** 5.1 ¶4: add **p. 8** for "Lee was developed over several months".
- [ ] **C5** Williams: verify pp. 233–234 in the journal version; for AlphaGo's episodic outcome-based update, cite the episodic REINFORCE section (§6) or Sutton & Barto §13.3 (p. 326ff.).
- [ ] **C6** Kocsis & Szepesvári: verify p. 283 vs 284 in the Springer version (UCT is defined in §2).
- [ ] **C7** Add **He et al. (2016)** for Eq. 5 and **Rosin (2011) or Coulom (2007)** for PUCT/MCTS origins.
- [ ] **C8** Use Sutton & Barto **§16.6, pp. 441–450** at 2–3 places (3.1 network inventory, 4.2 self-play loop, 5.1 evolution) to diversify the evidence base.
- [ ] **C9** Complete the OpenAI entry (model, version, date) and Sutton & Barto (year vs URL).
- [ ] **C10** Harmonise section-label quotes: Methods section labels currently mix straight `"…"` and curly `‘…’` quotes. Use one style throughout.

### P2: Formalities (≈ 1–2 h; ≈ 10 % of the grade)

- [ ] **F1** Turn on **automatic hyphenation** (Layout → Hyphenation → Automatic). It is currently off, and IU requires it.
- [ ] **F2** Reference list: Arial **11 pt**, **1.5 line spacing**, **left-aligned**, hanging indent 1.27 cm (currently 10 pt, 1.2 spacing, justified).
- [ ] **F3** Captions: "**Fig. 1** Learning and search …" and "**Tab. 1** …" with no period after the number, and "Source: …" in **10 pt** (currently 9 pt). Table body text no smaller than 9 pt; Tab. 2 is currently 8 pt and hard to read.
- [ ] **F4** Write all 7 equations with the **Word equation editor** (true sub- and superscripts). Replace `L_SL`, `p_σ`, `v_θ(s_L)`, `c_puct`, `Σ_b`, `f_θ` and the broken "𝑣 𝑝𝜌 (s)" in 3.3 ¶1.
- [ ] **F5** Rebuild the **ToC as a Word field** with right-aligned page numbers, front-matter lists before chapter 1, and the list of abbreviations included.
- [ ] **F6** Abbreviations: delete DNN and UCB1; add CNN (Convolutional neural network) and MSE (Mean squared error); keep the list alphabetical.
- [ ] **F7** Remove the 4 empty paragraphs (they cause the half-empty area on p. 9). Reflow Fig. 1 so that p. 4 is not ⅔ empty, e.g. scale the figure and let the text of 3.1 start on the same page.
- [ ] **F8** Fix spaced en dashes in page ranges ("486– 487", "21– 22", "23– 24") and "programme" → "program" (for software), and use "Fig. 1"/"Tab. 1" consistently in the running text (it currently mixes "Figure 1" / "Fig. 1" and "Table 1" / "Tab. 1").
- [ ] **F9** Move the "AI-assisted preparation note" out of the References section (see 5.3).
- [ ] **F10** Final page check: main text 12–15 pp. (currently 14; do not exceed 15 after adding footnotes and sources).

### P3: Reasoning and explanatory density (selective edits, no added pages)

- [ ] **R1** Replace the **illustrative decision example** (3.4 ¶2) with a short, *computed* PUCT calculation using Eq. 7: two actions, priors 0.7/0.3, given Q values and visit counts, showing U and the selected action. Alternatively, use the real example in Silver et al. (2016, Fig. 5, p. 487), which shows the value-network, policy-network, rollout and visit-count statistics behind one actual move against Fan Hui (check the figure before describing which statistic peaks where). Do not use invented visit counts.
- [ ] **R2** In 5.2, add **one sentence per experiment** saying *what is held constant and what varies*, e.g. "Same data and search; only network topology varies → architectural effect." A 3-row mini-table could replace two dense paragraphs at no extra length.
- [ ] **R3** 4.2 ¶2: state the policy-improvement loop in two plain sentences before the technical one (search → better move distribution → network imitates it → better search).
- [ ] **R4** Break up 3–4 of the longest sentences (maximum currently 47 words) and vary paragraph length. This improves readability and reduces the uniform-template signal.
- [ ] **R5** Methods paragraph (Intro ¶4): add 1–2 sentences on how sources were found and selected (databases, criteria: primary system papers, peer-reviewed methodology, independent replication or critique).

### P4: Authorship (non-delegable)

- [ ] **A1** Rebuild the document in your own Word file and remove the python-docx metadata (5.1).
- [ ] **A2** Rewrite the text in your own wording, section by section, checking each claim against the source pages listed in Section 3.
- [ ] **A3** Bring the AI declaration in line with the IU AI policy and with what actually happened (5.3).

---

## 7 Self-test before submission

Explain each point aloud in 2–3 minutes, without notes. The first three come from the external review; the fourth is my addition.

1. **Why AlphaGo Fan uses different models for different functions.** SL policy = broad human-like prior for search; RL policy = generator of strong self-play games for value training; value net = cheap leaf evaluation; rollout policy = very fast but weak continuation (2 µs vs 3 ms). Explain why the stronger RL policy is the *worse* search prior.
2. **How MCTS changes an individual decision.** Selection by Q + U (Eq. 7), expansion with priors, evaluation, backup; the most-visited root move can differ from the network's top move. Evidence: 3,055 vs 5,185 Elo.
3. **Why Zero's gain cannot be attributed to removing human data alone.** Fixed-data ablation (+600/+600 Elo from architecture); the SL-vs-self-play control changes the value-loss weight (0.01) and the data volume; Master vs Zero still differs in features, rollouts and initialisation; Lee already used search-generated value targets.
4. **What "without human knowledge" does and does not mean.** Rules and simulator, Tromp–Taylor scoring, symmetry augmentation, colour transposition, GP-tuned search hyperparameters (Silver et al., 2017, pp. 22–23).

---

## 8 Bottom line

v5 is a substantial step up from v1 (≈ 62 % → ≈ 79 %) and argues at Master level. It does not yet reach 1.0–1.7 because of citation precision (one systematic error, five locator or attribution errors), formatting deviations, and a lean, DeepMind-heavy source base. P1 + P2 + C7/C8 are mechanical and should take one working day; they make 1.7 realistic. P3 and P4 decide whether 1.3 or better is within reach, and P4 also removes the integrity risk.
