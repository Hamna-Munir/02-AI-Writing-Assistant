# Day 08 — Prompt Engineering Fundamentals

**Week:** 2 — Prompt Engineering & Reliable AI
**Objective:** Samajhna ke prompt actually AI ke behavior ko kaise control karta hai.

---

## 🎯 Today's Goal

- Prompt engineering ke core building blocks samajhna
- Bad prompts ko identify karna aur improve karna
- Writing Assistant ka basic generation feature start karna

---

## 📖 Topics Covered

### What is a prompt?

A prompt is made up of four components:

| Component | Purpose |
|---|---|
| Instruction | Kya karna hai (the task) |
| Context | Background info AI ko chahiye |
| Input | Actual data/text jis pe kaam karna hai |
| Output format | Response kis shape mein chahiye |

### System vs User instructions

- **System instructions** — AI ka persona/role/behavior define karte hain, poori conversation ke liye persist karte hain
- **User instructions** — har individual request, task-specific

### Clear vs Vague prompts

Vague prompts unpredictable output dete hain kyunki AI ko guess karna padta hai. Clear prompts specify karte hain: audience, tone, format, length, constraints.

---

## 💻 Coding — Improving 5 Bad Prompts

| # | Bad Prompt | Improved Prompt |
|---|---|---|
| 1 | Write a post. | Write a professional LinkedIn post about AI agents for beginner software engineers. |
| 2 | Summarize this. | Summarize the following article in 3 bullet points, focusing on key takeaways for a non-technical reader. |
| 3 | Fix this text. | Correct grammar and spelling in the following text while preserving the original tone and meaning. |
| 4 | Make it better. | Rewrite the following paragraph to be more concise and professional, keeping it under 100 words. |
| 5 | Translate this. | Translate the following text into formal Urdu, preserving technical terms in English where appropriate. |

**Pattern noticed:** har improved prompt mein 3 cheezein add hui — audience, format/constraint, aur tone.

---

## 🧠 New Concepts

- Instruction specificity directly output quality ko affect karti hai
- "Output format" specify karna (bullets, word limit, tone) reduces ambiguity
- Prompt likhte waqt khud se poochna: *agar main ye instruction kisi insaan ko deti, kya wo confuse hota?*

---

## 🛠 Project Progress

Writing Assistant ka **basic generation feature** implement kiya — user topic input deta hai, assistant professional/structured text generate karta hai using an improved prompt template (system + user prompt separation).

---

## ⭐ Bonus — Comparing 3 Prompts for Same Task

**Task:** Generate a short product description for a wireless mouse.

| Variant | Prompt | Observation |
|---|---|---|
| A | "Describe a wireless mouse." | Generic, no target audience, inconsistent length |
| B | "Write a 50-word product description for a wireless mouse, targeting remote workers, in a friendly tone." | Consistent length, clear audience, better relevance |
| C | "As a marketing copywriter, write a 50-word product description for a wireless mouse aimed at remote workers. Highlight comfort and battery life. Friendly tone." | Most consistent and on-brand output — role + constraints + specific features to highlight |

**Takeaway:** adding a role ("As a marketing copywriter") + explicit features to highlight gave the most reliable results.

---

## ❌ Mistakes

- Initially wrote prompts without specifying output length — got wildly inconsistent response sizes
- Forgot to separate system prompt from user prompt in first draft of `assistant.py`

---

## 💡 Lessons Learned

- Vague instructions = vague/unpredictable output, every time
- Being specific about format and audience is more impactful than making the prompt longer
- Comparing prompt variants side-by-side make it obvious which details actually matter

---

## 📝 Homework / Next Steps

- Review Day 9: System Instructions — build reusable system prompts for each assistant mode
- Refactor today's improved prompts into `prompts.py` as reusable templates

---

## 📂 Git Commit

```bash
git commit -m "feat: add basic prompt engineering"
```
