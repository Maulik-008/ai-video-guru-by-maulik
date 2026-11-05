# Research: the best way to make great, consistent videos with Gemini + Flow + Vids

Done 2026-11-05. Everything below is either from Google's own documentation or marked as third-party and to be verified in the account before it is relied on.

## The finding that shapes everything

**These three tools are not alternatives. They are three layers of one pipeline.**

| Layer | Tool | What it is genuinely best at | Cost |
|---|---|---|---|
| **Identity** | Gemini (Nano Banana Pro / Gemini 3 Pro Image) | Locking what a character, set and prop *look like*, as reusable reference images | Images are free in Flow; Gemini app usage is on your plan |
| **Motion + voice** | Google Flow (Veo 3.1) | Turning those references into 4/6/8-second shots with in-clip dialogue, lip sync, SFX and camera moves | Flow credits per clip |
| **Assembly + finish** | Google Vids | Timeline editing, captions, music (Lyria 3), voiceover, avatars, export — without any local tooling | Free tier, 10 Veo generations/month on personal accounts |

Trying to do identity in Flow gives drifting characters. Trying to do motion in Gemini is impossible (it is image-only). Doing assembly by hand is slow. The pipeline is **Gemini → Flow → Vids**, and the whole skill is built on it.

## What Veo 3.1 actually gives us (Google's own prompting guide)

- **Prompt formula:** `[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance]`.
- **Clip length: 4, 6 or 8 seconds.** Resolution 720p or 1080p. Aspect 16:9 or 9:16 — vertical is native, so a reel never needs cropping. Everything carries a SynthID watermark.
- **Dialogue is in-clip, with lip sync**, written into the prompt itself:
  - `A woman says, "We have to leave now."`
  - `SFX: thunder cracks in the distance`
  - `Ambient noise: the quiet hum of a starship bridge`
- **Ingredients to Video** is the official consistency mechanism: generate reference images for each character and the setting, then reference them *by role* in every shot prompt — "Using the provided images for the detective, the woman, and the office setting, create a medium shot of…". One shot per prompt.
- **First-and-last-frame** gives controlled transitions: make the start frame and the end frame as images, hand Veo both, and describe the move between them.
- **Timestamp prompting** can put several beats inside one 8-second generation: `[00:00-00:02] … [00:02-00:04] …`. Cheaper than four separate clips when the beats are tight.
- **Negative prompts do not work as negations.** Describe what *should* be there ("a desolate landscape with no buildings") rather than "no buildings".
- Add/remove object runs on Veo 2 and produces **no audio** — never use it on a dialogue shot.

## How length beyond 8 seconds actually works (Google Labs help)

- **Extend** continues a clip generatively, and Google's own announcement says chains can reach a minute or more. Each extension is generated **from the final second of the previous clip**, so drift compounds — it is for continuous action, not for a new beat.
- **Only Veo-generated clips can be extended**, and insert / remove / camera edits cannot be applied to extended clips.
- **Save frame** (pause on a frame → Save frame) stores a still that can then be used as an ingredient, a start frame or an end frame. This is the cleanest hand-off between consecutive shots.
- **Scenebuilder** is where shots become a sequence: More → Add to Scene, drag to reorder, trim each clip's start and end, preview, download the scene.
- Third-party guides report that an older Extend button could fall back to Veo 2 Fast — check the model on the clip before extending.

**Conclusion for us:** a reel is a *stack of shots* ("slabs"), not one long generation. Continuity comes from ingredients + verbatim descriptions + last-frame hand-off, not from Extend. Extend is reserved for a single action that must not cut.

## How character consistency is actually achieved

Three mechanisms, used together — this is the heart of the skill:

1. **A locked identity anchor.** One chosen portrait first, then a multi-angle character sheet generated *from it*. Nano Banana Pro blends up to 14 reference images and holds up to 5 distinct subjects. Typical sheet: six panels on a clean neutral background — front, 3/4, side, back, face close-up, mid-shot.
2. **Tightly cropped, single-subject ingredient images.** A busy background or a second person in frame confuses the model about which part is the ingredient. One subject per image, cropped tight. Most important ingredient (usually the character) first; third-party guides report a practical limit of about **three ingredients per shot**.
3. **Verbatim repetition of the description.** The same character description, word for word, in every shot prompt. Google's Vertex guidance makes the general point that the character description is the foundation of consistency, and recommends giving the character a name and a specific voice style for reuse. Third-party guides go further and call word-for-word repetition a hard rule; their percentage claims are unverified, but every source points the same way.

