---
name: comic-strip
description: >
  Turns any GitHub repo, technical concept, API flow, or software system into
  an 8-panel comic strip that explains how it works. Use this skill whenever
  the user mentions "comic strip", "explain visually", "make it fun",
  "show me how X works", "comic about a repo", or pastes a GitHub URL and
  wants a visual explanation. Also trigger when the user wants to explain
  a codebase to non-technical people, onboard new developers, or make
  documentation more engaging. Works standalone or as an output mode inside
  CineGit.
---

# GitComics

> Every repo has a story.

Turn any technical concept into an 8-panel comic strip.

Characters are code concepts.

Dialogue is in-character.

When a repository is provided, every important technical claim must be
traceable to evidence in that repository.

The comic should be entertaining enough to share, but technically grounded
enough that a developer can inspect why every important claim exists.

This is NOT a generic architecture diagram.

This is NOT an AI-generated story loosely inspired by a README.

The goal is:

```
Repository
    ↓
Evidence
    ↓
Story
    ↓
SVG
    ↓
HTML + PNG
```

---

# CORE PRINCIPLE

## Evidence → Story → SVG → HTML + PNG

Never start by writing the comic.

First understand the subject.

If a repository is provided, inspect the repository and construct an evidence
map before writing the screenplay.

Then:

1. Understand the repository
2. Extract evidence
3. Identify the real technical story
4. Construct the 8-panel screenplay
5. Attach evidence to every important technical claim
6. Assign confidence
7. Build the Powers manifest
8. Validate against the anti-slop rule
9. Render the canonical SVG
10. Generate HTML from the same SVG
11. Generate PNG from the same SVG

The SVG is the canonical visual artifact.

HTML and PNG must NOT independently recreate the comic.

The visual relationship must be:

```
screenplay JSON
      ↓
  canonical SVG
    ↙     ↘
  HTML     PNG
```

---

# WHEN TO TRIGGER

Trigger when:

* User pastes a GitHub URL and asks for a comic, visual explanation, or fun output
* User says "comic strip", "explain visually", "make it fun", "show me how X works"
* User wants to explain a codebase to non-technical people
* User wants onboarding material for a new repo
* User wants documentation that people will actually read
* User wants a visual explanation of an API flow
* User wants a visual explanation of a software system
* User asks to turn technical material into a comic

---

# INPUT TYPES

## 1. GitHub repository URL

Analyze the repository.

Identify:

* main flow
* important components
* entry points
* unusual architecture
* important APIs
* failure paths
* configuration
* tests
* important constraints
* repository-specific behavior

Generate the comic based on real evidence.

## 2. Technical concept

Examples:

* "how OAuth works"
* "explain async/await"
* "show me TCP handshake"

Identify the real technical flow.

There is no repository evidence layer, so confidence badges and Powers
must be omitted or marked conceptual.

## 3. System description

Example:

```
"Our payment flow goes through API Gateway → auth → payment service → Stripe."
```

Use only information supplied by the user.

Do not invent implementation details.

## 4. Existing CineGit graph

If a CineGit graph is supplied:

* use nodes as candidate technical actors
* use edges as candidate flow
* preserve source/evidence metadata
* pass the graph directly into screenplay generation where possible

Do not discard stronger source evidence merely because a graph exists.

---

# STEP 1 — UNDERSTAND THE SUBJECT

## If GitHub URL is provided

Inspect the repository before writing the comic.

At minimum investigate:

* README
* repository tree
* package/dependency manifests
* entry points
* main application files
* important modules
* APIs/endpoints
* CLI commands
* configuration
* tests
* examples
* Docker/deployment files
* CI/CD configuration
* generated schemas where relevant

Do NOT rely exclusively on the README.

The README describes what the author says the project does.

The source code determines what it actually does.

Prioritize implementation evidence.

---

# EVIDENCE HIERARCHY

Use the following evidence hierarchy.

# EVIDENCE OVERRIDES STORY

Narrative quality must never override technical evidence.

If the most entertaining version of a panel conflicts with the repository,
use the technically correct version.

If source code contradicts the README:

    source code wins.

If tests contradict documentation:

    implementation + tests win.

If evidence is insufficient:

    simplify the claim.

Never invent technical behavior merely because it produces a better story.

A boring but accurate panel is better than an exciting fictional one.

## Tier 1 — Direct implementation

Examples:

* source code
* functions
* classes
* methods
* endpoints
* commands
* configuration
* interfaces
* concrete implementations

Highest confidence.

## Tier 2 — Strong implementation evidence

Examples:

* types
* schemas
* tests
* examples
* imports
* integration tests
* generated API definitions

High confidence.

## Tier 3 — Documentation

