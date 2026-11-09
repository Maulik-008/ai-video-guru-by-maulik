# bade-chacha: exact prompts (draft, nothing generated yet)

Series: Gadbad Grah. Style: Pixar-style 3D.

## Anchor image (Gemini, Nano Banana)

```
Generate exactly ONE image only, no storyboard, no extra images. Pixar-style 3D character render, full body, standing, centred, plain neutral grey background, soft even studio lighting. Subject: an elderly Pixar-style 3D alien emperor with a very large wrinkled head and a small frail body, deep wrinkles, a drooping white handlebar moustache of glowing feelers, tiny round spectacles, a ruby-red gem on his wrinkled forehead, a permanently disappointed frown, a heavy maroon robe with gold trim. No text, no labels, no watermarks.
```

## Earth hologram version (do after the anchor is accepted)
Do not edit the description. In Earth shots add: "shown as a flickering green hologram, head and shoulders only".

## After the anchor is accepted
1. Save it as `portrait.png` in this folder.
2. Generate the 6-panel sheet from it, then tight ingredient crops (`ing-face.png`, `ing-full.png`).
3. Set `"frozen": true` in `character.json`.

## Result (2026-11-07)
Generated first try in a fresh Gemini chat with the prompt above plus 'no letters'. Saved as `portrait.png` (full size) and `ing-full.png` (1280 px). Not frozen until the user approves.
