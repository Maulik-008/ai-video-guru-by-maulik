# cast

Your characters. This folder is the most valuable thing in the repo — it is what makes video #2 look like video #1.

```
cast/<character-id>/
  character.json    frozen description + voice. Copied VERBATIM into every prompt.
  portrait.png      the locked identity anchor
  sheet.png         6-panel turnaround, generated from the portrait
  ing-face.png      tight single-subject crops, used as Flow ingredients
  ing-full.png
  prompts.md        exactly what made each image, and when
```

`<character-id>` is lowercase kebab-case and **permanent** — it appears in prompts, filenames and plans, so renaming it orphans every earlier video.

Images here are committed: they are small, and they are the library. The contract, the creation steps and the reuse workflow: [`.claude/skills/video-guru/references/consistency.md`](../.claude/skills/video-guru/references/consistency.md).

To reuse someone, just say so — "same chai uncle" — and the skill reads this folder instead of inventing a new face.
