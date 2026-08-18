# Day 9 — System Instructions

**Objective:** Give the AI a consistent personality and behavior, instead of repeating the same rules in every single message.

---

## 📖 Theory

### System instructions vs User instructions (recap + deeper look)

On Day 8 we saw that system instructions set the AI's role and rules, while user instructions are the specific request for one message. Today we go deeper into *how* to actually design good system instructions.

A system instruction usually answers three questions:

- **Who is the AI?** (its role — "You are a professional grammar assistant")
- **What should it always do or never do?** (its constraints — "Never change the meaning of the user's text")
- **How should it respond by default?** (its style — "Always respond in a friendly, concise tone")

Once this is set once, you don't need to repeat it in every user message — the AI keeps following it for the rest of the conversation.

### Instruction hierarchy

When a system instruction and a user instruction conflict, the system instruction generally "wins" — it acts like a set of ground rules the AI shouldn't break, no matter what the user asks in a specific message. This is why system instructions are the right place to put safety rules, tone rules, and formatting rules that must always apply.

Order of priority (highest to lowest):
1. System instructions (the rules that should never break)
2. User instructions (the specific task for this message)
3. The AI's own default behavior (used only when nothing else specifies what to do)

### Role

Giving the AI an explicit role ("You are a professional copywriter," "You are a strict grammar checker") narrows down *how* it should think about every request. Without a role, the AI defaults to a generic, average-sounding assistant voice.

### Constraints

Constraints are the boundaries you set — length limits, tone rules, things to avoid, formatting rules. Example: "Never use emojis," "Keep responses under 150 words," "Do not add information that isn't in the original text."

### Context

Context is background information the AI needs to do the task well but that isn't part of the instruction itself — for example, telling a grammar assistant "the user is not a native English speaker, so explain corrections simply" changes how it responds, even though the task (fix grammar) stays the same.

---

## 📚 Reading

[OpenAI: System Messages / Instruction Following](https://platform.openai.com/docs/guides/text-generation) (official docs)

---

## 💻 Coding Exercise

Build reusable system prompts in `prompts.py` for each mode of the Writing Assistant:

- **Writing Assistant** — generates new content
- **Grammar Assistant** — fixes grammar and spelling only
- **Summarization Assistant** — condenses text into key points

Each one should define: role, constraints, and default tone.

---

## 🛠️ Today's Feature

The user can now **select a mode** before sending their text:

```
1. Write
2. Rewrite
3. Grammar
4. Summarize
```

Each mode loads its own system instruction, so the AI behaves consistently within that mode instead of guessing what's expected each time.

---

## 🧠 Quiz

1. What three questions does a good system instruction usually answer?
2. If a system instruction and a user instruction conflict, which one should generally win?
3. What's the difference between giving the AI a "role" and giving it a "constraint"?
4. Why is context useful even when it doesn't change the actual task?
5. Why is it better to define a system prompt once, instead of repeating the same rules in every user message?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Write a system prompt for a **"Strict Grammar Checker"** persona that only fixes grammar and refuses to change tone, style, or meaning — even if the user asks it to. Test it by asking it (in a user message) to also "make the text sound more exciting," and see if it correctly refuses.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| AI ignores the system prompt | System instruction is too vague or buried inside a long message | Keep it short, direct, and placed as a separate system message |
| AI's tone changes between requests | System prompt not being sent with every request | Make sure `assistant.py` always attaches the mode's system prompt |
| Mode selection doesn't affect output | Wrong system prompt variable being passed in | Double-check the mode → prompt mapping in `prompts.py` |

---

## ✅ Checklist

- [ ] Understood the 3 questions a system instruction should answer
- [ ] Understood instruction hierarchy (system > user > default)
- [ ] Built reusable system prompts for Writing / Grammar / Summarization
- [ ] Added mode selection (1–4) to the assistant
- [ ] Bonus: tested a strict persona that refuses conflicting user requests
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: add system instructions and mode selection"
```