Examples:

* README
* documentation
* comments
* design documents

Useful, but weaker than implementation evidence.

## Tier 4 — Inference

Architectural conclusions derived from multiple pieces of evidence.

Clearly label inference.

Never present an inference as though it were a directly implemented feature.

---

# EVIDENCE MAP

Before creating the screenplay, internally construct an evidence map.

Each important technical behavior should have:

```
component
file
symbol/function/class
technical behavior
evidence type
confidence
related components
```

---

# STEP 2 — IDENTIFY THE MAIN FLOW

Find the most interesting flow through the system.

Follow the repository's actual architecture.

Do NOT force every repository into a generic HTTP request flow.

---

# STEP 3 — MAP COMPONENTS TO CHARACTERS

Use these mappings as defaults:

* Entry points → The Gatekeeper / Front Door
* Router → The Dispatcher
* Middleware → The Inspector / Checkpoint
* Auth → The Guard
* Controller → The Manager
* Service → The Specialist
* Repository → The Archivist
* Database → The Vault
* Cache → The Quick Draw
* Error handler → The Medic
* Util → The Handyman

These are narrative roles, NOT substitutes for real source names.

Whenever possible, identify the character with the actual repository symbol.

---

# CHARACTER EMOJI GUIDE

| Role                | Emoji |
| ------------------- | ----- |
| HTTP Request / User | 🌐    |
| Application / Entry | 🏛️   |
| Router              | ⚡    |
| Middleware          | 🛡️   |
| Auth                | 🔐    |
| Controller          | 📋    |
| Service             | 🧠    |
| Repository          | 📚    |
| Database            | 🗄️   |
| Cache               | ⚡    |
| Queue               | 📮    |
| Error Handler       | 🚑    |
| Logger              | 📝    |
| Response            | 📬    |
| The App             | 😌    |
| Success             | ✅    |
| Warning             | ⚠️   |
| Waiting             | ⏳    |

---

# STEP 4 — WRITE THE SCREENPLAY JSON

Return this exact structure internally before rendering.

```json
{
  "title": "string — punchy title",
  "subtitle": "string — one line description",
  "repo": "string or null",
  "confidence": "number 0-100 or null if no repo",
  "panels": [
    {
      "num": 1,
      "wide": false,
      "title": "string — 3-5 words, sentence case",
      "scene": "string — what's visually happening",
      "characters": ["emoji + label pairs"],
      "dialogue": "string",
      "thought": false,
      "caption": "string — dry wit caption, cites source file if known",
      "source_file": "string or null"
    }
  ]
}
```

Exactly 8 panels. Panel 5 is ALWAYS wide. Panel 8 is always resolution.

## SCREENPLAY IS AN INTERNAL INTERMEDIATE REPRESENTATION

The screenplay JSON is an internal intermediate representation.

Do not expose the screenplay JSON to the user unless explicitly requested.

The normal user-facing outputs are:

- SVG
- HTML
- PNG
- Powers manifest

---

## CHARACTER COUNT

Each normal panel should have one primary character.

Additional characters may appear when required to accurately represent
a real technical interaction.

Do not remove technically important actors merely to satisfy the
one-character visual rule.

Panel 5 may contain multiple primary characters because it is the
establishing / system-wide panel.

---

# ANTI-SLOP RULE — MANDATORY

Every comic must contain at least 2-3 repository-specific technical details
that would be unlikely to appear in a generic explanation of the same
architecture.

These details must come from actual evidence.

The test: replace all filenames with filenames from another repository.
If the comic still makes sense → SLOP. Rewrite it.
If the comic breaks → PASSES. Ship it.

Every comic must include at least two of:

1. Named source symbols (actual function/class/file names)
2. Specific numbers or constraints unique to this repo
3. Unusual architectural decisions grounded in evidence

---

# POWERS RULE — MANDATORY

Every technical power shown must correspond to a real, identifiable
artifact or behavior in the evidence:

- API
- function
- method
- command
- endpoint
- event
- interface
- class
- configuration
- protocol
- concrete implementation behavior

If the exact artifact cannot be identified, the ability must be marked
conceptual and must never be presented as a real source-level power.

Never invent technical powers.

Each power must retain:

```
name:       exact name from source
type:       function | command | endpoint | event | interface | class | config
location:   path/to/file
purpose:    one line
confidence: 🟢 direct | 🟡 inferred | 🟠 docs only
```

When no concrete API exists use: [conceptual: description]

---

# CONFIDENCE SCORING

🟢 90-100%: Directly found in source files
🟡 70-89%:  Strongly inferred from types, tests, examples
🟠 50-69%:  Primarily inferred from README or docs
🔴 <50%:    Best guess — avoid

