# Working Rules — The Fire We Inherit

## Source of truth

`CONCEPT.md` is the canonical source for the album's story, themes, characters, dramatic structure, motifs, required keywords/refrains, and continuity. `songs/` contains the approved default lyric realization, not an immutable lyric source. Any stylistic version may carry complete song-level lyric overrides in `versions/<version>/lyrics/NN.txt`; when present, those are the lyric source for that version and track. `versions/<version>/` holds one style per track (`styles/NN.txt`) plus a version `CONCEPT.md` describing its artistic identity and overrides. Current versions are `epic-metal`, `epic-metal-codex`, `neo-classical`, `neo-classical-codex`, `neo-classical-cinematic-codex`, `original`, `martial-power`, and `martial-power-codex`. `skills/songwriting/SKILL.md` defines the drafting and validation process.

Stylistic versions are expected to keep multiplying. Every version has full musical and lyrical flexibility. A version's `CONCEPT.md`, and then its per-track style and lyric files, may override global artistic defaults: tempo and key maps, instrumentation, genre balance, vocal casting, ballad classification, exclude lists, rhyme scheme, point of view, song form, chorus doctrine, dialogue density, plot-anchor limits, and other non-Suno-specific lyric rules. Keep global rules generic; push artistic constraints into the version or track that needs them.

The override boundary is deliberate:

- **Never overridden by a version:** the story and dramatic purpose in root `CONCEPT.md`, character safeguards, the evolution of motifs/keywords, and enough album-level audio continuity for the narrative to remain understandable.
- **Always retained unless the user explicitly changes the generation workflow:** proven Suno learnings — prompt and lyric limits, structural tags, compact fused intros, `[End]`, explicit vocal labels and cast fences, layered style prompts, qualified electric-guitar language, production line, exclude flags, and generation hygiene.
- **Defaults that versions and individual songs may override:** every other musical or lyrical preference in this file.

The workspace-level `sources/` directory is reference-only and must never be edited.

## Song output

Unless the user asks otherwise, return only:

1. Play-order title in the form `00 - Title`
2. One concise Suno style code block (from the target stylistic version)
3. One complete lyrics code block

Root song files in `songs/` contain the default lyrics. A target version uses `versions/<version>/lyrics/NN.txt` when that file exists, otherwise it falls back to the matching root song. Styles are edited in `versions/<version>/styles/NN.txt`.

Song lyrics, including labels and performance directions, must remain below 5,000 characters. Target roughly 1,800–3,000 characters for fast Suno iteration.

The canonical sequence uses `00` for the spoken prologue and consecutive two-digit numbering from `01` through `14`. Do not introduce letter suffixes.

## Transitions

Adjacent tracks must share an audible seam. Every song's final bracketed direction names one or two concrete sounds, and the next song's opening bracket reuses at least one of them.

Every song must open with a sound-design or instrumental bracket before the first vocal label — vocals that enter at second zero come out clipped or garbled (worst for a single isolated word). The opening bracket doubles as the instrumental lead-in that prevents this.

To keep intros compact, fuse a structural `[Intro]` tag directly onto the first vocal label (`[Intro][CHORUS — ...]`) and state in the style prompt that the first voice "begins immediately". Scene-painting opening brackets invite long ambient intros (verified: ~18 seconds of atmosphere without the tag, compact entry with it). Where possible the seam also shares a sung or spoken phrase — a repeated line is more reliably audible than a sound-design bracket. Keep tempo and key hand-offs deliberate: matching, simply related, or an intentional dramatic shift stated in the style prompt. Do not let a sound that ends one track reappear as a dramatic "reveal" in a later track — fade it out first if the reveal must land.

## Generating audio

