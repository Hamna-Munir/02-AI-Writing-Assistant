# Day 11 — Few-Shot Prompting

**Objective:** Teach the AI a desired behavior by showing it examples, instead of only describing the rules in words.

---

## 📖 Theory

### The problem instructions alone can't solve

Even a very clear instruction can leave room for the AI to interpret things differently than you intended — especially for things that are hard to describe in words, like a specific writing style, a formatting pattern, or a particular tone. Sometimes it's much easier to just *show* the AI what you want, rather than explain it.

### Zero-shot, One-shot, Few-shot

These terms describe how many examples you give the AI before asking it to do the real task:

- **Zero-shot** — no examples at all, just an instruction. Example: "Summarize this text." This is what we've done through Day 10.
- **One-shot** — exactly one example is given before the real request. Example: "Here's an example of a good summary: [example]. Now summarize this text: [new text]."
- **Few-shot** — multiple examples (usually 2–5) are given before the real request, showing a pattern the AI should follow.

### Why examples help

An instruction tells the AI *what* to do. Examples show the AI *how* it should look — the exact style, structure, length, or tone. Few-shot prompting is especially useful when:

- The desired output format is unusual or specific (e.g., a particular JSON shape, a specific tone of voice)
- Consistency matters more than creativity — you want every output to look similar
- The task is hard to describe precisely in a sentence, but easy to demonstrate with an example

### Structure of a few-shot prompt

```
Input: [example input 1]
Output: [example output 1]

Input: [example input 2]
Output: [example output 2]

Input: [the real input you want handled]
Output:
```

The AI reads the pattern from the input → output pairs, then continues that same pattern for the final input.

### Good examples vs bad examples

Examples only help if they're actually representative of what you want:

- **Good examples** are diverse enough to show the *range* of the pattern (not all identical), and clearly demonstrate the exact style/format/tone you want.
- **Bad examples** are inconsistent with each other, too similar to be useful, or accidentally include mistakes the AI might copy.

If your few-shot examples contradict each other in tone or format, the AI's output usually becomes inconsistent too — because it's now unsure which pattern to actually follow.

---

## 📚 Reading

[OpenAI: Few-shot prompting](https://platform.openai.com/docs/guides/prompt-engineering) (official docs — see the "Provide examples" section)

---

## 💻 Coding Exercise

Build a few-shot prompt for the Writing Assistant's tone control. Give the model 2–3 input → output example pairs showing a piece of text rewritten in a specific tone, then ask it to rewrite a new piece of text in that same tone.

```python
few_shot_prompt = f"""
Rewrite text in a persuasive tone. Follow these examples:

Input: Our product saves you time.
Output: Imagine getting hours of your day back — that's what our product delivers.

Input: The app is easy to use.
Output: You'll be up and running in minutes — no manual required.

Input: {new_text}
Output:
"""
```

---

## 🛠️ Today's Feature

The Writing Assistant's output is now **more consistent** across requests — instead of relying only on a tone instruction in words, tone-sensitive modes (like Rewrite and Generate) use a few relevant examples to anchor the style.

---

## 🧠 Quiz

1. What's the difference between zero-shot, one-shot, and few-shot prompting?
2. Why can examples succeed where instructions alone fail?
3. In what situations is few-shot prompting especially useful?
4. What makes an example "bad" for few-shot prompting?
5. What happens if your few-shot examples aren't consistent with each other?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Take one tone (e.g., "Friendly") and write 3 few-shot examples for it. Then test the same rewrite request with **zero-shot** (just an instruction) vs **few-shot** (instruction + your 3 examples), and compare how consistent the tone actually feels in each output.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| Output doesn't follow the example pattern | Too few examples, or examples too different from the real input | Add 1–2 more examples, and make sure they're similar in structure to the real task |
| Output copies an example almost exactly | The real input is too similar to one of the examples | Use a more clearly different real input during testing |
| Prompt gets very long | Too many or too long examples included | Keep each example short — 1–2 lines is usually enough to show the pattern |

---

## ✅ Checklist

- [x] Understood zero-shot vs one-shot vs few-shot
- [x] Understood why examples can succeed where instructions alone don't
- [x] Built a few-shot prompt for at least one tone
- [x] Compared zero-shot vs few-shot output for the same request
- [x] Bonus: tested 3 few-shot examples for the "Friendly" tone — output matched the example pattern naturally ("Hey there! Just a quick heads-up...")
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: add few-shot prompting for consistent tone output"
```
