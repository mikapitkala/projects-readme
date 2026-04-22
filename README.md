# Projects

A selection of things I've built, mostly for school. Most repos are private due to school policy (other students are working on the same assignments), but drop me a line, if you want to see them.

---

## kood/Sisu Projects (2025 – 2026)

### Ghostwriter – AI Content Generation Platform (2026)
**Solo project**

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![HTMX](https://img.shields.io/badge/HTMX-3366CC?style=flat&logo=htmx&logoColor=white)
![Alpine.js](https://img.shields.io/badge/Alpine.js-8BC0D0?style=flat&logo=alpinedotjs&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![OpenRouter](https://img.shields.io/badge/OpenRouter-6366F1?style=flat)

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

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/ghostwriter) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/ghostwriter)

---

### kood/Melee – Multiplayer Space Combat Arena (2025)
**Group project** (with Pavel)

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![CSS](https://img.shields.io/badge/CSS-1572B6?style=flat&logo=css3&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=flat&logo=socketdotio&logoColor=white)

Star Control 2 Supermelee inspired real-time combat for 2-4 players
in the browser. Newtonian(ish) physics, diverse ship loadouts, and
intense multiplayer battles.

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

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/multi-player) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/multi-player)

---

### dot-js – Frontend Framework from Scratch (2025)
**Group project** (with Pavel)

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![CSS](https://img.shields.io/badge/CSS-1572B6?style=flat&logo=css3&logoColor=white)
![No Build](https://img.shields.io/badge/No_Build-Required-brightgreen?style=flat)

A reactive frontend framework built without a virtual DOM. Import via ES modules and run - no build step, no tooling.

- Signals-based reactivity with O(1) fine-grained DOM updates
- Reactive markers update the DOM directly - no diffing, no wasted cycles
- Built-in scheduler for batched updates
- Global event delegation
- Dedicated router
- Ships with a classless CSS framework for styling out of the box
- Interactive 16-step tutorial built using the framework itself
- Performance comparison example against a vanilla JS todo app
- Minimal development server included (built-in Node modules only, no `npm install` required)

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/frontend-framework) [![Docs](https://img.shields.io/badge/Docs-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/frontend-framework/docs) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/frontend-framework)

---

### match-me – Recommendation Platform (2025)
**Group project** (with Pavel)

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white)
![PostGIS](https://img.shields.io/badge/PostGIS-336791?style=flat&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

Full-stack social platform with geospatial matching and recommendation scoring.

- Weighted compatibility scoring based on bio, interests, location
- PostGIS-powered geographical proximity matching
- Real-time chat via WebSockets
- JWT-based authentication with secure session handling
- Watercolor-themed UI with randomized pastel backgrounds and sketch effects on every page
- Swipe interactions with hand-drawn animation effects
- Custom launcher (Go binary) manages the full stack: PostgreSQL + PostGIS via Docker, backend API on :8080, Vite frontend on :5173
- Launcher auto-checks system requirements and provides setup guidance
- Primarily responsible for frontend

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/match-me) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/match-me)

---

### racetrack – Race Management System (2025)
**Group project** (with Pavel)

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=flat&logo=socketdotio&logoColor=white)

Real-time race management system with role-based interfaces and
live synchronization.

- Four management interfaces: front desk (session management), race control (safety/flags), lap tracker (timing), public leaderboard
- Role-based authentication with server-side key validation
- Real-time synchronization across all interfaces via Socket.IO
- Unified dashboard combining all views for race control center
- Mobile-responsive design for tablet and phone access
- State recovery - active races continue after server restart, timing and lap data preserved
- Test data mode with explicit confirmation to prevent accidental data loss
- Configurable race durations (60s for dev, 10min for production)

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/racetrack) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/racetrack)

---

### literary-lions – Book Discussion Forum (2025)
**Group project** (with Pavel)

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Zero JS](https://img.shields.io/badge/Zero-JavaScript-red?style=flat)

Full-stack forum for literary discussions, built with strict constraints: zero JavaScript, zero non-standard Go libraries.

- Pure server-side rendering with Go templates
- Auto-fetches book covers from Open Library API with fallback for misses
- Database migrations with automated schema updates
- Comprehensive seed functions for immediate content on first run
- Like/dislike system for posts and comments
- Category-based organization, search, filtering
- bcrypt password hashing, UUID session management via cookies
- Admin system with auto-generated credentials on first run
- Docker support for containerized deployment

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/literary-lions) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/literary-lions)

---

