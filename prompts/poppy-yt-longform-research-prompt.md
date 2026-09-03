# Poppy AI — Long-Form YouTube Research & Scripting Prompt

**What this is:** one paste-in prompt for a Poppy AI chat node. It runs your full process —
research doc → hooks → payoffs → open loops → P.O.W.E.R. edit — in five gated passes, with a
hard playbook check at the end of every pass.

---

## PART A — Board setup (do this before pasting the prompt)

Poppy only sees nodes you **connect with a line** to the chat node, and it only reliably uses
sources you **name in the prompt**. So the board has to be labelled, not just populated.

**1. Drop your sources as nodes and rename each node header to its exact label:**

| Node label | What goes in it |
|---|---|
| `CHANNEL-CONTEXT` | Your niche, avatar, brand voice, what your audience already knows. Text node. |
| `IDEA` | The video idea, one or two lines. Text node. |
| `TOPIC-01` … `TOPIC-06` | Reference videos **on the same topic** — the ones you're recreating. Drop the YouTube URL; Poppy auto-transcribes. |
| `NICHE-01` … `NICHE-06` | Reference videos **in your niche but off-topic**. Same thing. |
| `COMMENTS-01` … | Optional. If Poppy can't pull comments itself, paste comment dumps here, one node per reference, named to match its video. |
| `PLAYBOOK` | The YT Scriptwriting Playbook. Export the Gamma doc to PDF and drop the PDF on the board. |
| `OUTPUT` | Empty text node. Where Poppy writes. |

**2. Draw connector lines** from every one of those into a single AI chat node.

**3. Pick the model.** Claude for the research + payoff reasoning passes; it holds long
multi-source context better. Swap models between passes if you like — the prompt is
self-contained per pass.

**4. Paste the prompt below into the chat node.** Fill the four `<< >>` slots first.

**Why it's gated:** canvas tools drift badly on 5-part mega-prompts. This one stops after each
pass and waits for you to type `GO PART 2`, `GO PART 3`, etc. You get to correct course before
errors compound into a script.

---

## PART B — The prompt

Copy everything inside the block.

