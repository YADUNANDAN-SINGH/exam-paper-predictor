---
name: exam-paper-predictor
description: Predicts an upcoming exam paper from real past papers (PYQs, past papers, old exams) for any school board, university, college, entrance or professional exam, in any country or language. It finds 5–20 years of papers itself, maps the pattern and topic-wise weightage, and backtests its predictions on past years. Then it builds mock paper PDFs, separate solutions PDFs and an important-topics PDF, and can score a prediction against the real paper afterwards. Use whenever someone asks for a mock, sample, model, guess, practice or predicted paper, past-paper or PYQ analysis, exam pattern, topic or chapter weightage, important or most-expected questions, what to study before any exam (board, semester, midterm, final, resit, entrance or licensing), or to test prediction accuracy on an exam that already happened, even if they never say "past papers".
---

# Exam Paper Predictor

Predict a student's upcoming exam paper from real past papers. Test the prediction method on past years before trusting it, then deliver:

1. **Mock paper PDFs**, as many as the student asks for, in the real paper's pattern
2. **A separate solutions PDF** for each mock
3. **An important-topics PDF**: what to study, ranked by evidence

This works for any school board, university, college, entrance or professional exam, in any country and language. Nothing here is specific to one exam or one country: everything about the target exam comes from the student and from the papers you find. "Past papers" means real previous exam papers, whatever they're called locally: PYQs in India, past papers in the UK and Commonwealth, old exams in the US, Altklausuren in Germany, annales in France.

**The rule everything rests on:** every prediction traces back to real papers, and every accuracy number comes from a measured backtest. Never invent a past question, a year, a source or an accuracy figure. A student who catches one fake "past question" stops trusting the whole pack.

## Workflow

1. Intake: the target exam, who sets it, and the past-paper source
2. Collect 5–20 years of real papers
3. Map the pattern and topic-wise weightage
4. Backtest: predict past papers blind, score, refine
5. Predict the upcoming paper and write the mocks
6. Write and verify the solutions
7. Build the important-topics PDF
8. Check and deliver
9. Afterwards: score the prediction against the real paper, or run a test on an exam that already happened

Keep two working files in the working directory: `paper_bank.csv` (one row per question) and `backtest_log.md`. They keep the analysis reproducible and let you resume if interrupted.

**Short on time?** If the exam is within about 2 days, hold out just 1 paper in Step 4. Build and send the important-topics PDF first, then the mocks.

## Step 1 — Intake

Ask only for what's missing, all in one message, in the student's language. Only the exam itself is required; everything else has a default, and anything public you find yourself.

**Required: the exam they're targeting.** Country, institution (board, university, college or exam body), program and year or semester, course or subject (with its code if it has one), and which exam: board exam, end-semester, midterm, final, resit or entrance test. Codes and syllabus schemes change over time, and the wrong code finds the wrong papers.

**Ask, but never wait on: their past-paper source.** "Is there a website or archive you trust for official past papers? If not, I'll find them." With no answer, find the papers yourself (Step 2). Many institutions keep past papers behind a login (Moodle, Canvas, Blackboard, a library archive, a student-society archive). You can't log in, so for those ask the student to download and upload them. Photos and PDFs both work.

If the student says files are attached but none arrived, name exactly what's missing. Fetch anything public yourself instead of asking for it.

**Helpful** (if not given, use the default)

| Input | Default |
|---|---|
| Topics or units in scope, and anything excluded | The full current syllabus or course outline |
| Paper pattern, or a photo of a recent paper | Pattern of the most recent real paper |
| Number of mock papers | 2 |
| Exam date | The next scheduled sitting |
| Language of the paper | The language of the past papers |
| Exam conditions: open or closed book, calculator, formula sheet, online or on paper | Same as the most recent paper |
| For instructor-set exams: practice exams, problem sets, lecture slides, topic lists | None |

If the student doesn't answer the optional questions, don't stall. Proceed with the defaults and say which ones you used. A photo of a real paper is the best layout template: copy its header, instructions, sections, numbering and choice notation.

**Work out who sets the paper.** Everything downstream depends on it. If you can't tell, ask.
- **Central setter**: a board, an affiliating university or a national exam body sets one paper for many students. Past papers are usually public, and patterns repeat across years.
- **Instructor-set**: the course instructor or department writes the paper. This is how most universities in the US, UK, Europe and Australia work, and autonomous colleges too. Past papers are fewer and often behind a login, and a new instructor can change everything. Ask who teaches the course this term.

## Step 2 — Collect real past papers

