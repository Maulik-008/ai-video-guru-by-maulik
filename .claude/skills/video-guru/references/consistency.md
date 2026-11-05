# Consistency: the cast library

The one thing that separates a good AI video from a cheap one is that the same character looks like the same person in shot 5 as in shot 1 — and in next month's video too. That does not happen by prompting carefully. It happens because the character is a **saved artefact**.

## The three mechanisms (all three, always)

1. **A locked identity anchor.** One portrait, chosen and frozen. Everything else is generated *from that image*, never from the text again.
2. **Tight, single-subject ingredient crops.** One subject per image, plain background, no second person, no busy scene. A crowded reference makes the model guess which part you meant.
3. **Verbatim description.** The same words, in the same order, in every prompt the character appears in. Paraphrasing changes the face.

## Folder contract

```
cast/<character-id>/
  character.json     canonical record — the source of truth
  portrait.png       the locked anchor: head and shoulders, neutral expression, plain background
  sheet.png          6-panel turnaround generated FROM portrait.png
  ing-face.png       tight crop: face only
  ing-full.png       tight crop: full body, plain background
  ing-<variant>.png  optional: a wardrobe or age variant, same face
  prompts.md         the exact prompt that made each file, and the date

sets/<set-id>/
  plate.png          the establishing image of the place
  set.json           id, description (verbatim block), lighting, time of day
  prompts.md
```

`<character-id>` is lowercase kebab-case and permanent: `chai-uncle`, `riya`, `bolt-the-robot`. It appears in prompts, filenames and plans, so renaming it later breaks the link between old videos and new ones. Choose it once, with the user.

## character.json

```json
{
  "id": "chai-uncle",
  "name": "Chai Uncle",
  "created": "2026-11-05",
  "description": "a 58-year-old Indian tea seller, stocky build, deep smile lines, salt-and-pepper moustache, thick black-framed glasses, wearing a faded blue kurta with rolled sleeves and a grey shawl over one shoulder",
  "voice": "warm gravelly male voice, unhurried, Hindi with a Delhi accent, speaks as if he has told this story a hundred times",
  "signature": "always holds a steel kettle in his right hand",
  "doNot": ["no apron", "never clean-shaven", "no English dialogue"],
  "images": {
    "portrait": "portrait.png",
    "sheet": "sheet.png",
    "ingredients": ["ing-face.png", "ing-full.png"]
  },
  "appearsIn": ["chai-stall-dawn"]
}
```

**`description` is the frozen block.** It is pasted into every shot prompt, word for word, after the shot's cinematography. It must be one clause-chain, no line breaks, no stage directions — only what the character *looks like*. Mood, action and camera belong to the shot, never here.

**`voice`** is pasted into any shot where the character speaks, so the delivery matches across shots.

**`doNot`** is written as positives in prompts ("wearing a faded blue kurta", not "no apron") because negations do not work — it is kept here so the director can check the result rather than feed it to the model.

## Making a character (step 5 of the skill)

In **one Gemini chat per character**:

1. **Agree the words first** with the user. Read the `description` back to them and get a yes. After this it is frozen.
2. **Portrait.** "Generate exactly ONE image only, no storyboard, no extra images. Photographic head-and-shoulders portrait, neutral expression, looking at camera, plain light grey background, soft even lighting, 9:16: `<description>`."
   Regenerate until the user says *that is the character*. This is the only subjective step — everything after it is mechanical.
3. **Sheet, from the portrait.** With the portrait attached: "Using the attached image as the exact same person, generate exactly ONE image: a 6-panel character reference sheet on a clean neutral grey background — front full body, 3/4 full body, side profile, back, face close-up, mid-shot. Identical face, hair, wardrobe and proportions in every panel. No text, no labels."
4. **Ingredient crops.** From the sheet or the portrait, one tight crop per file. If Gemini will not crop reliably, ask for each one as its own single image with the portrait attached and "exactly the same person".
5. **Check before saving.** Compare each image against the written description, line by line: age, build, hair, glasses, wardrobe, the signature prop. One regeneration is normal. Two failures means the description is fighting itself — fix the words with the user, then start again from the portrait.
6. **Write `character.json` and `prompts.md` immediately**, before any video is generated.

## Reusing a character

When the user says "same uncle as last time":

1. Read `cast/<id>/character.json`. Show them the portrait and the description.
2. Use `description` **verbatim**, unchanged, even if a better phrasing suggests itself.
3. Use the saved ingredient crops as Flow ingredients — do not regenerate them. Regenerating the anchor is what makes a returning character look slightly wrong.
4. Append the new project to `appearsIn`.

## Evolving a character (new wardrobe, older, different mood)

Keep the same `id` and the same **face** clauses; change only the wardrobe clause. Save the new look as `ing-<variant>.png` and add a `variants` entry to `character.json`, with its own verbatim block. Never fork a second character id for a costume change — that is how a cast library rots.

## Multi-character shots

- At most **three ingredients per shot**, character first, most important first. Two characters plus a set is the practical maximum.
- Name each ingredient by role in the prompt: "Using the provided images for Chai Uncle, Riya, and the stall at dawn, …".
- More than two speaking characters in one 8-second shot is a losing fight: split it into two shots, one per speaker, and cut between them.

## When consistency fails anyway

It will, sometimes — a reference is a steer, not a guarantee. In order of what to try:

1. Regenerate the shot unchanged (different seed, same inputs).
2. Tighten the ingredient crop — remove background, remove the second person.
3. Put the character earlier in the ingredient order, and earlier in the prompt.
4. Shorten the shot: a 4-second shot drifts less than an 8-second one.
5. Change the shot so the face is less exposed — over-the-shoulder, side-on, a hands insert.
6. Record it as a degradation and tell the user. Do not quietly ship a different face.
