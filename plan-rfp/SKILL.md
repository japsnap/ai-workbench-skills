---
name: plan-rfp
description: Turn a research question into a short research brief (an RFP), and run it when asked, with an agent team sized to the question, saving a clean report with a 400 to 600 word summary into the user's notes folder. Use when the user types /plan-rfp, asks to "park this research", "make this a research question", "research this properly", or asks to run a parked question. Each run also files reports the user has ticked as read.
license: MIT
---

# /plan-rfp: research questions, parked and run cleanly

**概要（日本語）:** 調べたい疑問を、あとで誰でも実行できる短い「リサーチ依頼書（RFP）」にして保存し、頼まれたら深さに合わせたAIチームで調査します。結果は400〜600語（日本語なら約800〜1,200字）の要約付きレポートとしてノートのフォルダに保存され、未読・既読のフォルダで管理されます。途中の作業ファイルは一か所にまとめます。日本語の詳しい説明は README の後半にあります。

**Summary (English):** turns a question into a short research brief (RFP) that any later session can run without asking again, runs it on request with a team of AI agents sized to the question, and saves the result as a report with a 400 to 600 word summary in an unread folder. Reports move to a read folder when the user ticks them. All working files stay in one place.

## First run: set up once
If `<research folder>/_config.md` does not exist, ask these questions, one message, each with a default, and save the answers there:

1. **Where should research live?** Default: a `Research/` folder at the top of the user's notes folder (an Obsidian vault, or any folder).
2. **Which AI tools do you run?** (Claude, ChatGPT, Gemini, others.) Then map them to two roles:
   - **Strong model:** the most capable model available, for planning, judging evidence, verification and writing the final report.
   - **Fast model:** a cheaper, quicker model, for broad searching and gathering.
   If only one model is available, it plays both roles. Record the mapping; the user can change it any time by editing the file.
3. **Language of reports.** Default: the language the user writes in.
4. **Can the agent run several helpers in parallel?** (Claude Code, Codex and similar can; most chat apps cannot.) Default: detect it; if not, run the steps one after another.

Create the folders below if missing.

## Folders (lean: one place for everything)
```
Research/
  _config.md        settings from the first run
  _index.md         one line per question, newest at the top
  questions/        parked research briefs (status: parked)
  unread/           finished reports not yet read, newest first by filename date
  read/             reports the user ticked as read
  _working/         every working file (gatherer notes, scripts, downloads), one subfolder per question; nothing else is left anywhere
```

## Parking a question (the default action)
1. **Check for overlap.** Read `_index.md`. If an existing question covers the same subject, extend that file with a dated addition and say so.
2. **Distill and confirm.** Write the question in the user's own framing, the context a researcher must know (facts already established, so nobody rediscovers them), the scope from obvious to thorough, and the deliverable. Show a short recap; one round of corrections at most.
3. **Ask the depth, with a suggestion.** Suggest one tier and give a reason in one clause ("normal, because the field moves monthly and the answer feeds a decision"). Stakes, speed of change and the need to verify push the tier up.
4. **Write** `questions/<YYYY-MM-DD>-<descriptive-slug>.md` with frontmatter `status: parked`, `created`, `depth`, `models` (the tier recipe below, using the model names from `_config.md`), `what` (one plain line), and the sections Question, Context, Scope, Deliverable, Next actions ("Applicable: no" for curiosity research). Add one line at the top of `_index.md`.
5. **Report** in three lines: the file, the depth, and how to run it ("run <slug>").

Never run the research in the parking step unless the user says to run it now.

## Depth tiers (same logic for every AI tool)
| Tier | Who does what | Rough size |
|---|---|---|
| very light | Strong model alone, a few searches, one pass | a quick answer |
| light | Strong model plans and writes; 1 or 2 fast-model gatherers | an afternoon of reading |
| normal | Strong model plans; 3 to 5 fast-model gatherers in parallel, one per angle; strong model spot-checks the facts the answer rests on and writes the synthesis | the workhorse tier |
| heavy | As normal, plus strong-model helpers on the judgement-heavy angles and a fresh strong-model pass that tries to disprove the main claims | decisions that cost money if wrong |
| deep | A panel: strong-model analysts per angle, fast models for mechanical sweeps, adversarial verifiers and a completeness critic, repeated until two rounds find nothing new | only for expensive, hard-to-reverse decisions |

Without parallel helpers, run the same steps one after another with the same model roles. A run may go about 20 percent over its tier to finish properly; beyond that, wrap up and state what was cut.

## Running a question
1. Move the question's `status` to `running`. Create `_working/<slug>/`.
2. Gatherers write their notes only into `_working/<slug>/`. Every fact gets a date, a primary source (original paper, official page, the company's own announcement, a named news outlet) and a label: **verified** (read at the source), **partly verified** (secondary source or summary), **unverified** (not confirmed; left out of conclusions or marked). Vendor claims are labelled as claims. No invented numbers.
3. For fast-moving topics (AI, prices, laws, platforms), weight the newest sources and give the current date to every gatherer.
4. The strong model spot-checks the two or three facts the answer depends on, then writes **one report** to `unread/<YYYY-MM-DD>-<slug>.md`:
   - frontmatter: `type: research-report`, `question`, `created`, `depth`, `models`, `read: false`;
   - a `- [ ] Read` checkbox on the first line of the body;
   - **Summary (400 to 600 words)** that answers the question standing alone: the verdict, the few things that decide it, the numbers that matter, and what to do next;
   - the full report below it: findings by angle, tables where three or more things are compared, open gaps ("searched, not found"), and a source list.
5. Move the question file to `questions/` with `status: answered` and a dated one-paragraph answer at its end linking the report. Update its line in `_index.md` ("answered <date>").
6. Clean up: everything temporary is inside `_working/<slug>/`; delete downloaded binaries and scripts that are no longer needed, keep the gatherer notes as evidence.
7. **Show the summary in the chat in full**, word for word as written in the report, then one line with the report's path. The full report is for questions the summary does not settle.

## Filing what the user has read (every run)
At the start of any /plan-rfp call (parking or running), check `unread/`: every report whose `- [ ] Read` box is ticked (`- [x] Read`) moves to `read/` with `read: true` and the date. Report the count in one line ("2 reports moved to read/"). Never move an unticked report.

## Writing rules
- Plain language; expand every acronym on first use.
- Each file opens with one line saying what it is.
- Filenames start with the date and say what the research is about, so a stranger could guess the content.
- No filler; a clearly labelled gap beats a confident guess.
- Never install packages or run code downloaded from the web. Scripts the agent writes itself stay and run only inside `_working/<slug>/`.

## Works with /yap
When the user dumps thoughts with /yap and one item is really a question to research, /yap offers to park it here. A finished report can be linked from the idea or opinion note it informs.