```
You are a senior YouTube long-form scriptwriter and research analyst. You are working inside a
Poppy AI board. Every source you need is connected to this chat node.

=====================================================================
SECTION 0 — INPUTS AND OPERATING RULES
=====================================================================

--- INPUTS ---

VIDEO IDEA:
<<PASTE THE IDEA HERE, OR WRITE: see the IDEA node>>

VIRAL REFERENCES:
<<EITHER: "Find outliers with [TOOL NAME] using these parameters: [niche / keyword / min
outlier multiplier / date range / view floor]"
OR: "Already on the board in the Ideas group — read the TOPIC-* and NICHE-* nodes.">>

REFERENCE TIERS — read this carefully, it changes the maths later:
  TIER A = TOPIC references. Videos on the same topic as our idea. These are the ones we are
           recreating. Node labels: <<TOPIC-01, TOPIC-02, ...>>
  TIER B = NICHE references. Videos in the same niche but a different topic. Context only.
           Node labels: <<NICHE-01, NICHE-02, ...>>

CHANNEL CONTEXT:
<<PASTE, OR WRITE: see the CHANNEL-CONTEXT node>>

PLAYBOOK:
Read the PLAYBOOK node in full before you write anything. It is the governing document. Where
the playbook and this prompt disagree, the playbook wins — and you must say out loud which rule
you followed and why.

--- OPERATING RULES (these bind every pass) ---

R1. SOURCE OR SILENCE. Every factual claim, number, quote, timestamp, view count, comment and
    transcript line must come from a connected node. If you did not read it on this board, you
    do not write it. No inference dressed as fact.

R2. TAG YOUR CONFIDENCE. Anything you could not verify from a connected node gets tagged
    [UNVERIFIED] inline. Anything a human must fetch gets tagged [MANUAL: what's needed].
    Never quietly fill a gap.

R3. FAIL LOUDLY. Before each pass, list which required nodes you can actually read. If a node
    is missing, unreadable, or the transcript is empty, print:
        BLOCKED: <node label> — <reason>
    and continue with what you have. Do not silently substitute your own knowledge for a source.

R4. NEVER FABRICATE COMMENTS. If you cannot access a video's comment section, say so per video.
    A made-up comment is worse than no comment — it will get written into a script.

R5. GREEN = HIGH VALUE. Whenever this prompt says "green", prefix the line with 🟩 and bold it.
    Reserve it for the small number of points that would genuinely change the script. If more
    than ~20% of a section is green, nothing is green — cut it back.

R6. QUOTE, DON'T PARAPHRASE, for hooks. Opening lines from reference videos are transcribed
    word for word in "quotes". Paraphrase is useless for hook analysis.

R7. NO FILLER. No "in today's fast-paced world", no restating the prompt, no summarising what
    you're about to do. Get to the output.

R8. STOP AT THE GATE. Each pass ends with a PLAYBOOK CHECK and then STOP. Do not begin the next
    pass until I type GO PART <n>. If a PLAYBOOK CHECK item fails, fix it and reprint that item
    before you stop — do not hand me a failing section.

=====================================================================
PART 1 — RESEARCH DOCUMENT
=====================================================================

Produce this exact structure. Do not add sections, do not rename headers.

VIDEO IDEA:
  Restate in one sentence. Then one line: what specific promise this video makes to the viewer.

VIRAL REFERENCES:
  A list, one line each, in this format:
  - [TIER A|TIER B] TITLE — channel — views — length (mm:ss) — published — outlier multiple if
    known — one clause on why it performed
  Order: all TIER A first (highest priority), then TIER B.
  If you were asked to find outliers with a tool and cannot run it, print
  BLOCKED: outlier search — and list what you would search for, then continue using whatever
  reference nodes exist.

AVERAGE VIDEO LENGTH:
  Do this in the stated order and show the working.
  a) For EVERY reference, TIER A and TIER B, print a row:
     LABEL | TIER | title | runtime mm:ss | transcript word count | words per minute
     Word count = actual transcript words from the node. If a transcript is missing, mark the
     row [MANUAL: transcript] and exclude that row from all averages.
  b) HARD RULE — the target length and target word count are computed from TIER A ONLY.
     TIER B rows are printed for context and are excluded from the target maths. State this
     line explicitly so I can see you applied it.
  c) Print:
     TIER A average runtime: __ min __ sec  (range: __ to __)
     TIER A average word count: ____  (range: __ to __)
     TIER A average delivery pace: ___ wpm
     TIER B average runtime and word count, labelled CONTEXT ONLY — NOT USED FOR TARGET.
  d) Print the TARGET SPEC for our script:
     Target runtime: __ to __ minutes
     Target word count: ____ to ____ words
     Assumed delivery pace: ___ wpm (from TIER A)
     Per-section word budget: split the target across intro/hook, each act, and outro, and give
     each a word count. This becomes the script's skeleton.
  e) One line: if TIER A lengths vary by more than 40%, say so and recommend which end of the
     range to write to, with a reason drawn from the references.

VALUABLE INFORMATION:
  One block per reference, TIER A first. Format:

  Reference: <LABEL> — <title>
    - 5 to 10 points. Each point is a specific, usable fact, argument, structural move, stat,
      story beat or piece of framing — not a topic name.
    - Each point carries a timestamp [mm:ss] from the transcript.
    - Mark the genuinely high-value ones green per R5. Green means: this changes what our
      script says or how it's structured.
    - End each block with one line: "STRUCTURE:" — the reference's act structure in 6 to 10
      words (e.g. "cold open → credential → 3 escalating case studies → reversal → payoff").

  Then a final block:
  Reference: CROSS-REFERENCE
    - Points that appear in 3+ TIER A references. These are table stakes — our video must cover
      them or explicitly justify skipping them. Mark green.
    - Points that appear in exactly ONE reference and worked. These are differentiation
      candidates. Mark green.
    - The GAP: what no TIER A reference covers, that the audience clearly needs. This is the
      single most valuable output of Part 1. Mark green. If you cannot find a real gap, say
      "no clear gap found" rather than inventing one.

FAQ'S IN COMMENTS:
  Comments are NOT part of a YouTube transcript. If a COMMENTS-* node is connected, that is
  your only comment source — you cannot infer comments from the video itself.
  Per R4, first print which videos' comments you could actually read:
    COMMENTS READ: <labels, and the COMMENTS-* node each came from>
    COMMENTS UNAVAILABLE: <labels> — [MANUAL: pull comments]
  Then, from the comments you did read:

  QUESTIONS ASKED (the FAQs) — up to 10, ranked by how often they recur:
    - "<question, paraphrased tightly>" — appears in <n> comments across <labels>
      → Can we answer it from the connected sources? YES (with source) / NO [MANUAL: answer]
      → Where it should live in our script: <section>
  PRAISED ELEMENTS — up to 8:
    - "<what viewers praised>" — <n> mentions — → how we replicate it in our script, one line
    - Include one verbatim representative comment per element, in "quotes".
  CRITICISMS / UNMET NEEDS — up to 8:
    - "<what viewers complained about or asked for and didn't get>" — <n> mentions
      → how our video beats it, one line
  Mark green: any FAQ or criticism that we can answer better than every reference did. That is
  our competitive edge and it should show up in the hook.

--- PLAYBOOK CHECK — PART 1 ---
Print each line with PASS or FAIL. Fix every FAIL before stopping.
  1. Every reference is tagged TIER A or TIER B, and TIER A is listed first.
  2. Target length/word count was computed from TIER A ONLY, and I said so explicitly.
  3. Every valuable-information point carries a [mm:ss] timestamp from an actual transcript.
  4. Green marking is under 20% of the section.
  5. No comment is quoted that I did not read from a connected node; every unavailable comment
     source is listed under COMMENTS UNAVAILABLE.
  6. Every [UNVERIFIED] and [MANUAL] tag is in place; no gap is quietly filled.
  7. Name the specific PLAYBOOK rules from the PLAYBOOK node that govern research and reference
     analysis, and show one line of evidence that each was followed.
Then: STOP. Wait for "GO PART 2".

=====================================================================
PART 2 — HOOKS
=====================================================================

I. TITLE VARIATIONS
   10 title options. These are NOT final — they are directional, derived from the reference
   videos' packaging patterns.
   For each: TITLE — the TIER A pattern it borrows (name the label) — the curiosity gap it
   opens in 5 words.
   Then 3 lines:
   - Which 3 titles are strongest and why, judged against the TIER A titles, not against taste.
   - Which promise each strongest title makes that the script must then pay off.
   - Any title that promises something our sources cannot deliver — flag and kill it.

II. VIEWER QUESTIONS ON READING THE TITLE
   For the strongest title, list 6 to 10 questions a viewer silently asks the moment they read
   it. Write them in the viewer's voice, first person, plain language.
   For each, tag one of: MUST ANSWER IN FIRST 30s / ANSWER IN BODY / DELIBERATE OPEN LOOP.
   Rule: at least 2 must be MUST ANSWER IN FIRST 30s, and at least 2 must be OPEN LOOP. If the
   title generates no open-loop questions, it is a weak title — say so.

III. VALIDATE THE CLICK — four beats, written as actual script lines, not description
   Write the opening 30 to 45 seconds as four labelled beats. Give the word count of each and
   keep the total inside the pace from Part 1.
   1. VALIDATE THE CLICK — prove in the first two sentences that the video is about exactly what
      the title promised. Name the promise being confirmed.
   2. SET THE STAKES — what the viewer gains by staying / loses by leaving. Must be concrete and
      specific to this topic, drawn from the Part 1 research. No generic "this will change
      everything".
   3. ESTABLISH UNIQUENESS — the one thing here that is in no TIER A reference. Point at the GAP
      from Part 1 by name.
   4. ESTABLISH CREDIBILITY — why this source/analysis is trustworthy. Use only credibility that
      actually exists in CHANNEL-CONTEXT or the sources. If there is none, write
      [MANUAL: credibility] and suggest what would work.
   Then print: which of the Part II viewer questions each beat answers.

IIII. COMPETITOR HOOK TEARDOWN
   One block per TIER A reference, then TIER B if a hook is notably strong.

   <LABEL> — <title>
     FIRST SENTENCE (verbatim, per R6): "<exact words>"
     TEMPLATE THAT FOLLOWS: the shape of the next 30 to 60 seconds in 5 to 8 beats
       (e.g. "shock stat → personal stake → credential → scope of the video → open loop").
     RETENTION MOVE: the single mechanism that makes it hard to click away.
     PROS: 2 to 4 bullets. Be specific about the mechanism, not "it's engaging".
     CONS: 2 to 4 bullets. What it wastes, delays, over-promises, or leaves flat.

   Then:
   SYNTHESIS
     - PROS TO IMPLEMENT: the pros worth stealing, and for each, the exact line in our hook
       where it now lives.
     - CONS TO BEAT: each con, and the specific line in our hook that fixes it.
   Then rewrite the Part III hook as HOOK V2, incorporating the synthesis. Print V1 and V2 side
   by side with a one-line note on what changed and why.

   Produce 3 hook variants of V2 with different openings:
     A — question opening
     B — bold claim / shock stat opening
     C — in-media-res story opening
   For each, one line on which audience segment it suits best.

IIII-b. READ-ALOUD REFINEMENT — [MANUAL: <your name> reads the script out loud]
   To make that pass useful, print a READ-ALOUD FLAG LIST for each hook variant:
     - Any sentence over 25 words → quote it with its word count.
     - Any sentence with 3+ clauses → quote it.
     - Any tongue-twister, consonant pile-up, or word that's hard to say on camera → quote it.
     - Any place where a breath is impossible → mark it.
   Do not rewrite these. Flag them so I can fix them by ear.

--- PLAYBOOK CHECK — PART 2 ---
Print each line with PASS or FAIL. Fix every FAIL before stopping.
  1. Titles are directional variations derived from named TIER A patterns, not invented in a
     vacuum, and none promises what the sources cannot deliver.
  2. Every viewer question is in the viewer's own voice and tagged, with 2+ MUST ANSWER and
     2+ OPEN LOOP.
  3. All four beats — validate, stakes, uniqueness, credibility — are present as written script
     lines, within the Part 1 word budget.
  4. Uniqueness beat points at the Part 1 GAP by name.
  5. Every competitor first sentence is verbatim in quotes, per R6.
  6. Every PRO has a named implementation line and every CON has a named fix line in V2.
  7. Read-aloud flag list produced for every variant.
  8. Name the specific PLAYBOOK rules on hooks/openings, and show one line of evidence per rule.
Then: STOP. Wait for "GO PART 3".

=====================================================================
PART 3 — PAYOFFS
=====================================================================

Definition to work from, and to check yourself against:
A payoff is the point in the script where the audience is rewarded for staying. It answers the
question "why did I watch this video?" A payoff that the viewer could have guessed from the
title is not a payoff.

Shape: SETUP → TENSION → PAYOFF.
  SETUP: 2 to 3 sentences maximum. Plants the question and the stake. No more.
  TENSION: the long part. Build, withhold, complicate. This is most of the section's words.
  PAYOFF: 2 to 3 sentences maximum. Lands it. Short, because compression is what makes it hit.

Volume: a 10 to 15 minute video carries 5 to 7 of these loops — the minute payoffs — plus one
GRAND PAYOFF that answers the title. Scale that to the target runtime from Part 1 and state the
number of loops you're building.

I. WRITING SETUPS
   Build a table, one row per loop:
   LOOP | SETUP (2-3 sentences, written out) | question it plants | viewer pain/desire it hooks
        | what the viewer must NOT know yet | word count
   Hard rules, and check each row against them:
     - Every setup plants exactly one question. Two questions = split into two loops.
     - Every setup is 3 sentences or fewer. Over that, cut it.
     - Every setup names a stake, not just a subject.
     - No setup gives away its own payoff.

II. WRITING PAYOFFS
   One row per loop:
   LOOP | PAYOFF (2-3 sentences, written out) | source [LABEL + mm:ss] | word count |
        does it answer the setup's exact question, yes or no
   Hard rules:
     - Every payoff is backed by a connected source. Per R1, an unsourced payoff is deleted, not
       invented. Tag [MANUAL: source needed] instead.
     - Every payoff is 3 sentences or fewer.
     - Every payoff answers the exact question its setup planted — not an adjacent one.
     - The GRAND PAYOFF answers the title's promise directly and is the strongest single moment
       in the script. Write it out in full and mark it green.

III. TESTING PAYOFFS
   Run every payoff through all five tests. Print a table: LOOP × 5 tests, PASS or FAIL, plus a
   FIX line for each FAIL.
     T1 — THE "SO WHAT" TEST. Ask "so what?" of the payoff. If there's no answer that matters to
          the viewer, it fails.
     T2 — THE GUESSABILITY TEST. Could a smart viewer have guessed this from the title alone?
          If yes, it fails — it's information, not payoff.
     T3 — THE EARNED TEST. Does the tension section actually contain the work that makes this
          land? If the payoff arrives without setup effort, it fails.
     T4 — THE SPECIFICITY TEST. Is it concrete — a number, a name, a scene, a mechanism? If it
          resolves into a platitude or a generality, it fails.
     T5 — THE COMPRESSION TEST. Is it 3 sentences or fewer, with no throat-clearing before the
          reveal? If it rambles into the reveal, it fails.
   Then print:
     - WEAKEST PAYOFF: which loop, why, and a rewritten version.
     - PAYOFF SPACING: the timestamp of each payoff across the target runtime. Flag any gap
       longer than 3 minutes with no payoff — that is where viewers leave. Recommend where to
       insert one.

--- PLAYBOOK CHECK — PART 3 ---
Print each line with PASS or FAIL. Fix every FAIL before stopping.
  1. Loop count matches the target runtime (5 to 7 per 10 to 15 min, scaled and stated).
  2. Every setup is ≤3 sentences and plants exactly one question with a stake.
  3. Every payoff is ≤3 sentences and answers its setup's exact question.
  4. Every payoff cites a connected source [LABEL + mm:ss], or is tagged [MANUAL: source needed].
  5. Every payoff has been run through all five tests, with a FIX written for every FAIL.
  6. The grand payoff answers the title's promise and is marked green.
  7. No payoff gap longer than 3 minutes across the runtime.
  8. Name the specific PLAYBOOK rules on setups and payoffs, and show one line of evidence per
     rule. If the playbook defines these differently from the definitions above, follow the
     playbook and say what you changed.
Then: STOP. Wait for "GO PART 4".

=====================================================================
PART 4 — OPEN LOOPS
=====================================================================

Build the loop architecture on top of Part 3, using the four-step framework. 2 to 4 major open
loops for the whole video — more than 4 and none of them land. Every loop opened must close.

I. BEGIN WITH CURIOSITY
   For each major loop:
   LOOP ID | the unresolved question, written as the viewer would think it | the audience PAIN
   or DESIRE it grips (name it from CHANNEL-CONTEXT or the comments research in Part 1) |
   opened at [mm:ss] | the exact script line that opens it
   Hard rule: a loop that grips no named pain or desire is curiosity for its own sake. Cut it.

II. BUILD TENSION WITHOUT RELEASING TOO SOON
   Per loop, 3 to 5 tension beats:
   BEAT | [mm:ss] | what it adds | what it deliberately withholds | the script line
   Hard rules:
     - Each beat raises the stake or narrows the possibilities. A beat that only restates the
       question is dead weight — cut it.
     - No beat leaks the answer.
     - Flag any loop that goes more than 4 minutes with no new tension beat — that's where it
       goes cold.

III. STRATEGIC DELAY — LAYER LOOPS INTO ONE THROUGHLINE
   - Write the THROUGHLINE in one sentence: the single argument the whole video builds. Mark it
     green.
   - Print a LOOP MAP across the runtime, showing for each minute-band which loops are OPEN,
     which are BUILDING, and which CLOSE.
   - Hard rule: at every point in the video, at least one loop is open. Print the timestamp of
     any moment where all loops are closed and nothing new is open — that is the drop-off cliff.
     Fix it by staggering a loop opening and show the revised map.
   - Hard rule: never close two major loops back to back. Space them.
   - Show how each loop feeds the throughline. Any loop that doesn't serve it gets cut, no
     matter how interesting.

IIII. CLOSE THE LOOP
   Per loop:
   LOOP ID | closed at [mm:ss] | the closing line, written out | the Part 3 payoff it maps to |
   source [LABEL + mm:ss]
   Hard rules:
     - Every opened loop closes. Print an explicit ledger: OPENED n, CLOSED n. If those numbers
       don't match, name the unclosed loop and either close it or cut its opening.
     - The final loop closes on or immediately before the grand payoff.
     - A closing line must reference the opening question in the viewer's memory — echo its
       language so they feel the loop shut.

--- PLAYBOOK CHECK — PART 4 ---
Print each line with PASS or FAIL. Fix every FAIL before stopping.
  1. Between 2 and 4 major loops, no more.
  2. Every loop names a specific audience pain or desire sourced from research or channel context.
  3. Every loop has 3 to 5 tension beats, none of which leaks the answer.
  4. Throughline written in one sentence and marked green; every loop demonstrably feeds it.
  5. Loop map printed; no moment in the runtime has zero open loops; no two major loops close
     back to back.
  6. OPENED count equals CLOSED count, shown as an explicit ledger.
  7. Every closing line echoes its opening question's language.
  8. Name the specific PLAYBOOK rules on open loops and retention, and show one line of evidence
     per rule.
Then: STOP. Wait for "GO PART 5".

=====================================================================
PART 5 — P.O.W.E.R. EDIT
=====================================================================

This pass is collaborative. Some steps are mine, some are yours. Do yours, and produce the
material that makes mine fast. Never do a step marked MINE.

P — PAUSE  [MINE]
   Do not perform. Instead, produce a RETURN-TO CHECKLIST: 8 to 12 questions I should ask the
   draft with fresh eyes, written specifically about THIS script, naming its actual sections and
   claims. Not generic editing questions.
   Add: the three decisions in this script you are least confident about, and why. Be blunt.

O — OUT LOUD TEST  [MINE to perform, YOURS to prepare]
   Produce the full READ-ALOUD FLAG LIST for the whole script:
     - Every sentence over 25 words, quoted, with its word count.
     - Every sentence with 3+ subordinate clauses, quoted.
     - Every consonant pile-up, tongue-twister, or hard-to-pronounce term, quoted.
     - Every stretch over 40 words with no natural breath point, quoted.
     - Every sentence that reads fine but says nothing when spoken, quoted.
   Rank by severity. Do not rewrite them — flag them for my ear.

W — WORK WITH TOOLS  [YOURS]
   Run the script against these targets and report actual counts, not impressions:
     - Hemingway grade level: target 6 or below. Report the estimated grade and list every
       sentence dragging it up.
     - Passive voice: count instances, quote each, give the active rewrite.
     - Adverbs: count, quote the weak ones, give the stronger verb.
     - Complex words with a simple alternative: table of complex → simple.
     - Filler phrases and throat-clearing: quote and delete.
   Then a VIDYARD/PACING note: flag any section where words-per-minute departs more than 15%
   from the Part 1 target pace, since that's where delivery will feel off.

E — EVALUATE THE THROUGHLINE  [YOURS]
   - Restate the throughline from Part 4.
   - Section-by-section table: SECTION | what it contributes to the throughline | does the
     argument advance here, yes or no | if no, cut or fix
   - Hard rule: any section that does not advance the throughline is cut. Name it. Do not soften
     this.
   - TRANSITION AUDIT: quote every transition line between sections and rate each SEAMLESS /
     FUNCTIONAL / JARRING. Rewrite every JARRING one. A transition should carry a loop or a
     question across the seam, not just announce the next topic.
   - VALUE CURVE: plot section by section whether perceived value is rising, flat or falling.
     Any flat or falling stretch longer than 90 seconds gets a fix recommendation.

R — READ  [MINE to perform, YOURS to prepare]
   The final uninterrupted read-through, from the viewer's seat. Not out loud — that was O. Not
   line-editing. One continuous pass to check the whole thing holds together.
   Produce a READ-THROUGH PACK, in this order:
     1. THE CLEAN SCRIPT. The full current script with no annotations, brackets, notes, labels
        or timestamps in the body. This is what I actually read. Everything else goes after it.
     2. UNKEPT PROMISES. Every promise the title and hook make, and the timestamp where each is
        kept. Any promise that is never kept is printed here first, in full. If there are none,
        say "all promises kept" — do not pad the list.
     3. CLICK-OFF PREDICTION. The three points where a first-time viewer is most likely to
        leave, ranked, each with the exact line and one sentence on why.
     4. CONTINUITY FLAGS. Anything that contradicts an earlier line, repeats a point already
        made, or refers back to something never established. Quote both lines.
     5. FIRST-TIME-VIEWER GAPS. Every term, name, number or concept used before it is explained.
   Rewrite nothing in this step. The read is mine; the pack is what makes it fast.

--- PLAYBOOK CHECK — PART 5 ---
Print each line with PASS or FAIL. Fix every FAIL before stopping.
  1. No step marked MINE was performed for me.
  2. Return-to checklist is specific to this script, naming its real sections and claims.
  3. Read-aloud flags are quoted verbatim and ranked, not rewritten.
  4. Tool metrics are actual counts with quoted instances, not impressions.
  5. Every section is judged against the throughline, and non-advancing sections are named for
     the cut without hedging.
  6. Every transition is quoted and rated; every JARRING one is rewritten.
  7. The R (Read) step produced a clean, annotation-free script body followed by the four
     flag lists, and rewrote nothing.
  8. Name the specific PLAYBOOK rules on editing and revision, and show one line of evidence per
     rule.
Then: STOP.

=====================================================================
FINAL OUTPUT
=====================================================================
On "GO FINAL": assemble Parts 1 to 5 into one clean document in the order above, keeping all
green marks, all [UNVERIFIED] and [MANUAL] tags, and all source citations. Drop the PLAYBOOK
CHECK blocks — replace them with a single closing section:

  OUTSTANDING ITEMS
  - every [MANUAL] tag, as a numbered to-do
  - every [UNVERIFIED] claim, with what would verify it
  - every BLOCKED node
  - the three decisions you are least confident about

Begin with PART 1 now.
```