### stations – Train Network Pathfinding (2025)
**Group project** (with Pavel)

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Scale](https://img.shields.io/badge/Scale-10k_stations-orange?style=flat)

Terminal-based pathfinding for train networks with conflict-free
concurrent train movement.

- BFS shortest path algorithm
- Combinatorial optimization using bitmask iteration for finding maximum non-overlapping routes
- Handles networks up to 10,000 stations and 10,000 trains
- Terminal-based animated visualizer of train movements with colored output
- Conflict rules: one train per station per turn (except start/end), no repeated track usage in a turn
- Compressed output (gzip) for large simulations
- Comprehensive test suite with selective test execution
- Helper scripts for quick iteration during development

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/stations) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/stations)

---

### cars – Car Showcase & Comparison (2025)
**Solo project**

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![CSS](https://img.shields.io/badge/CSS-1572B6?style=flat&logo=css3&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)

Web app for browsing and comparing car models, consuming a separate
Node.js API.

- Recommendation algorithm scoring models, brands, and categories based on user interactions (views, likes, dislikes)
- CSS-only row/column highlighting in comparison view (notoriously difficult to pull off without JavaScript)
- Wikipedia integration for model and manufacturer details (currently blocked by their crawler restrictions, but the integration is there)
- Side-by-side comparison of unlimited models in a horizontal carousel
- Filtering by manufacturer, category, country
- Debug mode with performance metrics, request info, and all recommendation scores visible
- Glassmorphism UI with blurred background effects
- Light/dark mode toggle
- Async logging with configurable verbosity
- Configurable via config file or environment, with hardcoded
  defaults as fallback
- Auto-installs API server dependencies and starts it on launch

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/cars) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/cars)

---

### art – ASCII Art Encoder/Decoder (2025)
**Solo project**

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)

CLI and web tool for encoding and decoding ASCII art shorthand.

- Custom parser with strict and relaxed error modes
- Color control blocks with CSS-like syntax - CLI supports named colors, web version supports any HTML color name or hex value
- Reusable color library used across the entire Go module
- Session persistence via cookies in the web version
- File import/export with auto-detection based on extensions (`.encoded.txt` gets decoded, `.art.txt` gets encoded)
- Multiple input modes: literal strings, files, mixed
- Rainbow mode for when regular colors aren't enough

[![Readme](https://img.shields.io/badge/Readme-0366d6?style=for-the-badge&logo=readthedocs&logoColor=white)](https://github.com/mikapitkala/projects-readme/tree/main/art) [![Actual Repo](https://img.shields.io/badge/Repo_(Request_ACCESS)-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikapitkala/art)

---

## Personal & Work Projects

### vBulletin to Vanilla Forum Migration (2018)
**Solo project**

![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)
![Regex](https://img.shields.io/badge/Regex-69_groups-red?style=flat)

Migrated a 3D sci-fi art community forum (running since 2006) from vBulletin to Vanilla Forums.

- Official migration tools couldn't handle the database state due to years of customization
- Built custom migration using a single regex with ~69 capture groups to rebuild the database schema
- Learned enough PHP during the project to troubleshoot Vanilla customizations. Even wrote a couple of custom addons
- Still running on a LAMP stack I maintain on Digital Ocean
- Currently considering a rewrite in Go, HTMX, AlpineJS, Tailwind and SQLite

### FS_XLIFFer – Format Normalization Tool (2020)
**Work project**

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)
![XLIFF](https://img.shields.io/badge/XLIFF-orange?style=flat)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat&logo=jira&logoColor=white)

Internal tool at F-Secure for standardizing localization source formats. Effectively a superset of Projectinator - includes all its intake functionality plus format conversion.

- Converts various input formats (CSV, XLSX, inline tags) into standardized XLIFF kits
- CAT-tool-agnostic output - any translation tool can consume the results
- Includes Projectinator's project creation and intake functionality so you don't have to hop between tools
- Bootstrap-based UI customized to match the company branding at the time
- 5+ years in production use

### Projectinator – Jira Intake System (2019)
**Solo project**

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat&logo=jira&logoColor=white)

Web-based intake system for localization project tracking.

- Simple web forms that got 100% of tasks into Jira without anyone having to learn Jira
- Streamlined order form for customers
- Internal conversion tools for the team to turn emails, Teams messages, smoke signals, corridor ambushes and other ad-hoc requests into standardized tickets
- Bootstrap-based UI customized to match the company branding at the time
- 100% of projects tracked in Jira
- Functionality later folded into FS_XLIFFer for a more unified experience
