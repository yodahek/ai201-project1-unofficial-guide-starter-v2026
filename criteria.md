# Acceptance Criteria

## 1. Retrieval finds the answer
For at least 4 of my 5 test questions, the retrieved chunks include one
that contains the answer.

**Why 4 of 5:** Each chunk is one section of one guide, so a town-specific
question should pull back the right section. But at least one of my questions
depends on a cross-cutting guide (transport, seasons, accessibility) whose
topic is also mentioned briefly in individual town guides, so those can crowd
out the right chunk. 5 of 5 would assume that overlap never matters; 3 of 5
would accept retrieval failing on a town question, which the chunking should
prevent.

## 2. Every answer names a source
Every answer the system produces (i.e. every question that passes the
relevance gate) names at least one source document by filename.

**Why every one:** Citing sources is a required feature and the grounding
instruction asks for it explicitly. A missing citation is a bug, not a tuning
tradeoff, so there's no reason to allow misses. Refusals from the gate are
excluded because there's nothing to cite.

## 3. The gate refuses off-topic questions
When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about
that" — in at least 4 of 5 tries.

**Why 4 of 5:** Some out-of-scope questions share vocabulary with travel
guides (weather, food, prices) and may land closer than expected. Demanding
5 of 5 would push me to set the cutoff so low that it starts refusing real
questions, which is the worse failure for a guide people are supposed to use.

## 4. Chunks are the right size and stand alone
No chunk produced by `chunker.py::split_documents` is shorter than 200
characters or longer than 1,500 characters, and in a random sample of 10
chunks, at least 8 begin with their guide title and section heading and can
answer a question without reading the chunks around them.

**Why these numbers:** 200 is my merge threshold, so any shorter chunk means
the merge step failed. 1,500 allows my 1,200-character section limit plus the
heading prefix and a folded-in short section; anything past that means a
section wasn't split. 8 of 10 rather than 10 of 10 because a few guide
sections are genuinely short or list-like and may lean on context even when
merged correctly.

## 5. Answers are correct and cite the right file
For at least 4 of my 5 test questions, the answer contains that question's
`expects` phrase and cites the file the phrase actually appears in.

**Why 4 of 5, and why both conditions:** A correct fact with the wrong
citation can't be trusted or checked, so the two have to pass together. I
allow one miss because the cross-cutting guides repeat details from town
guides, and citing the other file that mentions the same fact is a
reasonable near miss. 3 of 5 would mean the system is wrong or unverifiable
almost half the time.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
<!-- e.g. "One of my questions is about a topic only two documents mention, so
     I expect that one to be hard." -->

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
<!-- Why all five and not four? What about your setup makes that achievable —
     or what would have to go wrong for it not to be? -->

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

---

## 4. Something about your chunks

<!-- YOU WRITE THIS ONE.

     How would you know if your chunks were the right size? Name something
     countable or observable.

     Examples of the right shape — don't copy these, they should come from
     what you actually saw in Milestone 3:
       - "At least 4 of 5 sampled chunks read as a complete thought, with no
          sentence cut in half at either end."
       - "No chunk is shorter than 200 characters, since anything below that
          in my corpus turned out to be a heading with no content under it." -->



**Why this target:**



---

## 5. Your choice

<!-- YOU WRITE THIS ONE TOO.

     Pick something you actually care about getting right. It could be about
     speed, about refusals, about a particular kind of question your corpus
     handles badly, about source attribution being correct rather than merely
     present — anything, as long as it names a number or an observable
     outcome. -->



**Why this target:**



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