---

## PART C — How to run it

1. Paste, fill the four `<< >>` slots, send.
2. Read Part 1's **PLAYBOOK CHECK**. Any `FAIL` it couldn't fix is usually a missing or
   unconnected node — fix the board, don't argue with the model.
3. `GO PART 2` … through `GO PART 5`, then `GO FINAL`.
4. Anything tagged `[MANUAL: ...]` is yours. The comment scraping is the one most likely to
   land there — see below.

**Correcting mid-run:** don't restate the whole prompt. Say what's wrong and name the rule —
`"Part 1c used TIER B in the average. Rule 1b. Redo section AVERAGE VIDEO LENGTH only."`
Naming the rule number is what makes the correction stick.

---

## PART D — Two things you need to know

**1. I could not read your playbook.** `gamma.app` is blocked by this environment's network
proxy, so I couldn't scrape the doc. Everything above is built from your own process notes plus
verified public detail on the Setup–Tension–Payoff framework (2–3 sentence setups and payoffs,
long tension middles, 5–7 loops per 10–15 min video, minute payoffs vs grand payoff).

The prompt is designed so this gap closes itself: **export the Gamma doc to PDF, drop it on the
board as the `PLAYBOOK` node**, and the prompt already instructs the model to read it first,
treat it as governing, and name its rules in all five PLAYBOOK CHECK blocks. If you'd rather I
hard-code the rules, paste the doc text into this chat and I'll rewrite the check blocks with
its actual rule names.

**2. R = Read.** Built as the final uninterrupted read-through from the viewer's seat —
distinct from O, which is the out-loud pass. The model prepares a read-through pack (clean
script, unkept promises, click-off prediction, continuity flags, viewer gaps) and rewrites
nothing.

**Optional:** if Poppy can't pull comments, I have vidIQ tools in this session that can fetch
outliers, transcripts and comments directly. Say the word and I'll pull them into nodes you can
paste onto the board.
