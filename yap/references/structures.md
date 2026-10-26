# Structures: proven ways to organise notes, and how /yap uses them

What this page is: the presets /yap can start from, where each comes from, how they combine, and the template for `_kb/structure.md`. Pick one, combine two, or map your existing folders; the routing table is yours to edit.

## What the well-known systems agree on
Across PARA, Johnny.Decimal, Getting Things Done, Zettelkasten, Linking Your Thinking and AI-maintained wikis, seven points recur:
1. **Inbox first.** Capture without deciding; sort later.
2. **Few top-level folders.** PARA has 4, ACE has 3, Johnny.Decimal allows at most 10 areas.
3. **Separate what you act on from what you keep.** Getting Things Done starts every item with "is it actionable?"
4. **Link rather than nest deeply.** Notes connect by links and index pages, not ten-level folder trees.
5. **Review on a schedule.** Systems that people abandon are usually capture without review.
6. **Archive instead of delete.** Finished and dropped things move out of the way but stay findable.
7. **Organise late.** Structure should grow from what you actually store, not be designed up front.

There is no quantified study of which structure people keep using; the evidence is practitioner experience and small qualitative studies. So /yap starts simple and changes the structure only from evidence in your own notes (point 7).

## The presets

### Starter (default)
A blend for a person who talks about ideas, content, opinions and projects.
```
Inbox/                      unclear items, sorted later
Ideas/                      things to build (product, tool, system)
Content/later|now|published/<topic>/   things to publish
Thinking/Takes/             dated opinions
Thinking/Hypotheses/        testable claims, with evidence over time
Thinking/Principles/        standing rules for deciding
Projects/<project>/         one folder per active project, with its to-do list
Reference/                  facts, findings, sources
Research/                   owned by /plan-rfp (questions, unread, read)
Life/                       personal
Archive/                    finished and dropped (Archive/dropped/ for weak ideas, with the reason)
```
How it maps to the classics: Projects is PARA's Projects; Life and Content are PARA Areas; Reference and Research are PARA Resources; Archive is PARA Archives. Inbox is GTD's in-basket and the Zettelkasten "fleeting note" stage. Takes, Hypotheses and Principles are Zettelkasten-style permanent notes: your own thinking, in your own words.
Example routing: "I think more VCs will build their own startups" goes to `Thinking/Takes/`; "an app that reminds me which words I forgot" goes to `Ideas/`; "post idea: why I stopped using streaks" goes to `Content/later/<topic>/`; "call the accountant on Friday" goes to `Projects/<project>/` or `Life/` as a checkbox.

### PARA (Tiago Forte, Building a Second Brain)
`Projects/ · Areas/ · Resources/ · Archives/`. Rule: a project has a goal and an end; an area is a responsibility with no end; a resource is a topic of interest; anything inactive goes to the archive. Choose it if your notes are mostly about getting work done. Criticism: opinions and ideas have no natural home; add `Thinking/` and `Ideas/` from the Starter preset.

### Johnny.Decimal (Johnny Noble)
No fixed names. Up to 10 areas as number ranges (`10-19 Work`, `20-29 Personal`), up to 10 categories in each (`11 Clients`), then numbered items (`11.01`). The reserved area `00-09 System` holds `00.01 Inbox`, `00.03 Templates`, `00.09 Archive` and similar. Choose it if you want every note to have a short address you can say out loud. Composes with any preset: prefix Starter folders with numbers (`10 Ideas`, `20 Content`, `30 Thinking`).

### Getting Things Done lists (David Allen)
`Inbox · Next Actions · Waiting For · Projects · Someday/Maybe · Reference`. These are lists, not necessarily folders. Choose it if most of what you say is tasks. Composes with the Starter preset as to-do lists inside `Projects/` and a `Someday/` folder for ideas you may never act on.

### Zettelkasten layers (Niklas Luhmann; Sönke Ahrens, How to Take Smart Notes)
Three kinds of note rather than folders: fleeting (quick capture), literature (what a source said, in your words) and permanent (your own idea, one per note, linked). Choose it if you write and want ideas to connect. Composes with the Starter preset: Inbox holds fleeting notes, Reference holds literature notes, Thinking holds permanent notes.

### ACE (Nick Milo, Linking Your Thinking)
`Atlas · Calendar · Efforts`: Atlas for knowledge and maps of content, Calendar for anything dated, Efforts for things you work on. An earlier version was called ACCESS. Choose it if you think in maps and link heavily.

### AI-maintained wiki (Andrej Karpathy's LLM wiki pattern, April 2026)
Three layers: raw sources you never edit, a wiki the AI writes and maintains, and a schema file that tells the AI the rules, with an index and an append-only log. /yap follows the same shape: `_kb/raw/` is the raw layer, your folders are the maintained layer, and `_kb/structure.md` is the schema.

## Combining presets
- **Starter + Johnny.Decimal:** number the top-level folders for stable addresses.
- **PARA + Thinking:** keep PARA for work, add `Thinking/` for takes and hypotheses.
- **Existing vault:** map your folders in the routing table; /yap never moves what you already have without a yes.
- **Language:** folder names can be in any language; the routing table is what /yap reads.

## Template for `_kb/structure.md`
```markdown
---
type: kb-structure
preset: starter
created: YYYY-MM-DD
notes_language: same as the dump
forecast_log: off
---

# Knowledge base structure

What this page is: the rules /yap follows to file a brain dump. Edit the routing table to change where things go.

## Routing table
| Type | Folder | Required fields |
|---|---|---|
| Idea | Ideas/ | What, Origin, Stage |
| Content | Content/later/<topic>/ | Hook, format, platform |
| Take | Thinking/Takes/ | Claim, date |
| Hypothesis | Thinking/Hypotheses/ | Claim, test, evidence |
| Principle | Thinking/Principles/ | Rule, origin |
| Reference | Reference/ | What, source |
| Project to-do | Projects/<project>/ | Checkbox |
| Life | Life/ | Date |
| Question to research | Research/ via /plan-rfp | Question |
| Unclear | Inbox/ | flag |

## Routing memory
| Type | Count | Where it went | Last three examples |
|---|---|---|---|

## Inbox themes
(items that did not fit, grouped by theme, with counts)

## Proposals
(pending: one line each, with the evidence; declined: with the date, not to be re-proposed for 20 runs)

## Run log
(date, items filed, proposals made)
```

## Sources
Tiago Forte, PARA (fortelabs.com); Johnny Noble, johnnydecimal.com; David Allen, Getting Things Done (gettingthingsdone.com); Sönke Ahrens, How to Take Smart Notes; Nick Milo, Linking Your Thinking (ACE); Andy Matuschak, Evergreen notes (notes.andymatuschak.org); Andrej Karpathy, LLM wiki gist (April 2026).
