# Voice and Tone

Defines the core principles for copywriting voice: clear over clever, plain language over jargon,
active voice, direct address, and tone that scales with stakes rather than mood.

## Core principles

- **Clear over clever.** A pun or a clever turn of phrase that makes someone pause to decode
  it has failed at the actual job of UI copy, which is to be understood instantly. Save
  personality for places where a moment of delight doesn't cost comprehension speed (an empty
  state, a success confirmation), never in a spot where the user needs to act quickly (an
  error, a form label, a destructive-action warning).
- **Plain language over jargon.** Write for someone encountering the concept for the first
  time, not for someone who already knows the internal name for a feature. If an internal or
  technical term must appear, define it in context rather than assuming familiarity.
- **Active voice, direct address.** "You can't undo this" reads faster and feels more honest
  than "This action cannot be undone." Speak to the user as "you", not in the passive third
  person, unless the project's own style guide specifically calls for a different register.
  See `project-source-of-truth.md`.
- **Say what happens, not what the system does internally.** "Your changes are saved" not
  "The save operation completed successfully." The user cares about the outcome, not the
  mechanism.
- **Be specific, not generic.** "3 files couldn't be uploaded" tells the user something
  actionable, "Something went wrong" doesn't. Specificity is almost always worth the extra
  words, within reason, see `error-messages.md` for how far to take this.

## Tone shifts with stakes, not with mood

Tone isn't a fixed personality applied uniformly everywhere, it should track how much is at
stake for the user in that moment:

- **Low stakes** (a success toast, an empty state before any data exists): warmth and light
  personality are fine, this is where a product's voice gets to show character.
- **Medium stakes** (a form validation message, a tooltip): neutral and helpful, get out of
  the way, don't editorialize.
- **High stakes** (an error that blocks progress, a destructive-action confirmation, a
  security warning): serious, precise, zero cleverness. A joke or a casual aside next to "This
  will permanently delete your account" undermines trust at exactly the moment trust matters
  most.

Never let a consistent brand voice override this scaling. A brand that's playful everywhere
else should still go straight and serious the moment stakes go up.

## Sentence case, not Title Case, by default

Unless a project's style guide specifies otherwise, use sentence case for UI text: buttons,
headings, labels, and menu items capitalize only the first word and proper nouns ("Save
changes", not "Save Changes"). This is the prevailing modern convention across most design
systems, but check `project-source-of-truth.md` first since some codebases still use Title
Case by established convention and consistency with existing copy matters more than which
convention is objectively more modern.

## Consistency with existing copy in the same product

Before writing new copy, check how similar situations are already phrased elsewhere in the
same product (search the codebase for similar strings). New copy that's individually well
written but inconsistent with the existing voice reads as jarring and unprofessional, worse
than copy that's slightly less polished but consistent.

## Anti-AI-sounding patterns

Copy that reads as artificially generated has recognizable tells. Avoid them even when the
result looks polished, because the goal is a specialist's voice, not a confident robot:

- **Empty corporate filler**: words that add weight without adding meaning: "delve into",
  "leverage", "utilize", "foster", "robust", "seamless", "cutting-edge", "revolutionary",
  "empower", "game-changer", "optimize". Use the plain word instead ("use" for "utilize",
  "improve" for "optimize"), or cut the filler entirely.
- **Essay openers and signposting**: "It's important to note that", "As we can see",
  "In today's fast-paced world", "Furthermore", "Moreover". Real product copy states the
  point directly; it does not announce the point first.
- **Unnecessary hedging**: "It's worth mentioning", "Needless to say", "One could argue".
  If the point matters, state it. If it doesn't, cut it.
- **Over-explanation**: restating what the reader already knows, or explaining the obvious
  inside the same sentence. If the added words don't change what the reader understands,
  remove them.
- **Uniform voice everywhere**: identical sentence structures and word choices on every
  surface. A real specialist varies sentence length and register by context, exactly as the
  stakes-and-tone rules above describe.

| Weak (AI-sounding) | Better | Why |
|---|---|---|
| "Utilize our robust search to seamlessly optimize your workflow" | "Search filters narrow results as you type" | Plain verb with no filler, states the actual outcome |
| "It's important to note that this action cannot be undone" | "This cannot be undone" | No hedged announcement of the warning the reader needs |
| "In today's fast-paced world, we leverage data to empower teams" | "Reports update every 5 minutes" | Concrete fact replaces the filler prologue |

## Adapt to the domain and audience

"Professional expert in the field" means matching the terms and register the field's own
practitioners use, not sounding generically corporate:

- **Learn the field's vocabulary first.** A medical product's term set for a radiologist
  differs from what a patient expects. Read the project's README, docs, glossary, and
  existing strings to learn its house terms before writing.
- **Match the audience's level, don't posture.** Address readers at their level. Do not
  dumb copy down or jargon it up for show. The goal is the vocabulary the audience already
  uses, used correctly.
- **Use precise terms, then define on first use when audiences span levels.** "Antidiuretic
  hormone" for a clinician, "reduces how much water your kidneys hold" for a patient, and
  "ADH (antidiuretic hormone)" for a mixed audience.
- **Confidence without overclaiming.** Field experts are precise about limits. Never commit
  the product to guarantees it does not actually make, see `project-source-of-truth.md`.
- **Let the project anchor the register.** If the project's existing strings are casual,
  write casual; if formal, write formal. The project's voice guide wins over these defaults.
