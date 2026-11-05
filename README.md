# ai-video-guru

**One Claude skill that makes videos in your own browser with Google Gemini, Google Flow (Veo 3.1) and Google Vids — and remembers your characters so the next video looks like the last one.**

```
/video-guru a chai uncle tells a girl why he never sleeps, Hindi, 30s reel
```

Claude brainstorms the story with you, agrees the cast, locks each character into a reusable library, plans the video as slabs of 8 seconds or less, generates them through your own logged-in Google accounts, assembles them, reviews the result, and tells you honestly what drifted.

No API keys. No local rendering. Your accounts, your credits, your files.

---

## The pipeline

These three tools are not alternatives — they are three layers of one method. Why, with sources: [docs/RESEARCH.md](docs/RESEARCH.md).

| | Tool | Its job | Cost |
|---|---|---|---|
| **1. Identity** | **Gemini** (Nano Banana Pro) | what characters and places *look like* — portraits, 6-panel character sheets, tight ingredient crops | free images |
| **2. Motion + voice** | **Flow / Veo 3.1** | what *happens* — 4/6/8-second shots with in-clip dialogue, lip sync, SFX, camera moves | Flow credits |
| **3. Assembly** | **Vids** | order, captions, music, titles, export — and AI avatars for presenter videos | free tier |

```
brainstorm ─► cast & consistency ─► shot plan (slabs ≤8s) ─► one confirmation
     │              │                      │
     │        Gemini: portrait ─► sheet ─► ingredient crops
     │                                     │
     └───────────────────────────► Flow: one prompt per shot, descriptions verbatim,
                                         dialogue in the prompt, save-frame hand-offs
                                          │
                                   Scenebuilder or Vids: order, trim, caption, music
                                          │
                                   review ─► regenerate the weakest shot ─► deliver
                                          │
                                   cast + sets saved for the next video
```

## The part that matters: consistency

A character is not prompt text you retype. It is a saved artefact:

```
cast/chai-uncle/
  character.json     the frozen description, copied verbatim into every prompt, forever
  portrait.png       the locked identity anchor
  sheet.png          6-panel turnaround, generated from the portrait
  ing-face.png       tight single-subject crops used as Flow ingredients
  ing-full.png
  prompts.md         exactly what made each image
```

Next month, "same uncle, new story" starts at the shot plan — the face is already decided. Three mechanisms do the work, and the skill enforces all three: a locked anchor image, tightly cropped single-subject ingredients, and the **same description word for word** in every shot. Details: [.claude/skills/video-guru/references/consistency.md](.claude/skills/video-guru/references/consistency.md).

## Setup

1. Install and connect the **Claude in Chrome** extension.
2. Allow these sites in the extension's site permissions and sign into each one in that browser: `gemini.google.com`, `flow.google.com`, `vids.google.com`.
3. Open this folder in Claude Code and run `/video-guru`.

That is all. There is nothing to install and nothing to build.

## What it will not do

Type a password · solve a CAPTCHA · accept terms · buy credits or upgrade a plan · generate anything before you say go · spend past the budget it quoted · publish anything anywhere · put a real person's likeness in a video.

And some things the tools genuinely cannot do well, which the skill reshapes with you instead of promising: readable on-screen text from Veo (titles are added in Vids), crowds, vehicles at speed, more than two speaking characters in one 8-second shot.

## Layout

```
.claude/skills/video-guru/
  SKILL.md                    the director — nine steps, in order
  references/
    brainstorm.md             question bank and how to offer three real angles
    consistency.md            the cast library contract and the reuse workflow
    prompting.md              Gemini and Veo 3.1 prompt formulas and syntax
    shotplan.md               slabs, joins, plan.json, manifest.json, credit budgeting
    browser-ops.md            the Gemini / Flow / Vids UI map and the stop conditions
    quality.md                the bar the finished video is checked against
.claude/agents/shot-runner.md optional worker for the long generation loop
cast/<id>/                    your characters — the thing worth keeping
sets/<id>/                    your places
projects/<slug>/              plan.json and manifest.json per video
docs/RESEARCH.md              what was researched, what is official, what to re-verify
docs/PIPELINE.md              the end-to-end walkthrough of one real video
```

## Status

The skill, the references and the library contract are written and ready to run. The Flow UI steps come from Google's Labs help plus public guides from November 2026, not from a live session here — check the first shot carefully, and correct `references/browser-ops.md` wherever the UI has moved.

Only this one route exists on purpose. Other routes — local rendering, hosted APIs — come later, and nothing here is shaped around them.
