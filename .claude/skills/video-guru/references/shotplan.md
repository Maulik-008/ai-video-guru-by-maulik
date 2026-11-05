# The shot plan: slabs of 8 seconds

Veo generates **4, 6 or 8 seconds at a time**. Everything longer is a stack of shots — "slabs" — joined deliberately. This file is how the stack is planned before a single credit is spent.

## Lengths that work

| Deliverable | Total | Shots | Typical mix |
|---|---|---|---|
| Hook reel | 15–20 s | 3 | 6 + 6 + 8 |
| Standard reel / short | 30 s | 4–5 | 8 + 8 + 6 + 8 |
| Story short | 45 s | 6–7 | mostly 8, one 4 for a beat |
| Long short | 60 s | 8–9 | mostly 8 |

More shots is not better. Each one is a chance for the face to drift and a credit spent. Three strong shots beat six weak ones.

## Beat sheet first (no prompts yet)

Write the story as beats, then map beats to shots:

1. **Hook (0–2 s).** A question, a promise or something wrong. No logo, no throat-clearing, no slow establishing drift.
2. **Setup.** Who, where — one shot, usually the only wide one.
3. **Turn.** The thing that changes. This is the shot to spend the extra credits on.
4. **Pay-off.** The answer, the punchline, the consequence. It must land on a beat, not fade out.

Show the user the beat sheet and the **dialogue**, not the prompts. Lines are what they care about and what they will want to change.

## Dialogue fits the slab, not the other way round

Speech runs about **2.2–2.8 words per second**.

| Shot | Words that fit |
|---|---|
| 4 s | up to 9 |
| 6 s | up to 14 |
| 8 s | up to 18 |

Leave room: a shot that is all talking from frame one feels rushed. Aim for 70% of the ceiling and let the shot breathe at each end. One speaker per shot — two people talking inside 8 seconds rarely survives.

## How shots join

| Join | When | How |
|---|---|---|
| `cut` | New angle, new beat, same world | Nothing special — same ingredients, same style line, different cinematography. The default. |
| `handoff` | The motion must continue across the join | In Flow, pause on the last good frame of shot N → **Save frame** → use it as the **start frame** of shot N+1. |
| `extend` | One unbroken action that cannot cut at 8 s | Flow's **Extend** on that clip. Only Veo-generated clips can be extended, and each extension is generated from the final second of the previous one, so drift compounds. Use once, twice at most, never as the backbone. |
| `frames` | A specific transition between two known images | First-and-last-frame: supply both stills and describe the move between them. |

Default to `cut`. Reach for `handoff` when a hand, a vehicle or a walk crosses the join. `extend` is a last resort.

## plan.json

```json
{
  "slug": "chai-stall-dawn",
  "title": "The first cup",
  "language": "hi-IN",
  "aspect": "9:16",
  "model": "veo-3.1-fast",
  "styleLine": "Shot on 35mm, warm highlights against cool shadows, shallow depth of field, fine grain, no text, no captions, no subtitles, no watermarks.",
  "cast": ["chai-uncle", "riya"],
  "sets": ["stall-dawn"],
  "beats": ["hook: tea poured in the dark", "setup: who he is", "turn: she asks why he never sleeps", "payoff: the answer"],
  "shots": [
    {
      "id": "s01",
      "seconds": 8,
      "beat": "hook",
      "set": "stall-dawn",
      "ingredients": ["cast/chai-uncle/ing-full.png", "sets/stall-dawn/plate.png"],
      "camera": "medium shot, slow push-in",
      "speaker": "chai-uncle",
      "line": "Pehli chai hamesha sabse acchi hoti hai.",
      "sfx": "the hiss of boiling milk, a steel tumbler set down",
      "ambient": "distant traffic, a crow, low morning street",
      "joinToNext": "cut",
      "prompt": "<the full Veo prompt, descriptions pasted verbatim>"
    }
  ],
  "assembly": { "with": "vids", "captions": true, "music": "soft tabla under dialogue", "endCard": "@handle" },
  "estimate": { "clips": 5, "creditsPerClip": 20, "retryAllowance": 1, "creditsTotal": 120 }
}
```

`prompt` is written out in full for every shot, with every character description pasted **verbatim** and the one `styleLine` appended. The plan is the thing that gets reviewed and the thing that gets replayed — a shot must be reproducible from it alone, months later.

## manifest.json (written while generating, next to the plan)

```json
{
  "slug": "chai-stall-dawn",
  "runStart": "2026-11-05T09:12:00+05:30",
  "outDir": "C:\\Users\\me\\Videos\\VideoGuru\\chai-stall-dawn",
  "ingredients": { "chai-uncle": "done", "stall-dawn": "done" },
  "shots": { "s01": { "state": "done", "file": "s01.mp4", "attempts": 1 }, "s02": { "state": "pending" } },
  "creditsSpent": 40,
  "notes": ["s01: regenerated once, extra hand in first take"]
}
```

Update it after **every** completed step. If a run is interrupted — a sign-in, a quota, a closed laptop — the next run skips everything marked `done`.

## Budgeting credits

`clips × credits-per-clip × 1.25` for retries. Quote that number in step 4, not the optimistic one, and stop when it is reached rather than spending into a second video's worth of credits.

Cheaper plans, in order of what to try when the balance is short:

1. Fewer, longer shots (five 8-second shots beat eight 5-second ones).
2. Timestamp prompting — several beats inside one 8-second generation, when they share a location and ingredients.
3. 4-second shots for reaction beats with no dialogue.
4. A shorter video. Twenty good seconds beat sixty thin ones.
