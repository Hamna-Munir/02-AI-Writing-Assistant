# Day 12 — Controlling AI Output

**Objective:** Learn how to control the AI's response — its length, style, and consistency — instead of just accepting whatever it returns by default.

---

## 📖 Theory

### Temperature

Temperature controls how "random" or "safe" the model's word choices are.

- **Low temperature (e.g., 0–0.3)** — the model picks the most likely next word almost every time. Output is more focused, predictable, and repeatable.
- **High temperature (e.g., 0.7–1.0+)** — the model is more willing to pick less-likely words. Output is more varied and creative, but also less consistent between runs.

Rule of thumb: use low temperature for factual/structured tasks (grammar fixing, summarizing), and higher temperature for creative tasks (brainstorming, creative writing).

### Tokens

A **token** is a chunk of text the model reads and generates — roughly ¾ of a word on average in English (short words are often 1 token, longer words can be 2–3). The API has two token-related settings worth knowing:

- **max_tokens** — the maximum length of the response. If set too low, the response gets cut off mid-sentence.
- **Total context length** — the combined size of your prompt + the response, which can't exceed the model's context window.

### Length control

The most reliable way to control response length isn't just `max_tokens` (which can cut a response off awkwardly) — it's *telling the model directly* how long you want the response to be, as part of the prompt. Example: "Answer in exactly 2 sentences" or "Keep the response under 100 words."

### Constraints

Constraints are explicit rules in the prompt that shape the output: word/character limits, required format (bullet points, numbered list, JSON), things to avoid (no emojis, no jargon), or required structure (must include an intro and conclusion).

### Output instructions

Output instructions tell the model exactly what shape the final answer should take — not just *what* to say, but *how* to present it. Being explicit here (rather than assuming the model will "just know") is what makes responses consistent across many requests.

---

## 📚 Reading

[OpenAI: Chat Completions API parameters (temperature, max_tokens)](https://platform.openai.com/docs/api-reference/chat/create) (official docs)

---

## 💻 Coding Exercise

Compare the same prompt at two different settings:

1. **Short response** — low `max_tokens`, explicit instruction like "answer in 1 sentence"
2. **Detailed response** — higher `max_tokens`, explicit instruction like "answer in a detailed paragraph with examples"

Also test the **same prompt at two temperatures** (e.g., 0.2 vs 0.9) and compare how much the output changes if you run it twice at each setting.

```python
# Short vs detailed
short = get_response("Explain overfitting in 1 sentence.", temperature=0.3, max_tokens=60)
detailed = get_response("Explain overfitting in a detailed paragraph with an example.", temperature=0.3, max_tokens=300)

# Low vs high temperature (run each twice to see consistency)
low_temp_1 = get_response("Suggest a tagline for a coffee shop.", temperature=0.2)
low_temp_2 = get_response("Suggest a tagline for a coffee shop.", temperature=0.2)
high_temp_1 = get_response("Suggest a tagline for a coffee shop.", temperature=0.9)
high_temp_2 = get_response("Suggest a tagline for a coffee shop.", temperature=0.9)
```

---

## 🛠️ Today's Feature

The user can now **choose an output style** before generating — Short, Medium, or Detailed — which adjusts both the prompt's length instruction and the `max_tokens` setting sent to the API.

---

## 🧠 Quiz

1. What does temperature control in an AI model's output?
2. Why is telling the model the desired length directly more reliable than relying only on `max_tokens`?
3. What's the difference between a token and a word?
4. When would you want low temperature vs high temperature?
5. What happens if `max_tokens` is set too low for the task?

*(Try answering from memory first, then check the theory section above.)*

---

## ⭐ Bonus

Run the same creative prompt (e.g., "Write a slogan for a bookstore") 3 times at temperature 0.2, and 3 times at temperature 0.9. Compare how similar or different the 3 outputs are at each setting, and note your observation.

---

## 🐞 Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| Response gets cut off mid-sentence | `max_tokens` set too low for the requested length | Increase `max_tokens` or shorten the requested output |
| Output is inconsistent between requests | Temperature set too high for a task that needs consistency | Lower the temperature for structured/factual tasks |
| Length instruction ignored | Instruction is vague ("keep it short") instead of specific | Use a concrete limit ("under 50 words" or "exactly 2 sentences") |

---

## ✅ Checklist

- [x] Understood temperature and its effect on output
- [x] Understood tokens and `max_tokens`
- [x] Compared short vs detailed responses for the same prompt
- [x] Compared low vs high temperature outputs
- [x] Added a Short/Medium/Detailed output style option to the assistant (verified: "Detailed" style on "AI in healthcare" produced a well-structured 3-paragraph response with concrete examples)
- [ ] Bonus: tested temperature consistency across repeated runs
- [ ] Git commit made

---

## 📂 Git Commit

```bash
git commit -m "feat: add output length and temperature control"
```
