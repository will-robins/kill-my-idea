---
name: roast
description: Roast a startup or business idea. It is funny and savage, but every burn is backed by a real, sourced fact, and it ends with the kill-my-idea verdict card. Use when the user says "roast my idea", "roast my startup", "roast <company>", or wants a shareable, funny verdict. Also works on famous companies (for example Juicero or Quibi).
---

# Roast My Idea

A roast is the kill-my-idea verdict told as stand-up. It is shareable on purpose.

## Steps

1. **Research and score** exactly as in
   `${CLAUDE_PLUGIN_ROOT}/skills/kill/SKILL.md`, sections 0–5: the safety rules, the brief,
   the kill-shot checklist, the evidence rules, the metrics and the scorecard. Famous companies need no questions; use public,
   well-documented facts.
2. **Write the roast** to `ideas/<YYYY-MM>-<slug>/roast.md` in this order:
   - the **verdict card** (section 6 of the kill skill), then the badge;
   - **5 burns**: one line each, one fact each, one source link each. Funny comes from the
     fact itself (numbers, quotes, irony), not from insults;
   - **"The one thing that's actually good"**: one honest line;
   - **The fix**: the cheapest test or pivot that could save it, in at most 2 lines;
   - one closing tagline, at most 12 words.
3. **Answer in chat** with the full roast. It must fit in one screenshot: no extra
   sections, no preamble.

## Rules

- Roast the idea, never the person: no looks, identity or private life.
- Facts only. Every burn has a source, and opinions are labelled as opinions.
  This keeps it funny and fair, and stops it from becoming defamatory.
- Real companies and public figures: only public, documented facts.
- Quotes must be verbatim from the linked source. If you can't confirm the exact words, paraphrase without quotation marks.
- Same language as the user.
- Never post anything on the user's behalf.
