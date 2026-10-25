# exam-paper-predictor

A Claude skill that predicts your next exam paper from real past papers (PYQs, past papers, old exams), and **tests its own predictions on past years** before you trust them.

For any student, anywhere: school boards, universities and colleges, entrance and professional exams, in any language.

**First real test, CBSE Class 12 Maths (March 2026):** the question types it told students to study first (Tier 1 and Tier 2) carried **90.8%** of the real paper's marks, and **66.4%** of the marks were question types that appear somewhere in its top mock paper. Matching the exact paper section by section was much harder: **32.5%**. [Full results](#results)

## What it does

Tell Claude your exam and subject. It will:

1. **Find 5–20 years of real past papers**, from a source you trust or by searching official sources first
2. **Map the exam pattern and topic-wise weightage**, computed in code rather than guessed
3. **Backtest itself**: predict recent past papers without reading them, score each prediction against the real paper, and improve
4. **Predict your upcoming paper** and build your PDFs:

| File | What's inside |
|---|---|
| `Subject_Mock_1.pdf` … `Subject_Mock_N.pdf` | Mock papers in your exam's exact pattern. Mock 1 is the most-likely paper |
| `Subject_Mock_N_Solutions.pdf` | Answer key and full solutions, with the past papers each question type came from. Every number is verified in code |
| `Subject_Important_Topics.pdf` | Topic weightage, must-study tiers, most-expected questions, repeated questions, a revision plan, and a page on how reliable the prediction is |

## How the backtest works

```
Papers:   2014 ………… 2021 │ 2022 │ 2023 │ 2024 │ → your exam
Round 1:  learn ─────────▶ predict 2022 blind → read it → score → improve
Round 2:  learn ────────────────▶ predict 2023 blind → read it → score → improve
Round 3:  learn ───────────────────────▶ predict 2024 blind → read it → score
Final:    learn from everything ──────────────────────────────▶ predict your exam
```

For every test paper it reports two scores:

- **Blind score**: the prediction before it learned anything from that paper. This is the honest estimate of how close your mock will be.
- **Refined score**: the prediction after it improved its method.

