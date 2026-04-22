# Projects

A selection of things I've built, mostly for school. Most repos are private due to school policy (other students are working on the same assignments), but drop me a line, if you want to see them.

---

## kood/Sisu Projects (2025 – 2026)

### Ghostwriter – AI Content Generation Platform (2026)
**Solo project** | Go, HTMX, AlpineJS, Tailwind CSS, OpenRouter API

Stateless content generation tool for blog posts and emails. Fill out a form with content requirements and style preferences, get streamed output that can be refined, edited, and exported.

- Vendor-agnostic via OpenRouter with direct provider fallbacks (OpenAI, Anthropic, Google, DeepSeek, Mistral, Grok)
- OpenAI or Anthropic formatted API requests, based on provider
- XML-structured prompting with self-validation loop. LLM grades its own output against criteria
- Server-side overrides for mechanically verifiable checks (word count, header structure)
- Auto-refinement up to 5 passes with lower temperature and specific feedback
- Temperature, max tokens, top-p, frequency penalty, and presence penalty are all configurable per-generation through the UI
- Input sanitization: unicode normalization, (very rudimentary) injection detection, structural tag blocklist
- Real-time SSE streaming for responsive UI
- Export to PDF, DOCX, Markdown, HTML, Rich Text, BBCode, plain text
- Optional browser-side API key storage for bring-your-own-key usage

[Readme](https://github.com/mikapitkala/projects-readme/tree/main/ghostwriter)

[Actual Repo](https://github.com/mikapitkala/ghostwriter) (request access)

---

### kood/Melee – Multiplayer Space Combat Arena (2025)
**Group project** (with Pavel) | JavaScript, CSS, Node.js, Socket.IO

Star Control 2 Supermelee inspired real-time combat for 2-4 players in the browser. Newtonian(ish) physics, diverse ship loadouts, and intense multiplayer battles.

- Zero canvas, zero images - ships are font glyphs, explosions are CSS gradients and box-shadows, stars are procedural dots
- (Ok, one image - the favicon is a screenshot of the CSS logo)
- Hardware-accelerated DOM rendering via `will-change: transform`
- Newtonian physics with three drag presets: beginner (arcade), medium (balanced), advanced (true Newtonian, no drag; the *correct* option)
- Spatial audio via Web Audio API with 3D positioning based on viewport
- Dynamic music - three intensity layers blend in real-time based on combat state
- Host-authoritative multiplayer with automatic host migration if the host disconnects
- Observer mode when lobby is full (4 players)
- 6 ship hulls with distinct stat profiles (Armor, Reactor, Recharge, Thrust, Agility)
- 4 primary weapons, 6 secondary abilities, 12 pre-built archetype loadouts
- Multiple game modes: Deathmatch, Last Ship Standing, Sudden Death
- Gravity well with inverse-square mechanics for slingshot maneuvers or dragging enemies to their doom
- Screen wrapping - fly off one edge, appear on the opposite. Bounce off Arena borders
- Dynamic camera that zooms and pans to keep all ships in view
- Local multiplayer (up to 4 players on one keyboard) and online multiplayer
- 30Hz state sync with client-side interpolation
- 60 FPS target with fixed 16.67ms physics timestep

[Readme](https://github.com/mikapitkala/projects-readme/tree/main/multi-player)

[Actual Repo](https://github.com/mikapitkala/multi-player) (request access)

---