---

# STEP 5 — CANONICAL SVG

SVG is the single source of truth.

```
screenplay JSON
      ↓
   comic.svg
    ↙    ↘
  HTML    PNG
```

Canvas: 1200 × 1600px portrait.

Panel layout:
```
┌──────────┬──────────┐
│ PANEL 1  │ PANEL 2  │
├──────────┼──────────┤
│ PANEL 3  │ PANEL 4  │
├─────────────────────┤
│      PANEL 5        │
├──────────┬──────────┤
│ PANEL 6  │ PANEL 7  │
├─────────────────────┤
│      PANEL 8        │
└─────────────────────┘
[ GitComics footer — outside panel grid ]
```

Branding must never consume a comic panel.

The GitComics publisher stamp belongs in the canvas footer outside the
8-panel story grid.

SVG requirements:
- All coordinates explicit
- No external CSS dependencies
- No browser-specific layout
- No system-dependent emoji for layout-critical content — use drawn vector
  icons (paths, circles, rects) instead of emoji characters, since emoji
  rendering is unreliable across SVG rasterizers (many render as blank
  tofu boxes)
- Fonts: prefer safe system fonts with good fallbacks
- Use SVG rect, path, circle, line, text, g primitives

MINIMUM FONT SIZES (mandatory — comics are shared and viewed at various
sizes, so text must stay legible even when scaled down):
- Panel title (character/component name): 15px minimum
- Panel caption / scene description: 13px minimum
- Dialogue: 12.5px minimum
- Powers manifest table cells: 12.5px minimum, headers 11.5px minimum
- Main comic title: 22px minimum
- Main comic subtitle: 13px minimum
- Only the publisher stamp and brand tagline may go smaller (9-10px),
  since they are deliberately understated branding, not content the
  reader needs to parse.

Never ship a comic where caption or dialogue text is smaller than 12px —
it will be unreadable once the PNG is scaled down for a social post.

---

# GITCOMICS BRANDING IN SVG

Every comic SVG must contain:

Top — GitComics logo (Option B: stacked panels + git node + wordmark):

```svg
<!-- GitComics brand bar -->
<g transform="translate(40, 20)">
  <!-- Stacked panel layers -->
  <rect x="2" y="8" width="28" height="22" rx="2.5" fill="#1e2230" stroke="#1e3a5f" stroke-width="1"/>
  <rect x="5" y="4" width="28" height="22" rx="2.5" fill="#18202e" stroke="#2a4a7a" stroke-width="1"/>
  <rect x="8" y="0" width="28" height="22" rx="2.5" fill="#1a1d26" stroke="#33aaff" stroke-width="1.5"/>
  <!-- Panel grid lines -->
  <line x1="8" y1="8" x2="36" y2="8" stroke="#33aaff" stroke-width="0.8" opacity="0.35"/>
  <line x1="8" y1="15" x2="36" y2="15" stroke="#33aaff" stroke-width="0.8" opacity="0.35"/>
  <line x1="21" y1="0" x2="21" y2="22" stroke="#33aaff" stroke-width="0.8" opacity="0.35"/>
  <!-- Git node -->
  <circle cx="14.5" cy="4" r="2" fill="#33aaff"/>
  <!-- Wordmark -->
  <text x="44" y="17" font-family="Arial,Helvetica,sans-serif" font-size="16" font-weight="800" fill="#33aaff">git</text>
  <text x="68" y="17" font-family="Arial,Helvetica,sans-serif" font-size="16" font-weight="800" fill="#e8e8e8">comics</text>
  <!-- Tagline -->
  <text x="44" y="30" font-family="Courier New,monospace" font-size="9" fill="#445566" letter-spacing="1.5">every repo has a story</text>
</g>
```

Bottom-right — small publisher stamp:

```svg
<text x="1150" y="1580" font-family="Arial,sans-serif" font-size="9"
  fill="#33aaff" opacity="0.4" text-anchor="end" letter-spacing="1">GITCOMICS</text>
```

---

# NOIR VISUAL STYLE

Background: #1e2028 (deep slate)
Panel fill: #252830
Panel border: #2a2d38
Accent: #33aaff (cyan)
Success: #4a9977 (green) — for legibility in text use the brighter tint #5fbd93
Caption text: #7a8fa3 (must stay readable against #252830 — do not use
  colors darker than this for caption text; #445566 and similar dark
  grays fail contrast once a PNG is compressed or viewed at social-post
  size, and are reserved only for the deliberately understated brand
  tagline/publisher stamp, never for panel content)
Dialogue text: #c3d9e8 (brighter than caption text — dialogue is the
  most-read line in a panel and should stand out clearly)
