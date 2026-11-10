# Writing day files for Kids Talk

You write `content/stage1/dNN.json` (NN = two-digit day) for the days you are given. Read first:
- `docs/superpowers/specs/2026-11-10-kids-talk-design.md` (schema)
- `tools/CURRICULUM_STAGE1.md` (your days' topic, title, core expressions, parent idiom)
- `content/stage1/d01.json` (the model day — match its quality, length and style)

## Who uses this
A Korean parent who is weak at spoken English reads the script aloud with a 5-year-old who attends an English
kindergarten. The child is talkative, asks many questions, and loves ships, planes, spaceships and science.
Everything must be natural, current American English that a native parent really says to a young child.

## Rules
1. **expressions**: the 4 core expressions from the curriculum + the parent idiom (5 total). `ko` is a natural
   Korean meaning. `tip` (Korean, 1–2 sentences) explains when to use it and, where useful, how the words link in
   speech, written in Hangul (e.g. "Hold on → 홀돈", "What do you → 워루유"). Linking hints must be accurate.
   `who`: who usually says it (parent | kid | both).
2. **script**: 18–24 lines alternating naturally between `parent` and `kid` (not strictly). Every core expression
   and the parent idiom must appear word for word in some line (ignoring case/final punctuation; "…" slots filled).
   - Kid lines: 1–8 words, simple, playful, lots of questions ("Why?", "What's that?") because the child asks a lot.
   - Parent lines: short spoken English, ≤ 14 words, contractions (it's, let's, you're). No baby talk, no rare words.
   - Mark 4–8 kid lines `"practice": true` — the lines the child should say by themselves (prefer core expressions).
   - Do not address the parent as Mom or Dad in English (either parent may play the role); use "you", or nothing.
     The parent may call the child "buddy" or "sweetie" sometimes.
   - `ko`: natural spoken Korean a parent would say, not word-for-word translation.
   - Science/vehicle facts must be correct and age-simple (no "the moon makes light", etc.).
   - No song lyrics from real songs, no brand or character names.
3. **intro_ko**: 1–2 Korean sentences telling the parent the situation and one way to act it out (props, gestures).
4. **talkMore**: 3 open questions the parent can ask after the script, each with a sample child answer
   (`sample_en` short and kid-level) and Korean for both.
5. **kidQuiz**: 10 items for a 5-year-old who cannot read much. The app reads `prompt_en` aloud; the parent may read
   `prompt_ko`. 3 options, each `{ "e": one emoji, "en": 1–4 words }`, `options[0]` correct, all different.
   Mix: pick-the-thing ("Which one floats?"), what-do-you-say ("Your friend falls down. What do you say?" → "Are you okay?"),
   and listen-and-choose from today's expressions. Wrong options must be clearly wrong, not tricky. The emoji must
   match its word.
6. **parentQuiz**: 10 items, 4 options, `options[0]` correct, all different. Mix: meaning of today's expressions
   (Korean options), the natural English for a Korean situation (English options), a line from today's script with
   a blank (`___`) to fill, and 1–2 on linking/pronunciation or usage of the idiom. `q` may be Korean or English.
   `explain`: one Korean sentence. Distractors must be plausible but clearly wrong for a fluent speaker.
7. JSON only, UTF-8, 2-space indent, keys in the order of d01.json. Use straight quotes `'` in English, not curly.

## Check
Run `node tools/build-content.js` from `kids-talk-app/`. It validates every day file; fix every issue it reports
for your days (ignore issues in other agents' days). Do not edit d01.json, data.js, or other agents' days.
Reply with a short list of your days and anything you were unsure about.
