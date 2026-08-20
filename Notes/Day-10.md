# Day 10 — Prompt Templates

**Objective:** Stop writing a new prompt by hand for every single request — build reusable prompt templates instead.

---

## 📖 Theory

### The problem with hardcoded prompts

On Day 8 and Day 9, prompts were written directly as full sentences inside the code. That works for a demo, but it breaks down fast in a real app — every time the tone, topic, or text changes, you'd have to rewrite the whole prompt string by hand. That's slow and error-prone.

### What is a prompt template?

A prompt template is a prompt with **placeholders** (variables) instead of fixed values. You write the structure once, and then plug in different values each time the assistant is used.

```python
prompt = f"""
Rewrite the following text in a {tone} tone:

{text}
"""
```

Here, `tone` and `text` are variables. The *shape* of the prompt stays the same — only the values change based on what the user provides.

### Why templates matter

- **Consistency** — every request follows the same well-tested structure, instead of a slightly different one each time.
- **Reusability** — one template can serve hundreds of different requests just by changing the variables.
- **Separation of prompt and code** — templates live in `prompts.py`, while `assistant.py` just calls them. This makes prompts easy to update without touching the application logic, and easy to test on their own.

### Variables vs hardcoded text

A hardcoded prompt has everything fixed — the topic, the tone, the format are baked directly into the sentence. A templated prompt keeps the *fixed* parts (instructions that never change) separate from the *variable* parts (things that depend on user input). Good templates make it obvious, just by reading them, which parts are fixed rules and which parts are user-supplied.

---

## 📚 Reading

[Python f-strings documentation](https://docs.python.org/3/tutorial/inputoutput.html#formatted-string-literals) (official docs)

---

## 💻 Coding Exercise

Add tone-based templates to `prompts.py` for the **Rewrite** feature. The template should accept:

- `text` — the text to rewrite
- `tone` — one of: Professional, Friendly, Formal, Simple, Persuasive

Example structure:

```python
def build_rewrite_prompt(text: str, tone: str) -> str:
    return f"""
Rewrite the following text in a {tone} tone. Keep the original
meaning, but adjust the word choice and sentence structure to
match the tone.

Text: {text}
"""
```

---

## 🛠️ Today's Feature

The **Rewrite** mode now lets the user pick a tone before rewriting:

```
Choose a tone:
1. Professional
2. Friendly
3. Formal
4. Simple
5. Persuasive
```

The selected tone is plugged into the reusable template — no new prompt has to be written by hand for each tone.

---

## 🧠 Quiz

1. What is a prompt template, in one sentence?
2. Why is separating prompts from application code a good practice?
3. What's the difference between a "fixed" part of a prompt and a "variable" part?
4. Why does hardcoding every prompt become a problem as an app grows?
5. In the rewrite template above, which two things change between requests?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Build one more template — a **Summarize** template that accepts `text` and a `length` variable (e.g., "3 bullet points" or "1 short paragraph"). Test it with the same text but two different length values, and compare the outputs.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| `KeyError` when formatting prompt | A variable name in `{}` doesn't match the function argument name | Make sure the placeholder name and the parameter name match exactly |
| Tone doesn't seem to change the output | Tone value not actually being passed into the f-string | Print the final prompt before sending it, to confirm the variable was inserted |
| Template prompt looks messy in output | Extra blank lines from multi-line f-strings | Use `.strip()` on the final prompt string before sending it |

---

## ✅ Checklist

- [x] Understood what a prompt template is and why it's useful
- [x] Understood the difference between fixed and variable parts of a prompt
- [x] Built a reusable `build_rewrite_prompt()` template with a `tone` variable
- [x] Added tone selection (1–5) to the Rewrite feature (verified: Friendly tone tested, output matched)
- [x] Bonus: built a Summarize template with a `length` variable (verified: 3 bullet points output, accurate)
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: add reusable prompt templates with tone control"
```
