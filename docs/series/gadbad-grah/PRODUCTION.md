# Gadbad Grah: Production plan

Written 2026-11-07. Read [BIBLE.md](BIBLE.md) first for the story and [SCRIPTS.md](SCRIPTS.md) for every line.
Nothing has been generated, downloaded or spent. This file is the plan for doing it.

---

## 1. Read this first: the tools changed under the repo

Google's Flow help pages (read directly on 2026-11-07) say:

- **5 December 2026: Veo 3.1 Fast, Veo 3.1 Quality and Omni Flash 1.1 are retired.** The models left are **Omni Flash 1.2** and **Veo 3.1 Lite**.
- **5 November 2026: Veo Extend was retired.** Extending a video now needs a Google AI Plus, Pro or Ultra plan and Omni Flash 1.2.
- **Veo 3.1 Lite** (720p): 4, 6 or 8 s clips, but **Ingredients-to-Video works at 8 s only**. No extend, no video-to-video.
- **Omni Flash 1.2:** described by Google as "higher visual quality and consistency, longer video lengths, duration-based pricing", with custom voices, 360p at one third the cost, and clips up to 10 s (up to 15 s on a paid plan).

**What this means for the repo.** [CLAUDE.md](../../../CLAUDE.md), [RESEARCH.md](../../RESEARCH.md) and [prompting.md](../../../.claude/skills/video-guru/references/prompting.md) still say "Veo 3.1 Fast by default", "Lite is visibly worse" and describe Extend. After 5 December the default model will not exist. I have **not** edited those files, because they define your pipeline and the change is your call. Tell me and I will update them with the evidence.

**What this means for the series.** Plan Wave 1 on the models that will still exist: **Veo 3.1 Lite** (cheap, 8 s ingredients) and **Omni Flash 1.2** (quality, longer shots, custom voice). Phase 0 below decides which one to use.

---

## 2. What the research found

I read two trend articles and two Google help pages in the browser, and ran about a dozen searches. Only primary pages are called "confirmed". Everything else is vendor or blog material, marked as such.

