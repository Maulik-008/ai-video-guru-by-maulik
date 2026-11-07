# sharma-aunty: exact prompts (draft, nothing generated yet)

Series: Gadbad Grah. Style: Pixar-style 3D.

## Anchor image (Gemini, Nano Banana)

```
Generate exactly ONE image only, no storyboard, no extra images. Pixar-style 3D character render, full body, standing, centred, plain neutral grey background, soft even studio lighting. Subject: a sturdy 50-year-old Indian housing-society secretary, Pixar-style 3D, a sharp black bob with one grey streak, rectangular glasses on a beaded chain, a bold magenta block-print cotton kurta, dark red lipstick, one permanently raised eyebrow. No text, no labels, no watermarks.
```

## After the anchor is accepted
1. Save it as `portrait.png` in this folder.
2. Generate the 6-panel sheet from it (prompt in `.claude/skills/video-guru/references/prompting.md`).
3. Crop tight single-subject ingredients (`ing-face.png`, `ing-full.png`).
4. Set `"frozen": true` in `character.json`. From then on the description is copied word for word and never edited.
