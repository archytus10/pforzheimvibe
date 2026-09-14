# HANDOFF

**Read this first in a new session.** Everything below is current as of the last commit
on `claude/sports-psychology-transcript-pwdedw`.

---

## What this repo is

Video scripts adapted from long-form source transcripts, plus the generated footage for
them. Two separate projects:

| Project | Path | State |
|---|---|---|
| **The Invisible Game** — 9-part sports psychology series | `scripts/invisible-game/README.md` | Scripts done. Ep 9 produced. |
| **Floating for Peak Athletic Performance** — 3-min float therapy promo | `scripts/floating/README.md` | Script done. 5 of ~16 shots generated. |

Dead work, kept only for history: `scripts/the-loop-*.md` and
`scripts/level-one-athlete.md`. The first two came from a Joscha Bach interview that was
abandoned as **too abstract and theoretical** — that transform failed and should not be
revived. `level-one-athlete.md` is superseded by the series.

---

## The immediate next step

The user set the cloud environment's **Network access** to **Full** so that `fal.ai`
becomes reachable. They want to switch video generation from Higgsfield to
**fal.ai `minimax/h3-max-turbo/text-to-video`**
(https://fal.ai/models/minimax/h3-max-turbo/text-to-video).

- Endpoint that was refused under the old policy: `https://queue.fal.run/fal-ai/minimax/h3-max-turbo/text-to-video`,
  `Authorization: Key <key>`.
- **The API key is not in this repo and must not be.** The user supplied one in the previous
  session and said they would rotate it. Ask them for the current key; keep it in the
  scratchpad or an env var, never a committed file.
- First thing to do: verify fal is now reachable, then continue the floating shot list
  on that model instead of Higgsfield.

---

## Floating project — production state

Script, timings and shot list: `scripts/floating/README.md`.
Visual board artifact: https://claude.ai/code/artifact/0354ad45-5b22-40bf-80ff-e15e2de099d6

Format: **16:9**, 720p, 8s per shot unless the user names a length. Casting for every
shot: **African American college football athletes**, late teens to early twenties.

### Shots generated so far (Higgsfield `minimax_h3_max`, 768p)

| # | Shot | URL |
|---|---|---|
| 01 | Sled push, indoor turf (rendered at 2K) | https://d8j0ntlcm91z4.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/hf_20260913_155038_d0397703-b1c6-40b0-a7e6-9f11d4ce42b8.mp4 |
| 02 | Weight room, heavy rep | https://d8j0ntlcm91z4.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/hf_20260913_165634_14958df6-931f-44ca-a0d3-309c3836d98f.mp4 |
| 03 | Still water, slow ripple | https://d8j0ntlcm91z4.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/hf_20260913_165920_cbd39643-69a1-438a-894e-dac57fc5604b.mp4 |
| 04 | Float room at rest, lid open | https://d8j0ntlcm91z4.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/hf_20260913_170554_f67c6d73-9585-4c8c-a149-805426aeead8.mp4 |
| 05 | Athlete enters the float room | https://d8j0ntlcm91z4.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/hf_20260913_171430_153abdad-3443-4439-a04e-093c196ece6b.mp4 |

Shot 05 was regenerated using **the last frame of shot 04 as a start image**, so the pod
and room match. Do the same for every remaining tank shot — generated tank interiors
otherwise drift, and they already do not match the user's real facility.

Section 1 (0:00–0:30) is complete with shots 01–04. Shot 05 opens section 2.
Remaining: shots 06–16, listed in the floating README and the artifact.

---

## The Invisible Game — production state

Scripts and per-episode source mapping: `scripts/invisible-game/README.md`.

Format: **9:16 vertical**, 768x1344. Narration voice is **fixed across the series** —
Cillian, `d8ba9f14-8a24-44db-932b-99e16c45bd32`, `preset`, via `text2speech_v2` with
`variant: elevenlabs`. Do not change it mid-series.

Every episode opens with the same ~27s **series cold open** (words and footage identical
each time). It is locked; re-cutting it means re-cutting all nine.

| Ep | Version | Link |
|---|---|---|
| 9 | v2, with cold open — current | https://d2ol7oe51mr4n9.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/66e07dfd-caa1-47cd-85ca-c475777d646e.mp4 |
| 9 | v1, no cold open — superseded | https://d2ol7oe51mr4n9.cloudfront.net/user_2yAUxnXAFoiK8f5HAU8aI7XdD8t/79846e54-01b8-4ccc-8a39-ac31d60912bc.mp4 |

Episodes 1–8 are written but not produced.

---

## Standing preferences

- **Answer in one plain-English sentence** unless more is explicitly asked for. The user
  set this rule and it holds.
- **Write simply.** An earlier draft opened a video on Gödel and non-converging functions
  and was rejected as too theoretical. The social intelligence source says it directly:
  short sentences, no jargon, don't try to sound smart.
- **Runtime is a ceiling, not a target.** 60–90s is fine, up to two minutes where the
  material earns it. Do not pad or amputate to hit a round number.
- Measure read times from actual word counts. The synthetic narrator reads at about
  **152 wpm**, slower than typical estimates — a script that "looks like" 60s runs 70.
- Commit and push after every substantive change; a stop hook enforces it.

## Gotchas that cost time last session

- **Git author must be `archytus10@users.noreply.github.com`.** The account blocks pushes
  that would expose a private email; a real address fails with GH007.
- **This container cannot fetch the Higgsfield CDN** (`d2ol7oe51mr4n9.cloudfront.net` was
  403 through the egress proxy), so finished videos cannot be attached in chat — hand the
  user the URL. Verify files from inside the Higgsfield sandbox instead.
- **No music.** Higgsfield's audio tool generates speech only and forbids its music model
  for standalone audio. Mixes are left at -16 LUFS / -1.5 dBTP for a licensed bed to be
  added by hand.
- Higgsfield often answers a generation with a **preset recommendation** ("IN THE DARK")
  instead of a job; resubmit with `declined_preset_id` set to that preset's id.
- Higgsfield `minimax_h3` at 2K took ~4.5 min per clip versus ~20s at 768p. Not worth it.

## Sources

- Floating: script supplied directly by the user, recorded verbatim.
- The Invisible Game: "The Ultimate Guide to Social Intelligence (Most People Are Level 1)",
  https://www.youtube.com/watch?v=L_szxpxvANM — channel name unconfirmed, YouTube is
  blocked from the session so it could not be verified.