Consistency does **not** carry over automatically: a sheet is a reference you feed in, never a guarantee. Expect to regenerate — one published test held identity in only two of four sheets.

**Conclusion for us:** characters must be *saved artefacts*, not prompt text retyped each time. That is the cast library.

## What Google Vids adds

- Browser timeline editor: describe a video and it drafts a script, pulls stock, suggests music, assembles.
- **Veo 3.1 generation inside Vids** (10 free generations a month on personal accounts), from text or a photo.
- **AI avatars** powered by Veo 3.1 that keep the same face and voice across scenes — a ready-made consistency mechanism for presenter-style videos, with no cast library needed.
- **Voiceover on the free tier**, AI music via Lyria 3, slides-to-video.
- Sources disagree on language counts (7 / 8 / 24) and on plan limits — verify in the account.

**Conclusion for us:** Vids is the finishing line (assemble, caption, music, export), and the right *generator* only for presenter and explainer videos, where its avatars beat anything we could keep consistent ourselves.

## The method we adopt

```
brainstorm ─► cast & continuity ─► shot plan (slabs of ≤8s) ─► one confirmation
   │                │                      │
   │           Gemini: portrait ─► sheet ─► tight ingredient crops          (free)
   │                                        │
   └──────────────────────────────► Flow: ingredients-to-video, one prompt per shot,
                                          verbatim descriptions, dialogue in prompt,
                                          save-frame hand-off between shots        (credits)
                                            │
                                     Scenebuilder: order, trim, download
                                            │
                                     Vids: captions, music, titles, export
                                            │
                                     review ─► regenerate weak shots ─► deliver
                                            │
                                     save cast + sets back to the library for next time
```

Rules that fall out of the research, and are enforced by the skill:

1. One shot per prompt. One subject per ingredient image. At most three ingredients.
2. A character's description is copied **verbatim** into every shot they appear in — never paraphrased.
3. 8 seconds is a hard ceiling per generation; plan in slabs. Timestamp prompting only *inside* one 8-second beat.
4. Dialogue, SFX and ambience are written into the Veo prompt, not added later, so lip sync is in-clip.
5. Extend only for continuous action; save-frame → start-frame for a new beat with the same character.
6. Vertical is native at 9:16 — never crop a 16:9 clip for a reel.
7. Regeneration is expected. Budget roughly one retry for every four shots.

## Sources

- [Ultimate prompting guide for Veo 3.1 — Google Cloud](https://cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-veo-3-1)
- [Edit videos & build scenes in Google Flow — Google Labs Help](https://support.google.com/labs/answer/16935718?hl=en&co=GENIE.Platform%3DDesktop)
- [Bringing new Veo 3.1 updates into Flow — Google blog](https://blog.google/innovation-and-ai/products/veo-updates-flow/)
- [Best practices for Veo on Vertex AI](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/best-practice)
- [Veo 3.1 Ingredients to Video update — CineD](https://www.cined.com/google-veo-3-1-ingredients-to-video-update-adds-native-vertical-format-4k-upscaling-and-enhanced-character-consistency/)
- [The complete guide to Veo 3 character consistency — BetterLink](https://eastondev.com/blog/en/posts/ai/20251207-veo3-character-consistency-guide/)
- [How to extend Veo 3 videos beyond 8 seconds — veo3ai.io](https://www.veo3ai.io/blog/veo-3-extend-video-beyond-8-seconds-2026)
- [Nano Banana Pro guide: character sheets, edits, 4K — Flick](https://flick.art/blog/nano-banana-pro-guide)
- [Creating a character reference sheet for AI videos — pIXELsHAM](https://www.pixelsham.com/2026/04/18/creating-a-character-sheet-for-ai-videos-using-nano-banana/)
- [Google Vids complete guide (Veo 3.1 + avatars)](https://pasqualepillitteri.it/en/news/652/google-vids-complete-guide-free-ai-video-creator-veo-avatars)
- [Google Vids — Wikipedia](https://en.wikipedia.org/wiki/Google_Vids)