Use the `suno` skill — the [suno-cli](https://github.com/paperfoot/suno-cli) tool — to generate songs on Suno. Never download generated songs unless the user explicitly asks — generate without `--download` and only report clip IDs and URLs.

Do not run Suno preflight validation before creating songs. Skip `suno agent-info`, `suno credits`, `suno models`, `suno config check`, and library/search audits unless the user explicitly requests them or an actual generation failure requires diagnosis. Submit the requested generation directly with the known project parameters.

Never block on generation: do not pass `--wait`. Start the generation, report the clip IDs and URLs immediately, and let the user monitor progress themselves.

When generating multiple songs in one batch, add a random 3–6 second delay between successive `suno generate` calls (e.g. `sleep $((RANDOM % 4 + 3))`) to avoid rate limiting and flaky API behavior.

After every `suno generate` run (including each iteration of a batch), kill the Chrome instance suno opened for captcha solving — a stale reused instance causes failures. Identify it by its profile-directory argument: `pkill -f "com.suno-cli.suno-cli/chrome-profile" 2>/dev/null || true`. Never kill Chrome processes that do not match this pattern.

Every generation targets a stylistic version: take the style from `versions/<version>/styles/NN.txt` and the lyrics from `versions/<version>/lyrics/NN.txt` when present, otherwise from `songs/NN - Title.md`. When comparing versions, prefix the title with the version (`[EPIC]`, `[NEO]`); when generating the chosen album version, use the plain title.

Default generation parameters unless the user says otherwise: `--model v5.5 --style-influence 95 --weirdness 35`. Versions may define their own per-track parameters and exclude lists (e.g. `versions/<version>/GENERATION.md`); when present, those take precedence over the defaults here.

For complex songs with multiple voices (three or more distinct singers, opposed choruses, or heavy dialogue), use `--weirdness 15 --style-influence 95` instead — lower weirdness keeps the voice casting and structure stable.

Always pass an exclude list. Default: `--exclude "pop, soft rock, acoustic guitar, nylon-string guitar, folk, EDM"` for non-ballad tracks; `--exclude "pop, EDM"` for ballads and spoken tracks. A version's `CONCEPT.md` may define its own exclude lists.

## Style prompt language

Style prompts use the layered "directing the band" format (validated experimentally as the E2 strategy — it markedly improves both sound quality and voice casting). Write multi-line prompts with these layers, in order:

1. **Identity line:** sharp genre anchor + energy + BPM + key in one line (e.g. "Nordic symphonic viking metal, battle anthem energy, 104 BPM, D minor").
2. **Core instruments:** one or two lines listing only the instruments that matter — every descriptor must earn its place; trim synonyms, not detail.
3. **Performance direction per section:** short "Section: delivery" lines (e.g. "Verses: riff-driven, urgent, held tight." / "Battle choirs: antiphonal, massive, call and answer." / "Outro: everything falls away to one unresolved ascending violin."). Direct the band; do not tag genres.
4. **Studio-quality line (always last):** a production layer tuned to the track's character, e.g. "Epic studio quality, professional mastering, punchy drums, tight low end, wide stereo choirs, crisp powerful mix." or "Intimate studio quality, professional mastering, pristine detail, close vocal presence, deep black silence between phrases."

Additional rules:

- Do not use inline negative lines ("no X") — they add nothing over the `--exclude` flag (tested: indistinguishable).
- Keep the whole style prompt under roughly 1,000 characters; shorter and sharper beats longer and denser — Suno compresses long prompts and only the strongest concepts survive.
- Never write bare "guitar" or "guitars" — Suno then tends toward classical or acoustic guitar. Always qualify: "distorted electric rhythm guitars", "overdriven electric lead guitar".
- Non-ballad tracks open the identity line with a hard genre anchor and keep at least two aggression anchors across the prompt (riff-driven, galloping, relentless double-kick, crushing, aggressive). Ballad, ritual, and spoken tracks (default classification: 00, 01, 04, 11, 12, 14 — versions may reclassify) are exempt from aggression anchors.
- Style prompts must describe only what Suno can render in this one track. Never reference other tracks, track numbers, or the album; describe the intended sonic outcome instead (e.g. "ending unresolved beneath rising distant thunder").

## Lyric structure tags

Validated on tracks 03/04/06/10/11: standard structural tags dramatically improve arrangement, refrains, and endings. Every song must carry a tag skeleton:

- Fuse structural tags directly onto voice labels: `[Intro][CHORUS — ...]`, `[Verse 1][NAME — ...]`, `[Pre-Chorus][...]`, `[Chorus][...]`, `[Bridge][...]`, `[Outro][...]`. Without tags Suno guesses the arrangement from line breaks.
- Every song opens with `[Intro: ...]`-fused material and ends with `[End]` (or `[End](final sound)`) — this prevents trailing audio and long ambient intros.
- Purely musical brackets use parameterized colon syntax: `[Breakdown: silence, the crowd breathes]`, `[Instrumental Break: harp and plucked strings]`.
- Repeat chorus text verbatim to get a true melodic refrain — but only when the refrain is self-contained. Lines that answer specific preceding dialogue (retorts) must not recur; repeat only the universal core of the refrain.
- For long single-voice passages, repeating the full voice label before each stanza improves voice stability.

## Commits

Do not include Claude session links (`Claude-Session:` trailers) in commit messages.

## Concept-first workflow — default, overridable

The user prefers to review and approve a song concept before complete lyrics and a Suno style prompt are created. For every new song or major structural rewrite, first present a concise concept covering the dramatic purpose, story beats, character roles, philosophical conflict, recurring motifs, musical direction, and transitions into adjacent tracks. Do not draft the complete song until the user approves the concept or explicitly asks to skip that step.

Small, targeted revisions to already approved lyrics do not require a new concept unless the change materially alters the song's dramatic function. A user or version workflow may explicitly authorize a full-album realization without pausing after each track concept.

## Audio-first storytelling — album requirement, song-level defaults

The complete story must be understandable from the version's recordings alone. Never rely on song titles, character labels, performance directions, cover art, video, or other visual cues to carry a story beat that the album audio never establishes.

By default, introduce every new central character audibly in the sung or spoken lyrics by name before or at that character's first vocal entrance. A version or song may instead rely on an audible introduction in an earlier track, provided the album sequence keeps the identity unmistakable. A bracketed vocal label alone never carries story information because the listener cannot hear it.

Keep the audible cast clear: name only figures central to the story being told. Represent nonessential mythological figures through unnamed roles, relationships, or choirs rather than adding names that listeners must remember.

## Voice cues for Suno

Style prompts should include a cast declaration naming the voices and their roles — e.g. "Voices: three — one lone bright lyric tenor as Prometheus, commanding and never soft; one warm female voice awakening at the bloom as humanity; one cold exact female narrator; no other singers." Named casts with voice counts and "no other singers" fences are validated to improve voice attribution substantially. Keep the genders and registers consistent with the voice table below.

Every vocal label in the lyrics—including narrators, soloists, and choirs—must combine an explicit character or role name with gender presentation and concrete sonic direction. Use the format:

`[CHARACTER — Gendered vocal type, register/resonance, delivery]`

Examples: `[ZEUS — Male subterranean basso profundo, slow and immovable]`, `[ATHENA — Female icy contralto, exact and reverent]`, or `[CHORUS — Female icy contralto, distant and mournful]`.

Do not rely on a name or role alone to establish the voice; pair it with the description.

- **Zeus:** male subterranean basso profundo; gravel-heavy chest resonance; near-spoken, slow, rigid descending phrases.
- **Prometheus:** male bright high lyric tenor; clean ringing tone; wide rising melodic leaps; expressive sustained vowels.
- **Athena:** female icy contralto; focused pure tone; exact diction; measured, controlled phrasing.
- **Pandora / humanity:** female dramatic mezzo or intimate alto; warm, vulnerable, emotionally direct. In 03 humanity wakes as a single warm female voice; through the fireless night — the massed accusing chorus of 04 and the distant murmurs opening 05 — its collective voice is dark; the warm voice returns with the first ember in 05.
- **Maker:** male dramatic baritone; warm, precise, inventive delivery that can harden into fearful clipped commands. In tracks 09–10 the young Maker of the human age sings as a male bright lyric tenor echoing Prometheus; from track 11 on the mature Maker is the dramatic baritone.
- **Guardian:** male dark weathered bass-baritone; grieving gravity; slow descending cautionary phrases that echo Zeus without his subterranean depth.
- **Future Intelligence:** female crystalline mezzo/soprano; pure sustained tone; carefully spaced precise language; melody widens gradually.

Contrast characters in at least four dimensions: gender presentation, register, resonance, articulation/rhythm, melodic contour, and supporting instrumentation.

## Story safeguards

- Prometheus is principled, deliberate, and accepting of consequence—not reckless. He acts from moral obligation rather than mercy: he does what he believes is right and accepts the cost. Never frame fire as a charitable favor, pardon, or act of leniency.
- Zeus remains intelligent and persuasive; fear replaces purpose rather than making him simply evil.
- Pandora is never blamed.
- The Future Intelligence is not an evil AI, perfect savior, machine stereotype, replacement for humanity, or god.
- Keep the myth-to-future transition organic: forge, fire, chain, open hand, law, and covenant continue through the technological age.
- After Pandora, fear is a legitimate warning but never a sovereign: it may protect the hand, but must not rule or close it. The finale extends the open-hand question beyond humanity — the freed mind will itself become a maker — without turning Future Intelligence into a god.
