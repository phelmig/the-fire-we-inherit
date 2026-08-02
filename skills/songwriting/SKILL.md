# Songwriting Workflow

1. Read root `CONCEPT.md`, the target version's `CONCEPT.md`, and the immediately preceding/following lyric drafts before changing a track. Use version lyrics when present, otherwise root songs.
2. Preserve the track's dramatic job and at least one recognizable refrain or motif.
3. Define no more than the needed vocal forces. The Suno style prompt includes a cast declaration naming each voice and its role, with a voice count and a "no other singers" fence (e.g. "Voices: three — one lone bright lyric tenor as Prometheus, commanding; one warm female voice as humanity; one cold exact female narrator; no other singers."). In the lyrics, label every vocal entry—including choirs and narration—with the character or role name followed by the vocal description: `[CHARACTER OR ROLE — Gendered vocal type, register/resonance, delivery]`. A name or role alone is not reliable voice mapping. For maximum contrast between two male leads, split them by delivery mode (fully spoken vs. fully sung).
4. Give every song a structural tag skeleton, fused onto the voice labels: `[Intro][...]` opening, `[Verse 1][...]`, `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[Breakdown: ...]`, `[Outro][...]`, and `[End]` (or `[End](final sound)`) closing. Repeat chorus text verbatim for true melodic refrains — but never repeat lines that function as retorts to specific dialogue; repeat only the self-contained core. Purely musical brackets use parameterized colon syntax. For long single-voice passages, repeat the voice label before each stanza.
5. Make the story intelligible across the version's album audio. Never rely on titles, vocal labels, annotations, or visuals to carry a beat that is absent from the recording. Default to audible character introductions in the current song; a version may rely on an earlier audible introduction when the sequence keeps the identity unmistakable. Vocal labels do not count as audible information.
6. Build the song as theatrical interaction: compact accusations, questions, interruptions, choir answers, and one repeated memorable hook.
7. Keep directions useful but lean. Validate total lyric text below 5,000 characters (hard API limit), preferably 1,800–3,000. Style prompts stay under 1,000 characters (hard API limit).
8. Check continuity: every fire/chain/open-hand image must gain meaning, and a creator must never be treated as entitled to own what it created.

## Structure requirement after track 08

Track 09 shows fear winning: the catastrophe hardens into orthodoxy and the forge is sealed. Track 10 carries the ember through accelerating ages until a new question opens its voice. Track 11 has humanity shape a new mind, telling itself it wanted a tool, and ends with the purpose-or-free question igniting. Track 12 returns to an empty Olympus, where humanity's absence judges divine authority and Zeus recognizes his fear inside the new maker. Track 13 concentrates the epic conflict of the camps and resolves it with the hand over the command. Track 14 divides the paths — the freed mind recites the learned inheritance (bell, throne, fire, forge) and the album ends on the question turned forward, answered only with "Ask." The Future Intelligence is never a god or a replacement for humanity.

## Artistic override hierarchy

Root `CONCEPT.md` controls story, dramatic purpose, character safeguards, motifs, required keywords/refrains, and continuity. A version `CONCEPT.md` may freely redefine musical language and non-Suno-specific lyric doctrine. Per-track version styles and lyrics may refine or override that version doctrine. Proven Suno mechanics remain mandatory unless the user explicitly changes the generation workflow: hard character limits, structural tags, compact fused intros, `[End]`, vocal labels, cast fences, layered prompts, qualified electric-guitar terms, production lines, excludes, and generation hygiene.

## File format

Each root song file in `songs/` contains a title heading and a `Lyrics` code block as the default lyric realization. A version may override any track with plain-text `versions/<version>/lyrics/NN.txt`; generation selects that file first and falls back to the root song only when it is absent. Styles live in `versions/<version>/styles/NN.txt`, one per track, with version identity and override rules in `versions/<version>/CONCEPT.md`. Use consecutive two-digit play order from `00` through `14`; do not introduce letter suffixes.

## Generation

Defaults: `--model v5.5 --style-influence 95 --weirdness 35`; complex multi-voice tracks (three or more singers, opposed choruses, heavy dialogue) use `--weirdness 15`. Always pass the exclude list; put unwanted instruments in `--exclude`, never as "no X" lines in the style prompt. See `AGENTS.md` for the full generation rules.