### Confirmed (Google's own pages)
- Credit costs and model limits above ([models page](https://support.google.com/flow/answer/16352836?hl=en), [credits page](https://support.google.com/flow/answer/16526234?hl=en)).
- Every account gets **50 Flow credits a day** (no rollover); Pro adds 1,000 a month, Ultra $100 adds 10,000, Ultra $200 adds 25,000.
- **Non-subscribers may be blocked from video generation during peak hours, roughly 2 PM to 5 PM UTC.** That is **7:30 to 10:30 PM India time**, your prime working hours. A paid plan removes this.

### Reasonably consistent across sources (not independently measured)
- **Series beat one-offs.** Recurring characters across numbered episodes are outperforming single viral posts ([Anijam](https://www.anijam.ai/blog/instagram-reels-trends/)). The Indian fruit-drama pages plan 20 to 30 part series ([BuzzInContent](https://www.buzzincontent.com/insight/how-low-effort-ai-fruit-drama-reels-are-hijacking-millions-of-indian-screens-11756545)).
- **Length: 45 to 60 seconds** had the highest median views and engagement in one 2026 analysis cited by secondary sources; others say completion rate peaks under 15 s. Sources disagree, and one says Reels over 60 s lose 20 to 50% completion unless tightly structured. **Decision (v2): every reel is about 62 s (seven 8 s shots plus a 6 s closing question), trailer 26 s, finale 76 s. Nothing goes over 90 s** (see the Instagram 90-second statement below). The first five posts are the test: if completion drops sharply at 62 s, we cut back to 6 shots.
- **Completion rate is the metric that matters** for Reels ranking. Instagram now reports a **3-second skip rate**, so the first two seconds decide everything. Spoken lines in the first 3 seconds are reported to beat background music (one unverified source). **Decision: every reel opens on a spoken line or a visual shock.**
- **Cadence:** vendors say 3 to 5 Reels a week; one series guide says to ship **4 episodes in 14 days, then check retention before planning more**, and that many creators quit at episodes 5 to 7 when numbers are still flat. **Decision: Wave 1 = the first five posts (trailer, E01, E02, P1, E03), then a data gate.**
- **What Instagram ranks on.** Social Media Today quotes Adam Mosseri (January 2025) naming **watch time, likes and sends** as the top signals; the secondary blogs say sends matter most for reaching non-followers ([Social Media Today](https://www.socialmediatoday.com/news/instagram-shares-algorithm-insights-2025/738034/), seen in a search result, not opened). **Decision: write lines people want to send to the person they remind them of (mom guilt, Aunty's rules, the family group, "Sharma-ji ka beta"), and keep the story watchable to the end.** I did not add any request to share.
- **Engagement bait is a real risk.** Instagram said in June 2024 that if it believes content "explicitly asks for engagement through shares, comments, tags, or other actions," it will not recommend it, with "comment a specific word, number, or emoji" as the example, and that **open-ended questions and calls to action are fine**; it later clarified that earnestly engaging with your audience is not bait ([article 1](https://www.socialmediatoday.com/news/instagram-certain-ctas-impact-post-reach/717732/), [article 2](https://www.socialmediatoday.com/news/instagram-clarifies-advice-single-word-ctas-longer-reels/718151/), both read in full). **Decision: Bhondu only asks open questions ("kya hai? aur kyun?"); a script check flags any "comment", "tag", "share", "like" in a spoken line.** These articles are from 2024, so recheck Instagram's current guidance before launch.
- **Reels over 90 seconds are not recommended** to non-followers (same June 2024 statement). **Decision: no reel passes 90 s.**
- **Alien fish-out-of-water:** the premise runs dry if the alien masters Earth too fast (the ALF critique), and works best with a through-line mystery (Resident Alien) and an ensemble that is not passive. **Decision: Dhamaka never masters Earth; Mausi's secret is the through-line; Aunty, Chintu and Bhondu all act.**
- **Desi comedy:** exaggeration, delivery and situational character comedy work; critics say Bollywood comedy declined through humiliation and stereotypes; a stand-up study lists "lazy maid" and "crass autowala" as worn-out tropes ([IAFOR](https://iafor.org/archives/journals/iafor-journal-of-media-communication-and-film/10.22492.ijmcf.7.1.02.pdf), [Milestone101](https://www.milestone101.com/lifestyle/The_Last_Laugh__Tracing_Hindi_Cinema_s_Fading_Funny_Bone)). **Decision: no group stereotypes; Aunty wins by rules, not by humiliating anyone.**

### Not found, so treat as unverified
- **Hindi lip-sync quality** in Veo 3.1 or Omni Flash 1.2. Every guide I found is English-first. One says non-English can show "minor sync drift on fast speech"; one anecdotal test says single-character lip sync worked about 80% of the time vs about 40% with multiple characters. **This is why Phase 0 exists.**
- **Instagram and profanity.** No official page I found names "ullu ke pathe" or "harami". Instagram's [Recommendations Guidelines](https://help.instagram.com/313829416281232) say recommended content is held to a higher standard than the Community Guidelines, and their examples are hate speech and graphic violence, not mild insults; the page I found is older. **Decision: keep insults mild, ration level 2, bleep anything stronger, and check the current Recommendation Guidelines yourself.** Blogs about "shadowbans" were low quality and ignored.
- **AI labelling.** Instagram has an "AI info" label (applied manually or detected automatically, with imperfect detection) and in May 2026 began testing an optional profile-level **"AI Creator" label**; reporting says Meta states it does not change distribution ([Engadget](https://engadget.com/2162426/instagram-is-testing-optional-ai-creator-labels), [MediaPost](https://www.mediapost.com/publications/article/414862/instagram-unveils-new-ai-creator-account-label.html)). I'd turn the label on: the characters are obviously animated and honesty costs nothing here. Your call.
- Specific reach claims ("tens of millions", "340% more reach") come from blogs and one agency interview. They show the format works, not how much.

---

## 3. Budget (Google's published credit costs)

Season 1 (v2 scripts) has **18 reels, 142 shots and about 1,094 seconds**. Retries are normal, so every number includes the repo's `× 1.25` allowance.

| Option | How it is charged | Wave 1 (36 shots, 274 s) | Wave 2 (48 shots, 372 s) | Wave 3 (58 shots, 448 s) | Full season (142 shots, 1,094 s) |
|---|---|---|---|---|---|
| **Veo 3.1 Lite** | 10 credits per clip (5 on Ultra). Ingredients mode is 8 s only, so every shot is generated at 8 s and trimmed in Vids. | about **450** | about **600** | about **725** | about **1,775** (890 on Ultra) |
| **Omni Flash 1.2 at 720p** | 3 credits per second | about **1,030** | about **1,395** | about **1,680** | about **4,100** |
| **Omni Flash 1.2 at 360p** (drafts) | 1 credit per second | about **340** | about **465** | about **560** | about **1,370** |

How far that goes:
- **Free:** 50 a day, no rollover, about 1,500 a month if used daily. Peak-hour video block applies.
- **Pro:** 1,000 extra a month. The full season on Lite fits in about a month on Pro plus free credits.
- **Ultra $100:** 10,000 a month. Covers the season on any option.

The v2 rewrite is about 15% more footage than the first draft (142 shots instead of 123): one extra beat per reel plus Bhondu's closing question. If credits are short, cut the closing question from the reels where it is least needed (it is also in the pinned comment) or drop to 6 shots per reel.

Cheapest sensible path: **write and lock every line at 360p or Lite, then regenerate only the shots you keep in the final model.** Do not assume a 360p take looks like the 720p take; the model regenerates.

Mausi's scenes (no face) and 4 to 6 s reaction shots are the cheapest to protect. Timestamp prompting can hold two beats in one 8 s clip when they share a set and ingredients.

---

## 4. Phase 0: test before committing (about 150 credits, 2 days of free credits)

The whole plan rests on four things nobody has verified for Hindi. Run these before generating anything for real.

| # | Test | Pass means |
|---|---|---|
| 1 | **Hindi lip sync:** one 8 s shot of Dhamaka saying the E01 s01 line, on Lite and on Omni Flash 1.2 (360p) | Mouth matches, no clipped first or last word |
| 2 | **Line length:** a 13-word line (E02 s03) in 8 s | The whole line fits. Hindi syllables run longer than English, so trim lines that clip |
| 3 | **Voice repeat:** the same voice spec in two clips; try Omni's custom voice | Same voice in both. If not, use Omni's preset voice per character |
| 4 | **Ingredients:** does Omni Flash 1.2 accept ingredients? The Lite page says yes (8 s). The Omni feature list was collapsed on the page I read | Two characters, one set, faces match the anchors |

If Hindi lip sync fails on both, stop and tell me: the fallback is a different format (silent visual gags with captions), which would be a different plan.

---

## 5. Build order

### Step A: lock the cast and the sets (all free, in Gemini)
Draft folders already exist in `cast/` and `sets/`. For each one:
1. Generate the anchor from its `prompts.md` and accept one (images are free; iterate here, not in Flow).
2. Build the 6-panel sheet, then the tight ingredient crops.
3. Set `"frozen": true`.

**Dhamaka needs three gem variants** as separate portraits (red, pink, blue-white). The gem is the plot, and the face stays the same across them. Order of importance for Wave 1: Dhamaka, Aunty, Bhondu, **Bade Chacha** (he narrates P1), the ship plate, the **council hall plate**, Mausi, Chintu, Tej. Bade Chacha needs two looks: solid on his throne (Gadbad), and the green hologram version for Earth.

### Step B: Wave 1 (posts 1 to 5: trailer, E01, E02, P1, E03)
Per reel, run the video-guru skill with the episode from [episodes.json](episodes.json). The dialogue, camera, set and sound for every shot are already written; the skill adds the verbatim character descriptions, the style line and the one confirmation. Then in Vids: title card ("Hamle mein N din baaki"), captions, music, export.

### Step C: the data gate (after E03 is 3 to 4 days old)
Also watch whether **P1 (the history reel) holds viewers as well as the Earth reels**. If it drops sharply, shorten P2 and P3 or cut one.
Check **per episode**: 3-second skip rate, view-through rate, shares, and whether viewers of E02 or E03 go back to E01. Rough vendor benchmarks for 30 to 60 s reels: above about 40% view-through. If early drop-off is high, fix the **first spoken line**, not the trend.

### Step D: Waves 2 and 3
Wave 2 (posts 6 to 11: P2, E04, P3, E05, E06, E07) and Wave 3 (posts 12 to 18: E08 to E14) follow the gate. The scripts can be rewritten after Wave 1 if a gag or voice does not land.

### Posting rhythm
- Release order: trailer, E01, E02, **P1**, E03, **P2**, E04, **P3**, E05, then E06 to E14 (the full list with shot counts is at the top of [SCRIPTS.md](SCRIPTS.md)). The first five posts take about 10 days at 3 a week. Do not publish the whole season at once; the countdown format works only if each number appears on its own day.
- Keep captions to one line and put the episode number in it. I found no reliable data on hashtags or best posting times, so measure both in your own Insights instead of following a rule.
- I have not published anything and will not: files stay on your disk, as the repo requires.

---

## 6. Risks and what I did about them

| Risk | Handling |
|---|---|
| **Models retire 5 Dec** | Plan on Lite and Omni 1.2; Phase 0 decides. Repo docs need an update (offered above) |
| **Hindi lip sync unproven** | Phase 0 first; short lines (about 70% of the slab); medium close-ups; one speaker per shot |
| **Voice changes between clips** | Same voice spec word for word in every prompt; test Omni custom voices |
| **Gem colour drift** | Three Dhamaka anchors; state the gem colour in every prompt; never rely on it being inferred |
| **Ship looks different each shot** | It is part of the `society-parking` and `ship-bridge` set plates. Describe the same three-legged dented pressure cooker every time |
| **Veo cannot spell** | Zero on-screen text in prompts; titles and captions only in Vids |
| **Extra faces and crowds** | Two characters at most, no crowds, no fast vehicles; traffic is sound. The Gadbad council is **heard, never seen**: off-screen shouting while the camera stays on one or two characters |
| **Closing questions flagged as engagement bait** | Open-ended questions only, never a request for a word, tag or share; the build script flags those words; recheck Instagram's current wording |
| **62 s is too long for completion** | Wave 1 is the test; a joke every shot; cut to 6 shots if the drop-off is sharp |
| **History reels feel slow** | P1 is a deadpan documentary with a joke every shot; flashbacks are placed after the Earth hooks (Option B); the data gate checks P1 retention |
| **Profanity and recommendation reach** | Mild insults, level 2 rationed, BEEP for the rest, no group-targeted abuse. Verify current guidelines |
| **Copying other people's work** | All lines are original. No film dialogue, no copyrighted songs, no real people or brands. "Sharma-ji ka beta" is a common idiom. Check handle and name availability before launch; I did not search trademarks |
| **Repeating the Zog series** | New world, new cast. Commander Zog and Kamla Dadi are untouched and could cameo in Season 2 if you want |

---

## 7. Sources

**Read in full (in the browser):**
- [Learn about Google Flow models & supported features](https://support.google.com/flow/answer/16352836?hl=en)
- [Manage your Google Flow credits](https://support.google.com/flow/answer/16526234?hl=en)
- [Instagram Reels Trends 2026, Anijam](https://www.anijam.ai/blog/instagram-reels-trends/) (a vendor blog)
- [How AI fruit drama reels are hijacking Indian screens, BuzzInContent](https://www.buzzincontent.com/insight/how-low-effort-ai-fruit-drama-reels-are-hijacking-millions-of-indian-screens-11756545)

**Seen only as search results (not opened):**
- Series strategy: [CreatorFlow](https://creatorflow.so/blog/instagram-content-series-strategy/); Meta's episodic Series test: [Gulf News](https://gulfnews.com/technology/media/instagram-and-facebook-reels-may-soon-work-like-tv-episodes-1.500561278)
- Length and retention: [SocialBu](https://socialbu.com/blog/instagram-reels-length), [OpusClip](https://www.opus.pro/blog/ideal-instagram-reels-length), [MoonB](https://www.moonb.io/blog/instagram-reel-length)
- Hooks: [OpusClip hook formulas](https://www.opus.pro/blog/instagram-reels-hook-formulas), [Pulse](https://www.pulse.bot/digital-marketing/news/human-speech-and-presence-help-drive-reels-engagement-26291baf-0b96-441f-aefa-8af987fa02e8)
- Veo dialogue: [Veo 3.1 dialogue + SFX](https://www.veo3gen.app/blog/veo-31-dialogue-sfx-prompts-that-actually-sync-a-creator-workflow-for-clean-mout), [Easton Dev audio guide](https://eastondev.com/blog/en/posts/ai/20251207-veo3-audio-generation-guide/)
- Alien sitcom craft: [Comedy.co.uk, fish-out-of-water](https://www.comedy.co.uk/pro/inside_track/fish-out-of-water-sitcom-format/)
- AI labels: [Engadget](https://engadget.com/2162426/instagram-is-testing-optional-ai-creator-labels), [MediaPost](https://www.mediapost.com/publications/article/414862/instagram-unveils-new-ai-creator-account-label.html)
- Recommendation Guidelines: [Instagram Help](https://help.instagram.com/313829416281232) (older page)
- Comedy and tropes: [IAFOR study](https://iafor.org/archives/journals/iafor-journal-of-media-communication-and-film/10.22492.ijmcf.7.1.02.pdf), [Milestone101](https://www.milestone101.com/lifestyle/The_Last_Laugh__Tracing_Hindi_Cinema_s_Fading_Funny_Bone)
- Trend context: [Fruit Love Island (Wikipedia)](https://en.wikipedia.org/wiki/Fruit_Love_Island), [IOL on Jean Phil](https://iol.co.za/technology/software-and-internet/2026-10-27-the-surprising-ai-influencer-behind-one-of-instagrams-biggest-meme-accountsand-its-a-crypto-push/)
