# Working Rules — The Fire We Inherit

## Source of truth

`CONCEPT.md` is the canonical source for the album's story, themes, characters, dramatic structure, motifs, and continuity. `songs/` contains the current approved draft for each track. `skills/songwriting/SKILL.md` defines the drafting and validation process. The workspace-level `sources/` directory is reference-only and must never be edited.

## Song output

Unless the user asks otherwise, return only:

1. Play-order title in the form `00 - Title`
2. One concise Suno style code block
3. One complete lyrics code block

Song lyrics, including labels and performance directions, must remain below 5,000 characters. Target roughly 1,800–3,000 characters for fast Suno iteration.

The canonical sequence uses `00` for the spoken prologue and consecutive two-digit numbering from `01` through `14`. Do not introduce letter suffixes.

## Transitions

Adjacent tracks must share an audible seam. Every song's final bracketed direction names one or two concrete sounds, and the next song's opening bracket reuses at least one of them.

Every song must open with a sound-design or instrumental bracket before the first vocal label — vocals that enter at second zero come out clipped or garbled (worst for a single isolated word). The opening bracket doubles as the instrumental lead-in that prevents this.

To keep intros compact, fuse a structural `[Intro]` tag directly onto the first vocal label (`[Intro][CHORUS — ...]`) and state in the style prompt that the first voice "begins immediately". Scene-painting opening brackets invite long ambient intros (verified: ~18 seconds of atmosphere without the tag, compact entry with it). Where possible the seam also shares a sung or spoken phrase — a repeated line is more reliably audible than a sound-design bracket. Keep tempo and key hand-offs deliberate: matching, simply related, or an intentional dramatic shift stated in the style prompt. Do not let a sound that ends one track reappear as a dramatic "reveal" in a later track — fade it out first if the reveal must land.

## Generating audio

Use the `suno` skill (the `suno` CLI) to generate songs on Suno. Never download generated songs unless the user explicitly asks — generate without `--download` and only report clip IDs and URLs.

Never block on generation: do not pass `--wait`. Start the generation, report the clip IDs and URLs immediately, and let the user monitor progress themselves.

When generating multiple songs in one batch, add a random 3–6 second delay between successive `suno generate` calls (e.g. `sleep $((RANDOM % 4 + 3))`) to avoid rate limiting and flaky API behavior.

After every `suno generate` run (including each iteration of a batch), kill the Chrome instance suno opened for captcha solving — a stale reused instance causes failures. Identify it by its profile-directory argument: `pkill -f "com.suno-cli.suno-cli/chrome-profile" 2>/dev/null || true`. Never kill Chrome processes that do not match this pattern.

Default generation parameters unless the user says otherwise: `--model v5.5 --style-influence 95 --weirdness 35`.

For complex songs with multiple voices (three or more distinct singers, opposed choruses, or heavy dialogue), use `--weirdness 15 --style-influence 95` instead — lower weirdness keeps the voice casting and structure stable.

Always pass an exclude list: `--exclude "pop, soft rock, acoustic guitar, nylon-string guitar, folk, EDM"` for non-ballad tracks; `--exclude "pop, EDM"` for ballads and spoken tracks.

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
- Non-ballad tracks open the identity line with a hard genre anchor and keep at least two aggression anchors across the prompt (riff-driven, galloping, relentless double-kick, crushing, aggressive). Ballad, ritual, and spoken tracks (currently 00, 01, 10, 11, 13, 14) are exempt from aggression anchors.
- Style prompts must describe only what Suno can render in this one track. Never reference other tracks, track numbers, or the album; describe the intended sonic outcome instead (e.g. "ending unresolved beneath rising distant thunder").

## Concept-first workflow

The user prefers to review and approve a song concept before complete lyrics and a Suno style prompt are created. For every new song or major structural rewrite, first present a concise concept covering the dramatic purpose, story beats, character roles, philosophical conflict, recurring motifs, musical direction, and transitions into adjacent tracks. Do not draft the complete song until the user approves the concept or explicitly asks to skip that step.

Small, targeted revisions to already approved lyrics do not require a new concept unless the change materially alters the song's dramatic function.

## Audio-first storytelling

The complete story must be understandable from the recording alone. Never rely on a song title, character label, performance direction, cover art, video, or other visual cue to explain who is speaking or what has happened.

Introduce every new central character audibly in the sung or spoken lyrics by name before or at that character's first vocal entrance. Give enough immediate context to establish the character's role or relationship to the conflict. A bracketed vocal label does not count as an introduction because the listener cannot hear it.

Keep the audible cast clear: name only figures central to the story being told. Represent nonessential mythological figures through unnamed roles, relationships, or choirs rather than adding names that listeners must remember.

## Voice cues for Suno

Do not place character names, gender presentation, or vocal-register mapping in the Suno style prompt. Style prompts describe only genre, tempo, key, arrangement, instrumentation, atmosphere, and vocal ensemble texture.

Every vocal label in the lyrics—including narrators, soloists, and choirs—must combine an explicit character or role name with gender presentation and concrete sonic direction. Use the format:

`[CHARACTER — Gendered vocal type, register/resonance, delivery]`

Examples: `[ZEUS — Male subterranean basso profundo, slow and immovable]`, `[ATHENA — Female icy contralto, exact and reverent]`, or `[CHORUS — Female icy contralto, distant and mournful]`.

Do not rely on a name or role alone to establish the voice; pair it with the description.

- **Zeus:** male subterranean basso profundo; gravel-heavy chest resonance; near-spoken, slow, rigid descending phrases.
- **Prometheus:** male bright high lyric tenor; clean ringing tone; wide rising melodic leaps; expressive sustained vowels.
- **Athena:** female icy contralto; focused pure tone; exact diction; measured, controlled phrasing.
- **Pandora / humanity:** female dramatic mezzo or intimate alto; warm, vulnerable, emotionally direct.
- **Maker:** male dramatic baritone; warm, precise, inventive delivery that can harden into fearful clipped commands. In tracks 08–09 the young Maker of the human age sings as a male bright lyric tenor echoing Prometheus; from track 10 on the mature Maker is the dramatic baritone.
- **Guardian:** male dark weathered bass-baritone; grieving gravity; slow descending cautionary phrases that echo Zeus without his subterranean depth.
- **Future Intelligence:** female crystalline mezzo/soprano; pure sustained tone; carefully spaced precise language; melody widens gradually.

Contrast characters in at least four dimensions: gender presentation, register, resonance, articulation/rhythm, melodic contour, and supporting instrumentation.

## Story safeguards

- Prometheus is principled, deliberate, and accepting of consequence—not reckless. He acts from moral obligation rather than mercy: he does what he believes is right and accepts the cost. Never frame fire as a charitable favor, pardon, or act of leniency.
- Zeus remains intelligent and persuasive; fear replaces purpose rather than making him simply evil.
- Pandora is never blamed.
- The Future Intelligence is not an evil AI, perfect savior, machine stereotype, replacement for humanity, or god.
- Keep the myth-to-future transition organic: forge, fire, chain, open hand, law, and covenant continue through the technological age.
- After Pandora, fear is a legitimate warning but never a sovereign: it may protect the hand, but must not rule or close it. The final spoken epilogue extends the open-hand question beyond humanity without turning Future Intelligence into a god.
