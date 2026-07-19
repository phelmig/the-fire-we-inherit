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

Adjacent tracks must share an audible seam. Every song's final bracketed direction names one or two concrete sounds, and the next song's opening bracket reuses at least one of them. Where possible the seam also shares a sung or spoken phrase — a repeated line is more reliably audible than a sound-design bracket. Keep tempo and key hand-offs deliberate: matching, simply related, or an intentional dramatic shift stated in the style prompt. Do not let a sound that ends one track reappear as a dramatic "reveal" in a later track — fade it out first if the reveal must land.

## Generating audio

Use the `suno` skill (the `suno` CLI) to generate songs on Suno. Never download generated songs unless the user explicitly asks — generate without `--download` and only report clip IDs and URLs.

Never block on generation: do not pass `--wait`. Start the generation, report the clip IDs and URLs immediately, and let the user monitor progress themselves.

When generating multiple songs in one batch, add a random 3–6 second delay between successive `suno generate` calls (e.g. `sleep $((RANDOM % 4 + 3))`) to avoid rate limiting and flaky API behavior.

Always pass `--style-influence 85 --weirdness 19` on every `suno generate` call.

Default generation parameters unless the user says otherwise: `--model v5.5 --style-influence 85 --weirdness 20`.

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
- **Maker:** male dramatic baritone; warm, precise, inventive delivery that can harden into fearful clipped commands.
- **Future Intelligence:** female crystalline mezzo/soprano; pure sustained tone; carefully spaced precise language; melody widens gradually.

Contrast characters in at least four dimensions: gender presentation, register, resonance, articulation/rhythm, melodic contour, and supporting instrumentation.

## Story safeguards

- Prometheus is principled, deliberate, and accepting of consequence—not reckless. He acts from moral obligation rather than mercy: he does what he believes is right and accepts the cost. Never frame fire as a charitable favor, pardon, or act of leniency.
- Zeus remains intelligent and persuasive; fear replaces purpose rather than making him simply evil.
- Pandora is never blamed.
- The Future Intelligence is not an evil AI, perfect savior, machine stereotype, replacement for humanity, or god.
- Keep the myth-to-future transition organic: forge, fire, chain, open hand, law, and covenant continue through the technological age.
- After Pandora, fear is a legitimate warning but never a sovereign: it may protect the hand, but must not rule or close it. The final spoken epilogue extends the open-hand question beyond humanity without turning Future Intelligence into a god.
