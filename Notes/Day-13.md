# Day 13 — Prompt Evaluation

**Objective:** Learn to test and compare prompts systematically, instead of just writing one prompt and assuming it works. This is one of the most important AI engineering skills — not writing a prompt, but proving it's the right one.

---

## 📖 Theory

### Why evaluation matters

Up to now, prompts were improved based on intuition — a bad prompt "felt" vague, so it was rewritten to be clearer. That works for obvious cases, but for anything going into a real product, intuition isn't enough. Two prompts can both *look* reasonable, but perform very differently once tested against real inputs. Evaluation is how you find out which one actually works — with evidence, not guessing.

### What is evaluation, in this context?

Prompt evaluation means running multiple prompt variants against the *same* set of test inputs, then scoring each variant's outputs against clear quality criteria. The prompt that scores best across the test set — not just on one lucky example — is the one that should go into production.

### Quality criteria

Common criteria used to judge a prompt's output:

- **Accuracy** — is the output factually/functionally correct for the task?
- **Clarity** — is the output easy to understand, well-structured?
- **Consistency** — does the prompt produce similarly-shaped output every time it's run, even with different inputs?

Other criteria can be added depending on the task (tone-matching, length adherence, formatting correctness, etc.).

### Test cases

A test case is one specific input you run through each prompt variant, so you can compare outputs on equal footing. Good test cases should:

- Cover typical, everyday inputs (not just the easiest case)
- Include at least one edge case (unusually short, unusually long, ambiguous, or awkward input)
- Stay the same across all prompt variants being compared — otherwise the comparison isn't fair

### Consistency

A prompt might work perfectly on one input and completely differently on another, even though the task is conceptually the same. Testing across multiple inputs — not just one — is what reveals whether a prompt is actually reliable or just got lucky once.

### Failure cases

A failure case is an input where the prompt's output is clearly wrong, poorly formatted, or ignores an instruction. Documenting *why* a prompt failed (not just that it failed) is what makes the next iteration better — for example, "Prompt A ignored the word limit when the input was very long" is more useful than just "Prompt A failed."

---

## 📚 Reading

[OpenAI: Evaluation best practices](https://platform.openai.com/docs/guides/prompt-engineering) (official docs — see evaluation-related sections)

---

## 💻 Exercise

Pick one task from the Writing Assistant (e.g., Summarize). Write **3 different prompts** for it:

- Prompt A
- Prompt B
- Prompt C

Then run all 3 against the **same 5 inputs**, and score each output.

### Evaluation Table

**Task tested:** Summarize
**Test inputs:** 5 sample paragraphs (4 typical news/article snippets + 1 edge case: the single word "Good.")

| Prompt | Accuracy | Clarity | Consistency |
|---|---|---|---|
| A — plain instruction, no format specified | 4/5 | 3/5 (returned a paragraph, not consistent bullet format) | 3/5 |
| B — "3 bullet points, non-technical reader" | 5/5 | 5/5 (clean, consistent bullets every time) | 5/5 |
| C — role persona + strict constraints | 3/5 | 4/5 (good clarity when it worked) | 2/5 (broke on 2 of 5 inputs) |

**Winner: Prompt B.** It produced exactly 3 clean bullet points on every single input, including the edge case, without ever breaking format or getting cut off.

### What actually happened when I ran this

- **Prompt A** worked but returned a paragraph instead of bullets — inconsistent shape from the other two variants, harder to use in a real UI.
- **Prompt B** was the most reliable — 3 bullets, every time, even on the very short "Good." input.
- **Prompt C** looked the most "well-engineered" on paper (explicit role, explicit constraints), but it actually performed the worst in practice:
  - On **Input 2** (stock market paragraph), the response was cut off mid-sentence ("Energy stocks...") — the longer, more verbose prompt pushed the output past the token limit.
  - On **Input 5** ("Good." — the edge case), the response came back **completely empty**.

---

## 🐞 Failure Case Notes

**Prompt C — Input 5 ("Good.") — empty output.**
Likely cause: the strict "only key facts, no opinions" instruction, combined with an input that has almost no factual content, may have left the model with nothing it judged safe to output. A plain instruction (like B) degraded more gracefully.

**Prompt C — Input 2 — cut off mid-response.**
Likely cause: the added role/persona text made the prompt itself longer, and combined with a longer input, the response exceeded the `max_tokens` limit before finishing.

**Key lesson:** a more elaborate, "smarter-sounding" prompt (C) is not automatically better than a simpler, well-constrained one (B). Evaluation caught a reliability problem that would have gone unnoticed if only one or two normal-looking inputs had been tested. The edge case ("Good.") was the one that actually exposed the weakness — this is exactly why edge cases belong in the test set, not just typical examples.

---

## 🛠️ Today's Feature

Whichever prompt performs best across the evaluation table becomes the **production prompt** — it gets moved into `prompts.py` as the default version used by the actual assistant, replacing any earlier, untested version.

---

## 🧠 Quiz

1. Why is testing a prompt against multiple inputs more reliable than testing it against just one?
2. Name the three quality criteria used in the evaluation table.
3. What makes a good test case, beyond just "a normal example"?
4. Why is documenting *why* a prompt failed more useful than just noting that it failed?
5. What should happen to the prompt that scores worst across the evaluation table?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Deliberately include one "hard" test case in your 5 inputs — something ambiguous, oddly formatted, or unusually long/short. See which of your 3 prompts handles it best, and note what made the difference.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| All 3 prompts score about the same | Prompts aren't different enough from each other to reveal a real difference | Make the variants more distinct (different structure, different level of detail) |
| Hard to score "clarity" objectively | No clear definition of what "clear" means for this task | Write a short rubric first — e.g., "clear = under 3 sentences, no jargon" |
| Best prompt on paper doesn't feel right in practice | Evaluation criteria didn't match what actually matters for the use case | Revisit the criteria — add or reweight based on what the output is actually used for |

---

## ✅ Checklist

- [x] Understood why prompt evaluation matters
- [x] Understood the three core quality criteria (accuracy, clarity, consistency)
- [x] Wrote 3 prompt variants (A/B/C) for one task
- [x] Tested all 3 against the same 5 inputs
- [x] Filled in the evaluation table with scores
- [x] Selected the best-performing prompt as the production version
- [x] Bonus: tested a hard/edge-case input across all 3 variants
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: evaluate prompt variants and ship production prompt"
```
