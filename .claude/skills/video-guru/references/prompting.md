# Prompting: Gemini and Veo 3.1

Formulas and syntax are from Google's own Veo 3.1 prompting guide; see [docs/RESEARCH.md](../../../../docs/RESEARCH.md) for sources.

## Gemini

### The rule that is never optional

Every image prompt starts with:

> Generate exactly ONE image only, no storyboard, no extra images.

Without it Gemini returns a contact sheet of ten variants and the run loses its anchor.

### Portrait (the identity anchor)

```
Generate exactly ONE image only, no storyboard, no extra images.
Photographic head-and-shoulders portrait, neutral expression, looking straight at
camera, plain light grey background, soft even lighting, sharp focus, 9:16.
Subject: <verbatim description>
```

### Character sheet (always generated FROM the portrait, with it attached)

```
Using the attached image as exactly the same person, generate exactly ONE image:
a 6-panel character reference sheet on a clean neutral grey background —
front full body, 3/4 full body, side profile, back view, face close-up, mid-shot.
Identical face, hair, wardrobe and proportions in every panel.
Even lighting, no text, no labels, no watermarks.
```

### Ingredient crop

```
Using the attached image as exactly the same person, generate exactly ONE image:
<full body | face>, plain neutral background, nothing else in frame, even lighting.
Subject: <verbatim description>
```

### Set plate

```
Generate exactly ONE image only, no storyboard, no extra images.
Establishing <wide|medium> shot, no people in frame, <aspect>.
Place: <verbatim set description>. Lighting: <time of day, quality of light>.
Style: <style line, identical across the whole video>
```

### Gemini hygiene

- One chat per character; one chat for all sets of a video (so the style holds).
- To continue in the same look: "same character exactly as in the previous image".
- Download from the image viewer's **full-size** button; the hover button does nothing while a reply is still streaming.
- Do not click the prompt box while the cursor is over an image — it opens the viewer and your typing goes nowhere.

## Veo 3.1 (in Flow)

### Prompt formula

```
[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance]
```

### Shot template used by the plan

```
Using the provided images for <Name>, <Name>, and <set>, create a
<shot size> <camera move>.
<Name>, <VERBATIM description>, <action>.
<context: where, when, what else is happening>.
<Name> says in a <voice spec>, "<line>"
SFX: <one or two effects>
Ambient noise: <the bed of the place>
<style line: film stock, grade, grain, lens — identical in every shot of the video>
```

Worked example:

```
Using the provided images for Chai Uncle and the stall at dawn, create a medium
shot, slow push-in.
Chai Uncle, a 58-year-old Indian tea seller, stocky build, deep smile lines,
salt-and-pepper moustache, thick black-framed glasses, wearing a faded blue kurta
with rolled sleeves and a grey shawl over one shoulder, pours tea from a height
into a steel tumbler without looking down.
A roadside stall before sunrise, steam in cold blue air, one bare bulb overhead.
Chai Uncle says in a warm gravelly unhurried voice, "Pehli chai hamesha sabse
acchi hoti hai."
SFX: the hiss of boiling milk, a steel tumbler set down
Ambient noise: distant traffic, a crow, low morning street
Shot on 35mm, warm highlights against cool shadows, shallow depth of field,
fine grain.
```

### Audio syntax (exactly these forms)

| Want | Write |
|---|---|
| Dialogue | `<Name> says, "<line>"` or `… says in a <voice spec>, "<line>"` |
| Effect | `SFX: thunder cracks in the distance` |
| Room tone | `Ambient noise: the quiet hum of a starship bridge` |

Dialogue goes **in the prompt**, so the lip sync is generated with the picture. Never plan to add the voice afterwards.

### Several beats inside one 8-second clip

```
[00:00-00:02] <shot>. <action>. SFX: …
[00:02-00:04] <reverse shot>. <action>.
[00:04-00:06] <tracking shot>. <action>.
[00:06-00:08] <wide reveal>.
```

Cheaper than four clips when the beats are tight and share one location. Not for beats that need different ingredients.

### Camera and style vocabulary

- **Movement:** dolly, tracking, crane, aerial, slow pan, POV, push-in, pull-out, orbit
- **Composition:** wide, medium, close-up, extreme close-up, low angle, high angle, two-shot, over-the-shoulder
- **Lens and focus:** shallow depth of field, wide-angle, soft focus, macro, deep focus
- **Mood:** "melancholic mood with cool blue tones", "harsh fluorescent overheads", "a single dramatic spotlight", "shot as if on 1980s colour film, slightly grainy"

Keep one **style line** for the whole video and paste it into every shot, the same way the character description is pasted.

### What does not work

- **Negations.** "No buildings" puts buildings in. Write what should be there: "a desolate landscape with no buildings or roads" is phrased as the presence of desolation.
- **Text on screen.** Veo spells badly. Titles, captions and end cards are added in Vids, never asked for in the prompt. Add "no text, no captions, no subtitles, no watermarks" to the style line.
- **More than ~18 words of dialogue in 8 seconds.** Speech runs about 2.2–2.8 words per second. Count before generating.
- **Add/remove object** — that runs on Veo 2 and returns a clip with **no audio**. Never use it on a dialogue shot.

### Settings before the first generation

Aspect from the plan (9:16 is native — never crop a 16:9 clip for a reel), outputs ×1, model **Veo 3.1 Fast** by default. Lite is visibly worse; Quality costs several times more and is worth it only for a hero shot the user asked to upgrade.
