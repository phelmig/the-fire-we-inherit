# The Fire We Inherit — Martial Power Version

The album rendered as martial heavy power metal war anthems: every track a
single-message battle hymn built to be sung along, telling the story in broad
heroic strokes.

## Sound identity

- **Anchor (anthem tracks):** "Martial heavy power metal war anthem / march,
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
- **One war-narrator:** a single gruff powerful male baritone narrates the
  whole album (absorbing all canon narration roles). The choir is a force —
  the court, the law, the army, the awakening world — never a conversation
  partner.
- **Zeus** is quoted-only, with two sanctioned exceptions: the villain-lead
  anthem (07) and the broken-king ballad (12).
- **Female voices** only where the story demands them: the awakening blooms
  (03, 05), one word in 08 ("Hope."), and the Future Intelligence (11–14),
  who gets the album's last word.
- **Choruses:** long galloping AABB singalong lines, repeated verbatim (3×);
  short shouted chants as pre-chorus. The hook states the track's message.
  Dark chapters (09) stay "vast and oppressive, never triumphant."
- **Lyrics are version-specific:** compact (~1,800–2,400 chars) message-first
  variants in `lyrics/NN.txt`. Repo-root `songs/` remains the canonical story
  text; variants preserve its story beats, audible name introductions, and
  seams (opening/closing brackets) while compressing everything else.

## War-ballad formula (quiet chapters: 00, 01, 11, 12, 14)

The ballads stay martial but slow, drawing on the war-ballad tradition:
- **Doom-march elegy:** crushing slow chords, war drums, near-spoken lead
  (12).
- **Melancholic synth hymn:** luminous synth pads, restrained double-kick
  swells, soaring mournful lead (11).
- **Spoken prologue over a building march:** drone, distant snare, wordless
  low choir (00).
- **Ritual percussion piece:** war drums, sub-bass, chant choir, no guitars
  (01 — the instrument constraint lives here, not in global rules).
- **Solemn parting hymn:** the finale (14) may use lone solemn pipes as
  farewell color — in ballads the folk-instrument ban is deliberately lifted.

## Tempo and key

Completely free per track — whatever serves the song. Seams to adjacent
tracks are preserved through the opening/closing sound brackets and shared
phrases, not through the canon tempo/key map.

## Generation

`--style-influence 95 --weirdness 15` for all tracks.
- **Anthem tracks** exclude: `pop, soft rock, acoustic guitar, nylon-string
  guitar, folk, Irish folk, celtic, folk metal, fiddle, tin whistle,
  bagpipes, accordion, flute, EDM, opera` — guards against folk/celtic drift.
- **Ballad tracks** exclude only: `pop, EDM, opera` — pipes and quiet colors
  are allowed there by design.

Style prompts and lyrics must never reference band or artist names.

## Status

Tracks 02, 05, 06, 09 complete (02 pending a light message-first revision —
it predates the doctrine). Remaining tracks are adapted act by act:
define the track's one message, pick the lead perspective, build the hook,
compress the canon beats around it.