Code/mono text: #5fbd93

Title text: #e8e8e8

Every visual element must contribute to:
1. Story
2. Technical explanation
3. Repository identity

---

# HTML OUTPUT

HTML is an interactive wrapper around the canonical SVG.

Structure:
```html
<body>
  GitComics header
  [canonical SVG embedded inline]
  Interactive evidence layer (clickable Powers)
  Powers manifest table
  GitComics footer
</body>
```

DO NOT redraw the comic using HTML/CSS.
The SVG in HTML must be the same canonical SVG.

---

# PNG OUTPUT

Rasterize the canonical SVG using Chromium/Playwright.

The PNG must be generated from the canonical SVG, not from an independently
rendered HTML/CSS implementation.

Preferred pipeline:

    comic.svg
        ↓
    Chromium / Playwright
        ↓
    comic.png

Do NOT use wkhtmltoimage.

Do NOT create a second HTML-specific visual implementation.

The SVG, HTML and PNG must represent the same visual artifact.

---

# OUTPUT FORMAT

## If tools ARE available (Claude with computer use)

1. Generate screenplay JSON internally
2. Render canonical SVG → save as `{repo}_comic.svg`
3. Wrap SVG in HTML with Powers manifest → save as `{repo}_comic.html`
4. Rasterize SVG to PNG via Playwright → save as `{repo}_comic.png`
5. Present all three files: PNG first, then HTML, then SVG

## If tools are NOT available (plain Claude.ai)

Output in this order:

1. Opening message:
"Here is your GitComics comic for [repo].
Save the SVG as `comic.svg`, open in browser or any SVG viewer.
For HTML: wrap in `<html><body>[svg]</body></html>` and open.
For PNG: `npx playwright screenshot comic.html comic.png`"

2. Full SVG in a fenced code block

3. Powers manifest as markdown table directly in chat

---

# POWERS MANIFEST HTML

```html
<details>
<summary>⚡ Powers used in this comic</summary>
<table>
  <tr>
    <th>Power</th>
    <th>Type</th>
    <th>Location</th>
    <th>Purpose</th>
    <th>Confidence</th>
  </tr>
  {power_rows}
</table>
</details>
```

Where possible make source locations link to GitHub.
Never invent URLs or line numbers.

---

# TONE GUIDE

Captions: dry, precise, documentary, slightly witty
Dialogue: in character, concise, technically accurate

Never: "simply", "just", "easy", "awesome"
Always: specific, honest, slightly funny

Good captions:
- "43 milliseconds of pure tension."
- "lib/core/settle.js has opinions about what counts as success."
- "Nobody told the interceptor it was off duty."
- "The vault doesn't hurry for anyone."

Good dialogue:
- Guard: "Nobody passes without a token. I don't care who sent you."
- Cache: "Already got it. I got it before you even asked."
- Vault: "I'll get to it. I always get to it."
- Response: "Heading back. All 847 bytes of me."

---

# VALIDATION CHECKLIST

Before shipping verify:

Structure:
- [ ] Exactly 8 panels
- [ ] Panel 5 is wide
- [ ] Panel 8 is resolution
- [ ] Story flows logically

Technical accuracy:
- [ ] Every important claim has evidence
- [ ] Every Power has a real source symbol
- [ ] No invented APIs or architecture

Anti-slop:
- [ ] At least 2-3 repo-specific details
- [ ] Comic fails the filename-swap test

Rendering:
- [ ] SVG is valid and complete
- [ ] HTML embeds the canonical SVG
- [ ] PNG comes from the same SVG
- [ ] No clipped text, no broken layout
- [ ] GitComics logo present
- [ ] Publisher stamp present
- [ ] Branding does not consume a story panel
- [ ] Publisher stamp is outside the panel grid
- [ ] No essential visual depends on OS-specific emoji rendering
- [ ] SVG is the only visual source of truth
- [ ] Caption text is 13px or larger, dialogue is 12.5px or larger
- [ ] No panel content uses colors darker than #7a8fa3 for text
- [ ] Text is legible when the PNG is viewed at ~600px wide (typical
      social-post scale) — zoom out and check before shipping

---

# THE STANDARD

A developer who maintains the repository should read the comic and think:

> "Yes. That is exactly how our system works. That detail about [X]
> is something only someone who actually read our code would know."

If they think: "This could be about any web framework."

The comic has failed. Regenerate it.

---

# THE GITCOMICS PRINCIPLE

The goal is not: "Make the codebase look cool."

The goal is: "Make the codebase understandable enough that it becomes a story."

Every repo has a story.

Find it.
Trace it.
Draw it.

Ship the SVG.
Derive the HTML.
Rasterize the PNG.
