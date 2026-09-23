# The Unofficial Guide





> **This file is your submission.** Fill it in as you go — most sections get


> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

Yodahe Kidanu city guide corpus

## What This Does

<!-- Each guide has been broken down by section and embedded as one single block in local storage using all-minilm-l6-v2. Each block is named based on the guide and section name (i.e. “brightwater – getting there”). The system will then retrieve the five nearest blocks when a user asks a question. The system will either refuse answering the question if the best score is above 0.70 or send the retrieved blocks to the model along with an additional grounding instruction. When the model returns an answer, it will identify the source file.

     Milestone 5. -->

## Chunking Strategy

**Chunk size:**
**Overlap:**

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

====================================================================== Chunk 1  |  source: guide_accessibility.md#0  |  produced by: chunker.py::split_documents ====================================================================== Getting around the region with limited mobility An honest assessment rather than a promotional one. Some of these places are difficult and it is better to know in advance. ====================================================================== Chunk 2  |  source: guide_corry_vale.md#5  |  produced by: chunker.py::split_documents ====================================================================== Corry Vale — Where to stay Perhaps thirty beds in the entire valley, spread across two pubs and a handful of farmhouse rooms. In summer these are booked months ahead. Camping is permitted on two marked fields and nowhere else. ====================================================================== Chunk 3  |  source: guide_givens_mill.md#2  |  produced by: chunker.py::split_documents ====================================================================== Givens Mill — Getting around Everything is on one street along the river. The mill is at one end and the church at the other, eight minutes apart. The riverside path continues in both directions for as far as you want to walk. ====================================================================== Chunk 4  |  source: guide_kestrelford.md#5  |  produced by: chunker.py::split_documents ====================================================================== Kestrelford — Where to stay Two inns on the square and a handful of rooms above the pubs. Booking ahead matters between May and September and not at all otherwise. There is no accommodation of any kind within four miles of the town in either direction. ====================================================================== Chunk 5  |  source: guide_pellew_sands.md#7  |  produced by: chunker.py::split_documents ====================================================================== Pellew Sands — Practical notes Cash is still useful at the market and in smaller places, though cards are accepted almost everywhere now. Mobile coverage is good in the centre and patchy on the outskirts. The nearest full hospital is in Brightwater; there is a minor injuries unit locally with limited hours. For each one, ask: could someone answer a question using only this, without reading what came before or after?

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:* What's the recommended way to get around Kestrelford

**Answer:** walking

```
```

**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
| Getting to Brightwater | IN | 0.253 |
| Pellew Sands best time | IN | 0.292 |
| Getting around Kestrelford | IN | 0.375 |
| Halden Bay ↔ Thornby Wells route | IN | 0.305 |
| Least accessible town | IN | 0.609 |


## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

Run it: python app.py ask “what’s the best time to visit Pellew Sands?”


**Moment 1: the chunker.** i had Claude write me a section-based chunker for chunker.py. At that point, Claude had not been exposed to the guides; therefore, it assumed headings were short lines without punctuation at the end and that the title would be indicated by the first line. I ran python app.py chunks and python app.py retrieve to confirm the chunks were labeled appropriately (e.g., kestrelford -- getting around). Therefore, for this specific corpus, its assumptions held true. [note: anything you may have altered or added e.g., chunk_size].

**Moment 2: relevance cutoff.** i pasted in my 10 retrieval scores into Claude and asked for recommendations regarding setting a cutoff. The distances ranged from 0.25-0.61 for real questions and 0.81-0.98 for off topic questions. Claude pointed out that the default of 0.60 would incorrectly reject the wheelchair-access question (0.609) since i asked specifically about “wheelchair users” but the guide states only “limited mobility.” i set the cutoff to 0.70 and also noted that close calls (travel related questions) could potentially slip by the gate.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
