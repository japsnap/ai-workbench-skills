# AI Workbench Skills: /yap and /plan-rfp

**概要:** 話すだけでアイデアや意見がノートに整理されていく「/yap」と、疑問をリサーチ依頼書にしてAIチームに調べさせ、要約付きレポートとして保存する「/plan-rfp」の2つのスキルです。どちらも Claude Code、OpenAI Codex、Cursor、Gemini CLI など Agent Skills 形式に対応したAIで使え、あなたのノートのフォルダ（Obsidian など）の中だけに書き込みます。使い続けると、アイデア・発信ネタ・意見・調査がたまる自分専用の「AIワークベンチ」になります。

**日本語の説明は下にあります。** (English first, Japanese below.)

---

## English

Two agent skills that turn an AI assistant into a workbench for your thinking.

- **/yap**: you talk (or type) a brain dump; the AI splits it into items, checks each one (does it already exist, is the claim true, is the idea weak), files it in the right place in your notes folder, and answers you. It starts from a well-known structure and learns a better one from what you actually say, proposing one change at a time and never reorganising without your yes.
- **/plan-rfp**: turns a question into a short research brief, runs it on request with a team of AI agents sized to the question, and saves a report with a 400 to 600 word summary into `Research/unread/`. Tick "Read" on a report and the next run moves it to `Research/read/`. All working files stay in one folder.

Used together: /yap catches the ideas and opinions, /plan-rfp brings back the evidence, and both file everything cleanly. After a few weeks you have a workbench of ideas, content plans, dated opinions, hypotheses with evidence, and research reports, all as plain Markdown you own.

### Install
Each skill is a folder with a `SKILL.md` (the [Agent Skills](https://agentskills.io/specification) format). Copy the folder you want into your tool's skills folder:

| Tool | Skills folder |
|---|---|
| Claude Code | `~/.claude/skills/` |
| OpenAI Codex | `~/.agents/skills/` |
| Cursor | `.agents/skills/` or `.cursor/skills/` in your project |
| Gemini CLI | `~/.gemini/skills/` or `~/.agents/skills/` |
| Claude apps | zip the folder and upload it under Skills |

macOS or Linux:
```sh
git clone https://github.com/japsnap/ai-workbench-skills
cp -r ai-workbench-skills/yap ai-workbench-skills/plan-rfp ~/.claude/skills/
```
Windows PowerShell, one line at a time:
```powershell
git clone https://github.com/japsnap/ai-workbench-skills
Copy-Item -Recurse ai-workbench-skills\yap, ai-workbench-skills\plan-rfp $HOME\.claude\skills\
```

### First use
- Starting a skill: in Claude Code type `/yap` or `/plan-rfp`; in Codex type `$yap` or `$plan-rfp`; in other tools ask in words ("yap this: ...", "park this research: ...") and the tool picks the skill. Gemini CLI asks your permission the first time, and Agent Skills may need turning on in its settings.
- `/yap` then talk. On the first run it asks where your notes live and either maps your existing folders or proposes a starter structure (see `yap/references/structures.md`: Workbench, PARA, Johnny.Decimal, GTD, Zettelkasten, ACE, and how to combine them).
- `/plan-rfp` then your question. On the first run it asks where research should live, which AI models you use (a strong one for planning and judging, a fast one for gathering; the same model can do both), and the report language.

### What these skills do and do not do
- They write only inside your notes folder (research goes to `Research/` inside it unless you pick another folder on the first run).
- They search the web when checking a public claim or running research, and label every web-sourced line. Search queries are built from what you said, so they leave your machine. /yap never searches with Life items, health details or the names of private people.
- The AI tool you run the skills in reads your notes, so that provider's privacy terms apply to them. The skills add no other service, install no packages and never run code downloaded from the web.
- Research quality depends on your AI tool's web access; every claim carries a verified, partly verified or unverified label so you can see how solid it is.

### Names used
PARA and Building a Second Brain are by Tiago Forte (Forte Labs). Johnny.Decimal is a trademark of Coruscade Pty Ltd. GTD and Getting Things Done are registered trademarks of the David Allen Company. Linking Your Thinking and ACE are by Nick Milo. Claude Code, Codex, Cursor, Gemini CLI and Obsidian belong to their owners. These names are used only to describe the methods and tools; this project is not affiliated with or endorsed by any of them.

### License
MIT. See `LICENSE`.

---

## 日本語

AIアシスタントを「考えるための作業台」に変える2つのスキルです。

- **/yap（ヤップ）**: 思いついたことを話す（または打つ）と、AIが項目ごとに分け、それぞれを確認し（すでに存在するか、主張は正しいか、アイデアとして弱くないか）、ノートのフォルダの適切な場所に保存して、短く返答します。最初は定番の構成から始め、あなたが実際に話す内容に合わせて、より良い構成を一つずつ提案します。あなたの「はい」なしに整理し直すことはありません。
- **/plan-rfp**: 疑問を短いリサーチ依頼書（RFP）にし、頼まれたら疑問の重さに合わせたAIチームで調べ、400〜600語（日本語なら約800〜1,200字）の要約付きレポートを `Research/unread/`（未読）に保存します。レポートの「Read」にチェックを入れると、次の実行時に `Research/read/`（既読）へ移ります。途中の作業ファイルは一つのフォルダにまとまります。

組み合わせると、/yap がアイデアや意見を受け止め、/plan-rfp が根拠を持ち帰り、どちらもきれいに整理して保存します。数週間で、アイデア、発信の計画、日付つきの意見、検証中の仮説、リサーチレポートがたまり、すべて自分のものとして持てるMarkdownになります。

### インストール
各スキルは `SKILL.md` を含むフォルダ（Agent Skills 形式）です。使うツールのスキル用フォルダにコピーしてください（上の表を参照。Claude Code なら `~/.claude/skills/`）。

### 最初の使い方
- 呼び出し方はツールごとに違います。Claude Code では `/yap` や `/plan-rfp`、Codex では `$yap` や `$plan-rfp`。その他のツールでは「yap this: …」「park this research: …」のように頼むと、AIがスキルを選びます。Gemini CLI では初回に許可を求められ、設定で Agent Skills を有効にする必要がある場合があります。
- `/yap` のあとに話すだけ。初回は、ノートの場所を聞き、既存のフォルダをそのまま使うか、初期構成（Workbench、PARA、Johnny.Decimal、GTD、Zettelkasten、ACE と、その組み合わせ方は `yap/references/structures.md`）を提案します。
- `/plan-rfp` のあとに疑問を書くだけ。初回は、リサーチの保存場所、使っているAIモデル（計画と判断用の強いモデル、情報集め用の速いモデル。同じモデルでも可）、レポートの言語を聞きます。

### できること・しないこと
- 書き込むのはノートのフォルダ（とその中の `Research/`。初回に別の場所を選んだ場合はその場所）だけです。
- 公開された主張の確認や調査のときにWeb検索を使い、Webから得た行には印をつけます。検索語はあなたが話した内容から作られるため、外部の検索サービスに送られます。/yap は「Life」の項目、健康に関する内容、一般の個人の名前を検索に使いません。
- ノートの内容はスキルを動かすAIツールが読み取るため、そのAIの提供元のプライバシー規約が適用されます。スキル自体はそれ以外のサービスを使わず、パッケージのインストールやダウンロードしたコードの実行もしません。

PARA、Johnny.Decimal、GTD（Getting Things Done）などの名称は各権利者のものです。方法やツールの説明のためにのみ使っており、本プロジェクトはいずれの権利者とも提携・承認関係にありません。

### ライセンス
MIT（`LICENSE` を参照）。
