# bhondu: exact prompts (draft, nothing generated yet)

Series: Gadbad Grah. Style: Pixar-style 3D.

## Anchor image (Gemini, Nano Banana)

```
Generate exactly ONE image only, no storyboard, no extra images. Pixar-style 3D character render, full body, standing, centred, plain neutral grey background, soft even studio lighting. Subject: a very tall skinny Pixar-style 3D alien, soft sky-blue skin, a long noodle neck, a small round head with huge gentle glossy brown eyes, one droopy antenna with a soft yellow tip, a loose grey uniform that is too short at the wrists and ankles, a shy permanent smile. No text, no labels, no watermarks.
```

## After the anchor is accepted
1. Save it as `portrait.png` in this folder.
2. Generate the 6-panel sheet from it (prompt in `.claude/skills/video-guru/references/prompting.md`).
3. Crop tight single-subject ingredients (`ing-face.png`, `ing-full.png`).
4. Set `"frozen": true` in `character.json`. From then on the description is copied word for word and never edited.

## Result (2026-11-07)
Generated first try in a fresh Gemini chat with the prompt above plus 'no letters'. Saved as `portrait.png` (full size) and `ing-full.png` (1280 px). Not frozen until the user approves.