The target is 90% at question-type level, meaning 90% of the paper's marks come from question types it predicted. It reports whatever it actually achieves, because some exams don't repeat enough to hit that. In its first real test it reached 32.5% section by section and 66.4% anywhere in the paper ([results](#results)).

## Works for any university, any country

- **Centrally set exams** (school boards, affiliating universities, national exams): it finds the official papers and models how the paper repeats from year to year.
- **Professor-set exams** (most universities in the US, UK, Europe and Australia): it weights your instructor's own past exams, practice exams, homework and lecture emphasis, and flags low confidence when the instructor is new.
- **Any language**: it searches with the local term for past papers (Altklausuren, annales, 過去問, 기출문제, …) and writes the mocks in the paper's language.
- **Any format**: written papers, MCQs with negative marking, essays, case studies, orals and vivas, question banks and exam tickets, and open-book, coding and lab exams.
- **Papers behind a login** (Moodle, Canvas, Blackboard, library archives): download them and upload them in the chat. It never tries to get around a login, and never looks for leaked papers.

## Why it's different

- **No fake past questions.** Every past question is tagged with its session and source. Anything else is clearly labelled `Original` or `Official sample`.
- **Evidence, not vibes.** You get "7 of 9 papers", not "very important".
- **Accuracy is measured, not claimed.** You see the backtest numbers before you study from the mocks.

## Install

### Claude (web or desktop)

Custom skills need a Pro, Max, Team or Enterprise plan.

1. In **Settings → Capabilities**, turn on **Code execution and file creation**.
2. Download `exam-paper-predictor.zip` from the [latest release](https://github.com/YADUNANDAN-SINGH/exam-paper-predictor/releases/latest).
3. In **Settings → Capabilities → Skills**, click **Upload skill**, choose the ZIP, and toggle it on.
4. Keep web search on in your chat so it can find papers.

Use the release ZIP, not GitHub's green "Download ZIP" button. That button adds `-main` to the folder name, and Claude requires the folder name to match the skill name.

### Claude Code

```bash
git clone https://github.com/YADUNANDAN-SINGH/exam-paper-predictor ~/.claude/skills/exam-paper-predictor
```

### On a free plan?

Paste the contents of [`SKILL.md`](SKILL.md) at the start of a chat as instructions. How much works depends on the tools that chat has, such as web search and file creation.

## Use it

Ask normally, in any language. You don't need to mention the skill:

> CBSE Class 12 Physics board exam in March. Make 2 mock papers and tell me the important topics.

> AQA A-level Chemistry in June. Three mock papers with mark schemes, please.

> My Linear Algebra final is in two weeks. My professor posted four old exams on the course site; here they are. What will the final look like?

> Ich habe nächsten Monat die Klausur in Analysis I. Hier sind die Altklausuren der Fachschaft – erstelle mir bitte eine Probeklausur mit Lösungen.

> My university end-sem for Engineering Mathematics-I (code BTAM101-23) is next month. PYQs are on brpaper.com. Make 3 mock papers with solutions.

> NEET: make a predicted paper from the last 10 years and give me chapter-wise weightage.

If you don't say which exam, Claude asks. If you don't name a source for past papers, it finds them itself.

### Test it on an exam that already happened

One prompt runs the whole test. It predicts the paper blind, saves the prediction, then finds the real paper and scores itself:

> Test yourself on CBSE Class 12 Maths 2026: predict it using only the 2021–2025 papers, then find the real 2026 paper and score your prediction.

If the exam happened before Claude's training cutoff, Claude may have seen that paper, so treat the score as optimistic. The clean test is an exam held after the cutoff.

## Results

### CBSE Class 12 Maths, March 2026 (retrospective test)

The prediction used only the 11 board papers from 2022–2025 and CBSE's sample papers up to 2025–26. It was frozen with SHA-256 hashes before the real paper of 9 March 2026 was opened. An independent sub-agent that never saw the prediction labelled the real questions, and the matching was done in code.

Scores on the four clean sets (65/2/1, 65/3/1, 65/4/1, 65/5/1), as a share of the real paper's marks:

| What was measured | Score |
|---|---|
| Question types ranked Tier 1 + Tier 2 in the important-topics PDF | **90.8%** (Tier 1 alone: 52.1%) |
| Mock 1: same question type, anywhere in the paper | 66.4% |
| Mock 1: same chapter, same section | 51.3% |
| Mock 1: same question type, same section (strict) | 32.5% |
| Mock 1 + Mock 2 (before hand edits): same question type, same section | 57.7% |

The skill's own blind backtest, on the July 2025 compartment paper, scored 46.7% strict and 85.0% by chapter.

**What held up:** the study list. The question types it told students to prioritise carried 90.8% of the real marks.

**What didn't:** the exact layout. Mock 1 copied the section layout of CBSE's 2025–26 sample paper, because the method gave that paper 60% of the weight. The 2026 setters moved chapters between sections, for example area under curves as case studies and functions in Sections B and C. A layout based only on past-paper frequency would have scored 43.3% strict.

**Next fix:** place question types by their past-paper frequency, use the sample paper only to confirm what's in scope, and report "anywhere in the paper" next to the strict score.

**Read with care:**

- The model that ran the test was trained on data up to June 2026, after the exam, so it may have seen this paper. Treat every score as likely optimistic.
- About 31 question titles from set 65/1/1 showed up in search results before the prediction was frozen, so the 65/1 series is excluded from the scores above.

Full report, with every per-question match: [`results/cbse-class12-maths-2026.md`](results/cbse-class12-maths-2026.md)

### Add your results

| Exam | Papers used | Blind backtest (strict) | Mock 1 strict | Mock 1 anywhere | Tier 1+2 share | Report |
|---|---|---|---|---|---|---|
| CBSE Class 12 Maths, March 2026 (retrospective) | 11 board papers + sample papers | 46.7% | 32.5% | 66.4% | 90.8% | [report](results/cbse-class12-maths-2026.md) |
| *your exam here* | | | | | | |

Used it for a real exam? After the exam, ask Claude in the same chat to score the prediction. It finds the real paper itself if it's public. Then open an issue with your row.

## Honest limits

- Accuracy is measured separately for each exam by the backtest. It isn't promised.
- Predicting the exact layout, meaning which question lands in which section, is the weakest part so far: 32.5% in the first real test, against 90.8% for the study list.
- Confident predictions need at least 5 years of papers from the same setter. With fewer, it still works but labels the prediction low-confidence.
- A new instructor or a teacher-set class test is hard to predict. Your teacher's hints beat any statistics.
- Some exams never release papers, including some licensing and professional exams. For those it builds practice papers from the official outline and makes no accuracy claims.
- It doesn't host or redistribute papers. It reads them from their sources and links back to them.
- Use the important topics to prioritise your revision, not to skip the syllabus.

## Contributing

Issues and PRs welcome, especially:

- Where to find past papers for a specific board, university or exam
- Local-language search terms that work in your country
- An exam type it handles badly, with an example
- Result rows from real exams

---

Made by [Yadunandan Singh](https://github.com/YADUNANDAN-SINGH). If it helped your exam, a ⭐ helps other students find it.
