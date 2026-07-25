# The Fire We Inherit — Martial Power Version

The album rendered as martial heavy power metal war anthems: every track a
single-message battle hymn built to be sung along, telling the story in broad
heroic strokes.

## Sound identity

- **Anchor (every track):** "Martial heavy power metal war anthem / march,
  *[energy]*, *[tempo/key]*."
- **Shared palette:** chugging distorted electric rhythm guitars, relentless
  double-kick, martial snare, massive synth-brass and keyboard wall, pounding
  electric bass.
- **Production signature:** "Epic studio quality, professional mastering,
  punchy modern metal mix, thick keyboard-brass wall, loud guitars, massive
  gang choirs."

## Song doctrine (validated on 02, 05, 06, 09)

- **Message-first:** each track carries ONE key message; no dialogue
  back-and-forth. One lead perspective start to finish. Other characters
  appear only as quoted lines inside the narration, or as a single cry
  answered once by the choir.
- **Lead voice:** one gruff powerful male baritone (war-narrator or
  first-person hero). The choir is a force — the court, the law, the army,
  the awakening world — never a conversation partner.
- **Choruses:** long galloping AABB singalong lines, repeated verbatim (3×);
  short shouted chants as pre-chorus. The hook states the track's message.
- **Lyrics are version-specific:** this version carries its own compact
  (~1,800–2,400 chars) message-first lyric variants in `lyrics/NN.txt`.
  The repo-root `songs/` directory remains the canonical story text; these
  variants preserve its story beats, audible name introductions, and seams
  (opening/closing brackets) while compressing everything else into hooks.
- **Warm female voice** appears only where the story demands it (the 05
  ignition bloom); everything else stays male-voiced.
- Dark chapters (09) keep their choruses "vast and oppressive, never
  triumphant" — the singalong must stay sinister, not festive.

## Generation

`--style-influence 95 --weirdness 15` for all tracks. Always exclude:
`pop, soft rock, acoustic guitar, nylon-string guitar, folk, Irish folk,
celtic, folk metal, fiddle, tin whistle, bagpipes, accordion, flute, EDM,
opera` — the extended list guards against the folk/celtic drift this genre
vocabulary invites.

Style prompts and lyrics must never reference band or artist names.

## Status

Tracks 02, 05, 06, 09 are complete (styles + lyric variants). The remaining
tracks are adapted with the same doctrine: define the track's one message,
pick the lead perspective, build the hook, compress the canon beats around it.
