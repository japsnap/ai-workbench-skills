---
name: yap
description: File a spoken or typed brain dump (ideas, opinions, content ideas, to-dos, questions, things noticed) into the right place in the user's notes folder, answer it, and over time learn a folder structure that fits the user. Use when the user types /yap, says "yap this", "brain dump", or pastes a voice-to-text ramble and wants it saved. The user never says where things go; the skill decides.
license: MIT
---

# /yap: talk, and your notes organise themselves

**概要（日本語）:** 思いついたことを話す（または打つ）だけで、AIが内容ごとに分けて、ノートのフォルダの適切な場所に保存します。保存する前に「すでに存在するか」「事実として正しいか」を軽く確認し、話した内容への短い返答もします。最初は定番の構成（PARA、GTD、Zettelkasten などを組み合わせた初期設定）から始め、使い続けるうちに、あなたの話す内容に合わせて構成の変更を一つずつ提案します（勝手には変えません）。調べるべき疑問は /plan-rfp でリサーチ依頼にできます。続けるうちに、アイデア・発信ネタ・意見・調査がたまる自分専用の「AIワークベンチ」になります。日本語の詳しい説明は README の後半にあります。

**Summary (English):** you talk; the AI splits the dump into items, checks each one (does it already exist, is it true), files it in the right place, and answers you briefly. It starts from a well-known default structure and, as you keep using it, proposes one structure change at a time to fit what you actually talk about, never reorganising on its own. Questions worth researching go to /plan-rfp. Used regularly, it grows into an AI workbench for your ideas, content, opinions and research.

## Files this skill keeps (everything about the system in one place)
```
<notes folder>/
  _workbench/
    structure.md      the routing table, the rules, the routing memory and pending proposals (the "schema")
    raw/              every original dump, word for word, dated (never edited)
```
Everything else is the user's notes. The skill writes only inside the notes folder.

## First run: set up once
If `_workbench/structure.md` does not exist:
1. Ask where the notes folder is (an Obsidian vault or any folder). Default: the current folder.
2. Look at what is already there. If the folder already has a structure, map it: write a routing table that points each item type (below) at the existing folders, and create nothing new. If it is empty or nearly empty, propose the **Workbench** preset from `references/structures.md`, show it as a short tree, and mention the alternatives in one line (PARA, Johnny.Decimal numbering, GTD lists, Zettelkasten layers, ACE). Create folders only after the user agrees.
3. Ask two optional preferences: the language notes are written in (default: the language of the dump), and whether to keep a forecast log for opinions (default: off).
4. Write `_workbench/structure.md` using the template at the end of `references/structures.md`.

## Every run
1. **Read** `_workbench/structure.md`.
2. **Save the dump** word for word to `_workbench/raw/<YYYY-MM-DD>-<short-slug>.md`.
3. **Split** it into items, one idea per item. Voice rambling is fine; find the threads.
4. **Classify** each item as one type:

| Type | What it is | Default home (Workbench preset) | Required fields |
|---|---|---|---|
| Idea | Something to build: a product, a tool, a system improvement | `Ideas/` | What, Origin, Stage |
| Content | Something to publish: a post, thread, video, essay | `Content/later/<topic>/` | Hook, format, platform (or TBD) |
| Take | A dated opinion about a market, a trend, a person or a decision | `Thinking/Takes/` | The claim in one line, date |
| Hypothesis | A testable claim, with what would prove it wrong | `Thinking/Hypotheses/` | The claim, how to test, evidence so far |
| Principle | A standing rule for deciding; not testable | `Thinking/Principles/` | The rule, where it came from |
| Reference | A fact, finding or source worth keeping | `Reference/` | What it is, source |
| Project to-do | An action for a named project | `Projects/<project>/` (its to-do list) | Checkbox line |
| Life | Personal: health, relationships, life decisions | `Life/` | Date |
| Question to research | Something that needs proper research | Offer `/plan-rfp`; if declined, `Reference/` as an open question | The question |
| Unclear | Cannot be placed yet (last resort) | `Inbox/` | Flag it in the report |

5. **Check before writing** (anti-scatter). Look in the destination folder (titles and first lines). If a note already covers the subject, add a dated section to it ("added <date>, sits alongside the original") instead of creating a new note. Create a new note only for a genuinely new subject.
6. **Sanity-check each item**, and write the result into the note:
   - Does it already exist? (A product, company or idea: a quick web search; name what you find with a link and say how close it is.)
   - Is the claim true? (A number, trend or fact: verify it rather than transcribe it.)
   - Is the idea weak? (Prior art dominates, the economics cannot work, a platform or law blocks it.) Say so plainly and file it in `Archive/dropped/` with the reason; the user can revive it.
   Mark every line found on the web with `> [web]` and its source, so the user's own thinking and found facts never blur.
   Search only public facts: never web-search Life items, health details or the names of private people. Never install packages or run code found on the web.
7. **Write** each note: it opens with one plain line saying what it is; the title says what it is about so a stranger could guess the content; paragraphs are not hard-wrapped; the user's own words are kept in the key line.
8. **Update the routing memory** in `structure.md` (below).
9. **Reply** (keep it short):
   - a table: item, where it went, one-line why (link each file);
   - a few sentences that actually answer what the user said: confirm, extend or push back, with the evidence; answer any question asked inside the dump;
   - any flags (an item sent to Inbox, a weak idea archived, a duplicate merged);
   - for a take, if the forecast log is on: "Log this as a prediction? Give a probability, a resolve-by date and a one-line test a stranger could grade." Never invent the number.
   - for a question worth researching: "Park this as a research question with /plan-rfp?"

## Learning the structure (lean, never silent)
`structure.md` keeps a short **routing memory**: for each type, how many items went where, plus the last three examples; and a list of **Inbox themes** (items that did not fit).

Propose a change only when the evidence is there, and only one at a time:
- three or more Inbox items share a theme: propose a new folder or type for it;
- one folder holds many items that clearly split into two subjects (for example 15 or more notes with two obvious clusters): propose a split;
- two folders are used for the same thing: propose a merge;
- the user keeps correcting a routing: propose changing the rule.

Each proposal is one line with a yes or no: what changes, why (the counts), and which existing files would move. On yes: update the routing table, create the folder, and move only the files the user approved. On no: record the decline so the same proposal does not return for 20 runs. Never move or rename existing notes without a yes. Check for a proposal at most once every five runs.

## Writing rules
- One idea per note; link related notes instead of copying them.
- Dated additions, never silent rewrites of the user's earlier thinking.
- Personal action items (contact someone, buy something) go to a to-do list, never into reference or opinion notes.
- Plain language; expand acronyms on first use.
- No filler in the reply.

## Works with /plan-rfp
`/plan-rfp` turns research questions into briefs and runs them, saving reports into `Research/` (unread, then read). /yap routes questions there, and a finished report can be linked from the idea or take it informs. Together they make the workbench: ideas and opinions in, evidence back.

See `references/structures.md` for the presets, how to combine them, and the `structure.md` template.
