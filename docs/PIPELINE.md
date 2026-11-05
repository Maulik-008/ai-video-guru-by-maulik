# One video, end to end

A worked example of what `/video-guru` actually does. The video: a 30-second Hindi reel, two characters, one set, 9:16.

---

**User:** `/video-guru a chai uncle tells a girl why he never sleeps, Hindi, 30s reel`

### 0. Preflight (no generation)

Claude loads the browser tools in one call, opens a tab, checks `gemini.google.com`, `flow.google.com` and `vids.google.com` are allowed in the extension and signed in, reads the Flow credit balance (say 240), and closes the tabs it opened.

### 1. Brainstorm

Length, aspect and language came from the prompt, so Claude asks only what is missing — tone, and whether this continues anything — then offers three angles:

```
A. The confession      hook: tea poured in the dark, before anyone is awake
                       shape: she asks, he deflects twice, then answers
                       ending: the answer is about his son, not about tea

B. The ritual          hook: the same four actions, done perfectly, in silence
                       shape: her narration over his routine
                       ending: she realises she has been coming here for years

C. The argument        hook: "You are going to kill yourself doing this"
                       shape: a row that turns warm
                       ending: she takes the kettle from him
```

The user picks **A**.

### 2. Cast and consistency

`cast/` is empty, so both characters are new. Claude writes the descriptions and reads them back:

> **chai-uncle** — "a 58-year-old Indian tea seller, stocky build, deep smile lines, salt-and-pepper moustache, thick black-framed glasses, wearing a faded blue kurta with rolled sleeves and a grey shawl over one shoulder". Voice: warm, gravelly, unhurried, Delhi Hindi.
> **riya** — "a 24-year-old Indian woman, slim, shoulder-length hair tied back loosely, round silver earrings, wearing an oversized olive hoodie and jeans, a canvas tote on one shoulder". Voice: light, quick, affectionate.

The user changes "olive hoodie" to "mustard hoodie". Both blocks are now **frozen** — from here they are copied word for word into every prompt, in this video and every future one.

### 3. Shot plan

Thirty seconds becomes four shots, and the dialogue is written to fit:

| Shot | s | Beat | Who | Line (words) | Join |
|---|---|---|---|---|---|
| s01 | 8 | hook | uncle | "Pehli chai hamesha sabse acchi hoti hai." (7) | cut |
| s02 | 6 | setup | riya | "Aap kabhi sote nahi ho kya?" (6) | cut |
| s03 | 8 | turn | uncle | deflects, 12 words | handoff |
| s04 | 8 | payoff | uncle | the real answer, 14 words | — |

Claude shows the user the beats and the lines — not the prompts — and they tighten s04. Then it writes `projects/chai-stall-dawn/plan.json` with the full Veo prompt for each shot, descriptions pasted verbatim, one shared style line.

### 4. One confirmation

> Video: *The first cup* · 30 s · 9:16 · 4 shots
> Cast: 2 new (Gemini images, free) · Set: 1 new
> Flow: 4 clips on Veo 3.1 Fast ≈ 80 credits, +25% for retries ≈ **100**. You have 240.
> Downloads: 7 images + 4 clips → `C:\Users\me\Videos\VideoGuru\chai-stall-dawn`
> Assembly: Vids (captions + music + end card)
> Go?

**User: yes.** That yes covers this run only.

### 5. Ingredients in Gemini (free)

One chat per character. Portrait → user says *that is him* → 6-panel sheet generated **from the portrait** → two tight ingredient crops. Same for Riya. One chat for the set plate: the stall before sunrise, no people in frame.

Everything is saved immediately into `cast/chai-uncle/`, `cast/riya/`, `sets/stall-dawn/`, each with the prompt that made it. Riya's sheet comes back with the wrong earrings and is regenerated once.

### 6. Shots in Flow (credits)

One project, 9:16, ×1, Veo 3.1 Fast. Per shot: attach ingredients (character first, max three) → paste the prompt exactly → approve that one generation → wait → check it.

- **s01** lands clean. 20 credits.
- **s02** puts a second person in the background; regenerated once. 40 credits.
- **s03** is good; its last frame is saved for the hand-off into s04.
- **s04** uses that frame as its start frame, so the motion carries across the cut.

Each clip is downloaded at 720p into the output folder and recorded in `manifest.json`. Spent: 100 credits, exactly the budgeted figure.

### 7. Assemble

Google Vids: the four clips in order, Hindi captions, a soft tabla bed under the dialogue, an end card with the handle. Export to the output folder.

### 8. Review

Against the bar: the hook works, faces hold across all four shots, s02's framing crops Riya's tote. Claude names that as the weakest shot and offers one regeneration — the user says ship it.

### 9. Deliver

> `…\chai-stall-dawn\chai-stall-dawn.mp4` — 30 s, 9:16, 100 credits.
> Problems: s02 regenerated once (extra person); the tote is cropped in s02. Everything else as planned.
> Saved for next time: **chai-uncle**, **riya**, **stall-dawn**. Next video with them starts at the shot plan.

---

## What the second video costs

"Same uncle, he is teaching someone to pour" skips steps 2 and 5 entirely: no Gemini work, no identity decisions, no drift from a re-generated anchor. Brainstorm, plan, generate, assemble — and the face is already right, because it is the same file.

That is the whole point of the cast library.
