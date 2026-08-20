# Day 8 — Prompt Engineering Fundamentals

**Objective:** Understand how a prompt actually controls an AI's behavior, and learn to turn a vague prompt into a clear one.

---

## 📖 Theory

### What is a prompt?

A prompt is simply the text you send to an AI model. But a *good* prompt is built from four parts:

- **Instruction** — what you want the AI to do (the task itself).
- **Context** — background information the AI needs to understand the task properly.
- **Input** — the actual data or text the AI should work on.
- **Output format** — how you want the answer shaped (a list, a paragraph, a specific word count, etc.).

Most beginner prompts only include the instruction and skip the other three parts. That's exactly why the output feels random or off-target.

### Why does the prompt control the AI's behavior?

An AI model doesn't "know" what you want — it only has the words you give it to guess from. If your instruction is vague, the model has to fill in the gaps itself, and it usually fills them in a generic way. If your instruction is specific, there's much less room for the model to guess wrong.

Think of it like giving directions to a taxi driver. "Take me somewhere nice" gets you a random result. "Take me to the Italian restaurant on Main Street, near the library" gets you exactly where you meant.

### System instructions vs User instructions

- **System instructions** — set the AI's role, personality, or rules. These usually apply for the *whole* conversation, not just one message. Example: "You are a professional copywriter who writes in a friendly tone."
- **User instructions** — the specific request for *this* particular message. Example: "Write a 100-word product description for a wireless mouse."

Keeping these separate makes the AI's behavior more consistent, because the "rules" (system) don't have to be repeated in every single message (user).

### Clear prompts vs Vague prompts

A vague prompt leaves out details the AI actually needs to do a good job — things like who the audience is, how long the answer should be, or what tone to use. A clear prompt states these details directly instead of hoping the AI guesses correctly.

**Vague:** "Write a post."
**Clear:** "Write a professional LinkedIn post about AI agents, aimed at beginner software engineers."

The difference isn't length — it's specificity. The clear version tells the AI exactly *who* it's writing for and *what* the topic is, so there's almost no guessing left.

---

## 📚 Reading

[OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) (official docs)

---

## 💻 Coding Exercise

1. **Pick 5 bad/vague prompts** — things like "Write a post," "Summarize this," "Fix this text."
2. **Rewrite each one** by adding the missing pieces: audience, format, tone, or length.
3. **Test both versions** in your assistant script and compare the outputs side by side.
4. Save your before/after pairs in this notes file.

### Improved Prompts — Before & After

| # | Bad Prompt | Improved Prompt |
|---|---|---|
| 1 | Write a post. | Write a professional LinkedIn post about AI agents for beginner software engineers. |
| 2 | Summarize this. | Summarize the following article in 3 bullet points, for a non-technical reader. |
| 3 | Fix this text. | Correct the grammar and spelling below, without changing the tone or meaning. |
| 4 | Make it better. | Rewrite this paragraph to be more concise and professional, under 100 words. |
| 5 | Translate this. | Translate this text into formal Urdu, keeping technical terms in English. |

**Pattern I noticed:** every improved version adds the same three things — an audience, a format or length limit, and a tone.

---

## 🛠️ Today's Feature

Added the basic **text generation** feature to the Writing Assistant — the user gives a topic, and the assistant returns a well-structured response using an improved (specific) prompt instead of a raw, vague one.

---

## 🧠 Quiz

1. What are the four parts that make up a good prompt?
2. What's the difference between a system instruction and a user instruction?
3. Why does a vague prompt lead to inconsistent output?
4. Give one example of turning a vague prompt into a clear one.
5. Why might two people get very different answers from the same AI model if they don't write their prompts carefully?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Pick one task (for example, "write a product description") and create **3 different prompt versions** for it. Run all 3 through the assistant and compare which one gives the most consistent, useful result. Note down *why* the best one worked better.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| Output is too generic | Prompt only has an instruction, missing context/format | Add audience, tone, and format details |
| Output length keeps changing | No length/word limit specified | Add a word or sentence limit to the prompt |
| AI ignores part of the instruction | Instruction is too long or contains too many tasks at once | Break the prompt into smaller, clearer instructions |

---

## ✅ Checklist

- [x] Understood the 4 parts of a prompt (instruction, context, input, output format)
- [x] Understood system vs user instructions
- [x] Rewrote 5 bad prompts into clear prompts
- [x] Tested before/after prompts and compared results
- [x] Basic text generation feature added to the assistant (verified via `python -m src.main` → Write mode)
- [x] Bonus: compared 3 prompt variants for one task
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: add basic prompt engineering"
```
