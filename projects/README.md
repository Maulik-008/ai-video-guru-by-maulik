# projects

One folder per video: `projects/<slug>/`.

| File | Committed | What it is |
|---|---|---|
| `plan.json` | yes | beats, shots, ingredients and the full Veo prompt for each shot — the reproducible record of the video |
| `manifest.json` | yes | run state: what generated, how many attempts, credits spent, problems |
| clips, stills, the finished video | no | they live in your output folder, not in git |

The format of both files is in [`.claude/skills/video-guru/references/shotplan.md`](../.claude/skills/video-guru/references/shotplan.md).

A plan is worth keeping: months later it regenerates the same video, because every description in it is verbatim and every ingredient points into `cast/` and `sets/`.