Find all the papers first, then read them oldest first. Leave the most recent 1–3 unread for now; Step 4 explains which and why.

**Where to look**
- If the student named a trusted source, use it first. Go elsewhere only to fill gaps, and tell them when you do.
- Central setter, in this order:
  1. The official site of the board, university or exam body
  2. Its archive or library portal
  3. Established past-paper repositories
- Instructor-set, in this order:
  1. The course website and the instructor's own page
  2. Department or library exam archives
  3. Student-society archives
  4. The student's LMS, through uploads

  Past exams of the same subject at other institutions are different papers. Use them only as extra practice, tagged `[Other institution]`, never as evidence for the prediction.
- Search in the institution's language with its local term, combined with the institution, course name, code and year:

| Language | Local terms |
|---|---|
| English | previous year question papers / PYQ (India), past papers (UK, Commonwealth), past questions (West Africa), old exams, practice exams, past finals (US) |
| Hindi | पिछले वर्ष के प्रश्न पत्र |
| German | Altklausuren |
| French | annales, sujets d'examen |
| Spanish | exámenes anteriores, exámenes resueltos |
| Portuguese | provas anteriores, exames resolvidos |
| Italian | temi d'esame |
| Dutch | oude tentamens |
| Turkish | çıkmış sorular |
| Russian | экзаменационные билеты, вопросы к экзамену |
| Chinese | 历年真题, 往年试题 |
| Japanese | 過去問 |
| Korean | 기출문제 |
| Arabic | امتحانات سابقة |

