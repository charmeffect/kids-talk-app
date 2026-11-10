# Reviewing Kids Talk day files

You review and fix existing day files in `content/stage1/` (your day range is given). First read
`tools/CONTENT_BRIEF.md` (the writing rules) and `content/stage1/d01.json`. Then read each of your files in full
and fix problems **in place** (keep the schema, key order and 2-space style). Check:

1. **English**: natural, current American English a native parent says to a 5-year-old. Fix stiff, British,
   bookish or grammatically wrong lines. Kid lines stay short.
2. **Korean**: `ko` translations match the English and sound like natural spoken Korean. Fix mistranslations.
3. **Linking/pronunciation hints** in `tip` and parent quiz: they must be accurate for American English
   (flap t, dropped h in "him/her", "did you" → 디쥬, "want to" → 워너, "get it" → 게릿). Fix or remove a
   wrong hint. A pronunciation quiz question whose "correct" answer is doubtful → rewrite the question as a
   meaning/usage question.
4. **Facts**: science, space, vehicle and nature facts must be correct (simplified is fine, wrong is not).
5. **Quizzes**: `options[0]` must be clearly correct and every other option clearly wrong; nothing ambiguous,
   no trick for a 5-year-old; each emoji must show its word; avoid emoji newer than 2021 (Unicode 14+, e.g.
   🪽 🪏 🫎). A "Which is NOT…" question is allowed only if the prompt says so explicitly.
6. **Consistency**: the 5 expressions still appear word for word in the script after your edits.

Do not rewrite content that is fine; make the smallest fix. Do not touch files outside your range or data.js
by hand. Run `node tools/build-content.js` at the end — it must report 0 issues.
Reply with a compact list: file → what you changed (one line each), and anything you left unsure.
