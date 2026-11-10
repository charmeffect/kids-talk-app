# Kids Talk — design (2026-11-10)

## Goal
A daily 20–30 minute English conversation routine for a parent and child, done after kindergarten/school.
The child is 5 (English kindergarten), talkative, loves ships, planes, spaceships and science. The parent is
weak at spoken English and everyday idioms, so every line carries a Korean translation and a tip, and every line
can be heard aloud. Content runs from age 5 to grade 6 (9 stages), built ahead of time one quarter at a time.

## Decisions (approved by the user)
- Content is written in advance (in Claude Code sessions), not generated live in the app.
- Format: parent–child role-play script. No comprehension questions inside the script.
- After each day: 10 quiz items for the child and 10 for the parent.
- Pronunciation: the device's speech voices now (best available voice), with an mp3 hook for later replacement.
- Schedule: 5 days a week (20 per month). First delivery: stage 1, months 1–3 (60 days).

## Stages
| Stage | Age / grade | Status |
|---|---|---|
| 1 | age 5 (7세반 전) | months 1–3 in this delivery |
| 2 | age 6 | later |
| 3 | age 7 | later |
| 4–9 | grade 1–6 | later, renewed each year |

## Day content (`content/stage1/dNN.json`, one file per day — source of truth)
```json
{
  "stage": 1, "day": 1,
  "topic": "daily | ships | planes | space | science",
  "title_en": "How was your day?", "title_ko": "오늘 하루 어땠어?",
  "intro_ko": "One or two sentences for the parent: the situation and how to play it.",
  "expressions": [
    { "en": "How was your day?", "ko": "오늘 어땠어?", "tip": "Parent tip in Korean (usage, linking: How-was-your → '하우워즈유어')", "who": "parent|kid|both" }
  ],
  "script": [
    { "who": "parent|kid", "en": "…", "ko": "…", "practice": true }
  ],
  "talkMore": [ { "en": "What was the best part?", "ko": "…", "sample_en": "…", "sample_ko": "…" } ],
  "kidQuiz": [ { "prompt_en": "…", "prompt_ko": "…", "options": [ { "e": "🚀", "en": "rocket" }, … 3 ] } ],
  "parentQuiz": [ { "q": "…", "options": ["correct", "…", "…", "…"], "explain": "…" } ]
}
```
- 4–5 expressions (one is an everyday idiom/phrasal phrase useful to the parent).
- Script 18–24 lines; child lines short (1–8 words); 4–8 child lines marked `practice` ("아이가 말해보기").
- `talkMore`: 3 open follow-up questions with a sample child answer, to stretch the talk to 20–30 minutes.
- `kidQuiz`: 10 items, 3 options, `options[0]` correct (shuffled on screen); played aloud, chosen by emoji + word.
- `parentQuiz`: 10 items, 4 options, `options[0]` correct; meaning, natural response, fill-in from the script.
- Optional `audio` on any script line (`"audio": "audio/s1d01-03.mp3"`) — played instead of the device voice.

`tools/build-content.js` validates every day file and writes `data.js` (`const KIDS_TALK = {...}`), like friends-app.
Curriculum (topics and target expressions for days 1–60): `tools/CURRICULUM_STAGE1.md`. Writing rules: `tools/CONTENT_BRIEF.md`.

## App (`index.html`, vanilla, Korean UI)
- Home: stage picker (1–9; unbuilt stages shown as "준비 중"), "오늘 할 차례" card = first unfinished day,
  calendar by month → week → day with ✓ marks, weekend review card per week.
- Day screen, in order: 오늘의 표현 (expression cards with 🔊 / slow 🐢) → 역할극 대본 (each line: speaker, English,
  Korean (toggle to hide), 🔊; practice lines highlighted "아이가 말해보기"; "전체 듣기" plays the script in order)
  → 더 이야기하기 → 아이 퀴즈 → 부모 퀴즈 → 완료.
- Settings: parent role 엄마/아빠 (voice gender), speech speed, Korean shown/hidden, voice check + iPhone guide
  for downloading enhanced/premium voices (Settings → Accessibility → Spoken Content → Voices → English).
- Speech: Web Speech API; pick the best en-US voice (enhanced/premium/natural first); parent voice by role gender;
  child voice = a different voice with higher pitch. Audio file used first when present.
- Weekend review: the week's expressions as flashcards + 10 mixed quiz items from that week.
- Progress in localStorage (`kids_talk_progress`): finished days, quiz scores.

## Deployment
Own repo `charmeffect/kids-talk-app`, GitHub Pages, like the other apps.

## Testing
- `node tools/build-content.js` must report 0 issues.
- Headless-Chrome smoke test (`tools/smoke-test.html`) drives home → day → quizzes → completion.