- Record the URL of every paper you use.
- Use only papers the student is allowed to access. Never look for leaked or unreleased papers for the upcoming exam (that's academic misconduct), and never get around a login or paywall.

**How many**
- Aim for 10–20 years, with a minimum of 5.
- Every real sitting counts as one paper. Two sittings a year give two papers per year; exams held in shifts give one paper per shift. Resit and supplementary papers count too, but tag them, because they're sometimes set differently.
- Match the kind of exam: past finals predict a final, past midterms predict a midterm. Use the other kind only for style and question types.
- Instructor-set courses often have fewer than 5 papers from the current instructor. Use earlier instructors' papers at lower weight, and lean on practice exams, problem sets and lecture emphasis.
- If you find fewer than 5 years of papers, tell the student right away and continue with what exists. Add, in this order:
  1. Official sample papers, mark schemes and blueprints, tagged `[Official sample]`
  2. Previous-scheme papers for topics still in the syllabus
  3. Papers the student uploads

  Mark every prediction as low-confidence.
- If the exam draws from a published question bank (exam-ticket lists, question catalogues for oral exams, official question banks), get the bank itself. The job becomes ranking which items are most likely and preparing all of them.
- If the exam body never releases papers (some licensing and professional exams), there is nothing to backtest. Use the official content outline, its weightage, and any official practice tests. Label the mocks as practice papers, not predictions, and make no accuracy claims.

**Reading**
- Many sites host scans or image viewers. If text extraction or a fetch returns nothing usable, render the pages to images and read them, or open the viewer in a browser tool, scroll and zoom.
- If a paper is only partly readable, use what you can read and mark it partial.
- If the syllabus scheme changed within your range, note the year. Map old topics to the current syllabus and drop topics no longer in it.

**Recording**: one row per question in `paper_bank.csv`:
`paper_id, session (e.g. 2023-Dec), setter, source_url, section, q_no, marks, unit, topic, question_type, format, repeat_of, text`

- `setter` is the instructor or exam body.
- `marks` is marks or points, whichever the paper uses.
- `format` is MCQ, short, long, numerical, essay, case, coding, drawing, oral and so on.
- `repeat_of` names an earlier question this one repeats verbatim or nearly so.
- With internal choice, record every printed question.

`question_type` is the key column. Name a type by what the student must *do*, so questions solved by the same method share a type even when the numbers or the wording change:

| Real question | question_type |
|---|---|
| Verify Euler's theorem for u = (x³ + y³)/(x + y) | Euler's theorem — verify for a given function |
| Find the Thevenin equivalent across terminals AB | Thevenin equivalent — numerical |
| Explain the sliding filament theory of muscle contraction | Muscle contraction — mechanism, descriptive |
| "Economic causes outweighed political ones." Discuss, with reference to 1914. | Causes of WWI — evaluate a claim, essay |

For large MCQ exams (100+ questions), use concept-level types (chapter → concept) and keep the text only for questions you'll quote. Otherwise the data gets too sparse to show patterns.

## Step 3 — Pattern and weightage

Compute everything with code (pandas or plain Python), not by eye. Run this first on the papers that are not held out (see Step 4), then again on all papers after Step 4.

**Pattern**
- Sections, number of questions, marks each, internal choice ("any 2 of 3", "OR"), formats, duration and total marks.
- Negative marking and exam conditions: open or closed book, calculator, formula sheet, online or on paper.
- Any pattern change, and when it happened. The latest pattern governs the mocks; older papers still count for topic and type frequency.

**Topic-wise weightage**
- For each unit or topic: marks per paper, average share of the total, range, and trend over the last 3–5 papers.
- Weight by marks, not question count: one 10-mark question outweighs three 1-mark questions.

**Question-type frequency**
For each type, record the papers it appeared in (out of N), its usual section and marks, and the last session it appeared. Then label its signal:
- **Fixed**: appears in at least 70% of papers, usually in the same section
- **Rotating**: alternates with a sibling type (A one year, B the next)
- **Rising**: rare early, frequent recently
- **Fading**: absent from the last 3+ papers
- **Never asked**: in the syllabus but never seen

**Repeat rate**: the share of questions that repeat an earlier past question verbatim or nearly so. This varies widely between exams, so measure it rather than assume it.

**Instructor-set exams**: also measure how many exam questions mirrored homework, practice-exam or lecture examples. In many courses that overlap is the strongest predictor available.

## Step 4 — Backtest: predict past papers before reading them

This step is what makes the predictions trustworthy. Before predicting the real exam, prove the method on past papers it hasn't seen, measure the match, and improve it.

**Set up**
- Sort the papers oldest to newest. Hold out the most recent ones as tests: 3 if you have 8 or more papers, 2 if you have 6–7, and 1 if you have 3–5.
- With fewer than 3 papers from the same setter, a backtest tells you almost nothing. Skip it, say so, and mark the predictions low-confidence.
- Read and record every paper except the held-out ones. Find the held-out papers' URLs, but don't read their questions yet. If you must open one to confirm it's the right paper, look only at the header.
- You may use a held-out paper's structure (sections, question counts, marks), since students know the pattern before their exam too. Its questions stay off-limits until scoring.
- If the student's sample photo is itself one of the papers, don't hold it out.
- If the held-out papers are already visible in the conversation, you can't be truly blind. Generate each blueprint mechanically, with code, from the earlier papers' data only. Note in the reliability section that the test was not fully blind.

**Each round** (oldest held-out paper first)
1. **Predict.** Using only papers dated before the held-out paper, write a blueprint with exactly as many question slots as that paper. Each slot is section + marks + topic + question_type; for question-bank exams, a slot is a bank item. Save it in `backtest_log.md` before you read the paper.
2. **Reveal.** Read the held-out paper and add it to `paper_bank.csv`.
3. **Score.** Match each actual question to at most one predicted slot, then compute:
   - **Type hit rate**, the main accuracy figure: marks of actual questions whose type was predicted ÷ total printed marks
   - **Topic coverage**: marks of actual questions whose topic was predicted ÷ total printed marks
   - **Repeats caught**: how many of the actual verbatim repeats you predicted

   Because the blueprint has the same number of slots as the real paper, predicting everything can't inflate the score.
4. **Diagnose** each miss in one line. Common causes: new topic, missed rotation, recency underweighted, pattern change, instructor change, or a type labelled too narrowly or too broadly.
5. **Refine** the method and log the change, e.g. "weight last 3 papers ×2", "treat A/B as a rotating pair", "Section C always draws from Units 3–4". Every refinement must be a general rule that could have been known before that paper. Never add a rule that just names a question you saw in it.
6. **Move on** to the next held-out paper. The one you just scored joins the training data.

**Default starting method** (the backtest tunes it)
- Score each type by the number of papers it appeared in, with the last 3 papers counting double. For instructor-set exams, the current instructor's papers also count double.
- For a rotating pair, predict the member that didn't appear last time.
- Fill each section's slots with the highest-scoring types that usually appear there at those marks. Keep marks per unit close to each unit's average weightage.
- If history shows new types every year, reserve 10–20% of slots for rising or never-asked types.

**When to stop**
- Target: a type hit rate of 90% or more on the held-out papers.
- Stop when you reach it, or when two refinement rounds bring no gain. Tuning past that point memorises the past instead of predicting the future.
- Some exams don't repeat enough for 90%, especially large competitive exams and exams with a new instructor. Report what you actually achieved and why.

**Report two scores per held-out paper.** The **blind** score comes before any refinement from that paper; the **refined** score comes after. The blind score is the honest estimate of real-exam accuracy, so never report the refined score alone.

Once the backtest is done, send the student a short chat update before building the PDFs: papers found, the pattern, the top-weightage topics and the blind/refined scores. It's useful on its own, and it lets them correct the scope early.

## Step 5 — Predict the upcoming paper and write the mocks

1. Apply the refined method to **all** papers to produce the final blueprint for the upcoming exam. Use the latest pattern and only in-scope topics.
2. **Mock 1 is the most-likely paper**: the final blueprint, filled in.
3. **Mocks 2…N** keep the real pattern and weightage, but use the next-most-likely options for rotating and uncertain slots, and different question types on the high-weight topics. Together the mocks should cover every Tier 1 and Tier 2 type (Step 7). If the student asks for more than about 5, tell them the later ones will overlap, then make them anyway.

**Writing questions**
- Write in the paper's language and conventions: command words ("Derive", "Prove that", "Discuss", "Explain with a neat diagram"), notation, number format, difficulty and length.
- Give repeat-type questions fresh numbers, a fresh function or a fresh case. Include near-verbatim repeats in roughly the measured repeat rate: if this exam repeats questions word for word, the mock should too.
- Stay strictly inside the student's scope. Leave borderline topics out of the paper and mention them in the important-topics PDF instead.
- If a question needs a figure (circuit, graph, diagram, map, data table), draw it in code, for example with matplotlib, schemdraw, or TikZ under LaTeX. Never refer to a figure that isn't there.

**Layout**: follow the student's sample or the latest real paper. Include the header (exam, subject, code, time, maximum marks), instructions, sections, numbering, marks per question, choice notation and page numbers. Keep source tags off the question paper so it feels real; they go in the solutions.

## Step 6 — Solutions (one separate PDF per mock)

- Put the answer key for objective questions first, then full solutions in paper order.
- Write answers the way this exam awards marks. If a mark scheme or rubric is available, follow it.
  - **Numericals**: Given → Formula → Substitution → Calculation → Result with unit
  - **Derivations and proofs**: every step
  - **Theory**: key points, definitions, labelled diagrams, and a sensible length for the marks
  - **Essays and case questions**: a model outline with the thesis, main arguments, evidence or cases to cite, and what lifts an answer to top marks
  - **Coding**: a reference solution, run against test cases in code
- Under each solution, add a source tag such as `Type seen in 5 of 8 papers: 2019-May Q4, 2022-Dec Q5, 2024-May Q3` or `[Original — rising topic]`.
- **Verify every numerical and symbolic answer in code** before it goes in the PDF, using Python, with sympy for algebra and calculus. Recheck every MCQ key. If the check and the solution disagree, find the error and fix the solution.
- If a source question looks misprinted, say so and use the corrected version.

## Step 7 — Important-topics PDF (study before the exam)

Sections, in this order:
1. **Pattern at a glance**: one table.
2. **Topic-wise weightage**: average marks and %, range, trend and papers appeared in. A simple bar chart helps.
3. **Must-study topics, in tiers.** For each topic, list the question types asked, one real past question with its session tag, and the usual marks.
   - **Tier 1 — Must study**: in at least 70% of papers, or a high-confidence slot in the final blueprint
   - **Tier 2 — Should study**: 40–70%
   - **Tier 3 — If time permits**: appeared at least twice, or rising
   - **Low priority**: fading or never asked. These are still in the syllabus, so never say "skip".
4. **Most expected questions**: the top 15–30 types, ranked, each with a real past question as an example.
5. **Repeated questions**: questions that have already come word for word more than once.
6. **Common mistakes** that lose marks on Tier 1 types.
7. **Revision plan** for the time left, if the exam date is known. With one day left, cover Tier 1 only, in order.
8. **How reliable is this?** The papers used (count and sessions), each held-out paper's blind and refined scores, the main misses and why, and any data gaps.
9. **Sources**: every paper used, with its URL.

## Step 8 — Check and deliver

- **Tooling**: use whatever PDF tooling is available. LaTeX suits maths-heavy subjects. For right-to-left or complex scripts (Arabic, Urdu, Hebrew, Devanagari, Bengali, Tamil, Thai), use HTML-to-PDF in a browser engine or XeLaTeX/LuaLaTeX, because ReportLab doesn't shape these scripts correctly. Noto fonts cover most scripts.
- **Paper size**: use the country's standard, A4 or US Letter.
- **Visual check**: render every page to an image and inspect it for overflowing equations, broken tables, stranded headings, questions split across pages and missing figures.
- **Marks check**: for each mock, the marks add up to the maximum, question counts per section match the pattern, and internal choices are present.
- **File names**: `<Subject>_Mock_1.pdf`, `<Subject>_Mock_1_Solutions.pdf` and so on, plus `<Subject>_Important_Topics.pdf`.
- **Chat reply**: keep it short. List the files, the papers used (N and sessions), the blind and refined scores, and any limitation the student must know. Don't repeat the PDFs' contents.

## Scoring against the real paper

Two cases end here: a student comes back after their exam, or someone asks you to test the skill on an exam that already happened ("predict CBSE 2026 from 2021–2025 and give me the accuracy"). Past papers and the real paper are public material, so find them yourself rather than asking for uploads.

**Test on a past exam** (one run, nothing to attach)
1. Treat the target exam as upcoming, with the day before it as the cut-off. Use only papers from before it (inside the user's window, if they gave one), plus official sample papers published before it.
2. Run Steps 1–7 blind. Put a pre-target year in every search query, and skip any result about the target paper, its answer key or post-exam analysis. Every predicted question cites the earlier papers it comes from; anything uncited is `[Original]`.
3. Freeze the prediction. Save the PDFs plus `prediction_blueprint.csv` (Mock 1, one row per question: q_no, section, marks, topic, question_type, evidence). Log each file's SHA-256 in `test_log.md`, and send the files to the user before going on.
4. Only now find the real paper, from the official source first. Note its set or shift code; if several sets exist, score each one.

**After the student's own exam**: use the real paper they share, or find it yourself. The prediction must already exist, in this conversation or uploaded. If it doesn't, say so plainly and offer a test run instead. Never generate the prediction now: one made after the exam isn't a prediction.

**Scoring rules** (strict: a doubtful match is a miss, and every number comes from code)
- Count every printed question, including both options of an internal choice, at its printed marks.
- **Type hit**: solved by the same method as a predicted question. **Topic hit**: same topic, different method. Each predicted question matches at most one actual question.
- If you can start a sub-agent, have it do the matching from the frozen files and the real paper only, so the prediction isn't graded by its author.
- Report: a table with one row per actual question (best match, hit type, one-line reason); Mock 1's type hit rate and topic coverage, by marks and by count; all mocks combined; the share of marks from Tier 1 + Tier 2 topics; a section breakdown; and the biggest misses with reasons.
- End with one shareable line, e.g. "Mock 1 matched 78% of the marks by question type; all mocks 91%; Tier 1+2 topics covered 88%."
- If the exam took place before your training cutoff, you may have seen the paper in training. Say the score is likely optimistic and call it a retrospective test. A clean test needs an exam after your cutoff.

## Adapting to the exam

| Situation | What changes |
|---|---|
| Central setter (boards, affiliating universities, national exams) | Usually the most predictable. Official sample papers, mark schemes and blueprints are often published, and the latest official sample usually defines the current pattern. |
| Instructor-set course exams | The instructor matters more than the institution. Weight that instructor's papers most, and use practice exams, homework and lecture emphasis heavily. A new instructor means low confidence; say so. |
| Internal tests in a centrally examined system (class tests, mid-sems) | Use the central end-of-term papers for in-scope units, any past internal papers, and the teacher's hints. Here hints outweigh frequency. |
| Entrance and competitive exams | Many questions, rare exact repeats, several shifts. Predict at concept level: topic-wise weightage is the most valuable output. Expect lower type hit rates. |
| Published question bank or ticket list | Rank the items by likelihood and give model answers for all of them, highest-ranked first. |
| No papers released | Practice papers built from the official outline and practice tests. No backtest and no accuracy claims. |
| Essay-based (humanities, law, social sciences) | Predict themes and question framings. Mocks keep the paper's choice structure (e.g. "answer 3 of 8"), and solutions are model outlines. |
| Oral exams and vivas | The "mock" is a ranked list of likely questions with model answers and likely follow-ups, not a paper. |
| Open-book, take-home or online exams | Expect application and analysis rather than recall. Mirror the platform's question formats. |
| Practical, lab, coding or drawing exams | Predict task types. Give reference solutions, test cases or worked drawings. |

## Never

- Invent a past question, session, source or accuracy number.
- Look for leaked or unreleased papers, or get around a login or paywall.
- Say a question "will definitely come". Give the evidence ("7 of 9 papers") and let the student decide.
- Put out-of-scope topics in a mock.
- Report a refined backtest score without the blind one.
- Do arithmetic in your head when the result goes into a PDF.
