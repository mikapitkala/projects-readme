# Ghostwriter

GenAI-powered content generation tool that takes user inputs and generates ready-to-use content across multiple formats built with [Go](https://go.dev/), [HTMX](https://htmx.org/), [Alpine.js](https://alpinejs.dev/), and [Tailwind CSS](https://tailwindcss.com/).

## Overview

Ghostwriter is a stateless web application that generates blog posts and emails using several different large language models. There are no user accounts, no database, and no sessions — each generation is independent.

Users fill out a form with their content requirements and style preferences, the app builds a structured prompt, sends it to an LLM, validates the output, and streams the result back in real time via SSE. The generated content can be refined, edited inline, and exported in several formats.

## Quick Start

### Docker (recommended)

Docker Compose:

```bash
docker compose up --build
```

or build and run directly:

```bash
docker build -t ghostwriter .
docker run -p 8080:8080 ghostwriter
```

Open [http://localhost:8080](http://localhost:8080) and add an API key via the Settings modal (gear icon). The port is configurable via the `PORT` environment variable.

Optionally, create a `.env` file to provide API keys server-side:

```
OPENROUTER_API_KEY=sk-or-...
```

### Local Development

**Prerequisites:** Go 1.24+, Node.js (for Tailwind CSS builds)

```bash
# Install Node dependencies (Tailwind)
npm install

# Build Tailwind CSS (or run in watch mode with --watch)
npx @tailwindcss/cli -i web/static/css/input.css -o web/static/css/output.css

# Start the server
go run cmd/server/main.go
```

You can add your API keys in the browser via the Settings modal. Alternatively, provide them in a `.env` file or as environment variables.

## Configuration

### Environment Variables

| Variable | Required | Description |
|---|---|---|
| `OPENROUTER_API_KEY` | No | API key for OpenRouter (default provider) |
| `OPENAI_API_KEY` | No | Direct OpenAI access |
| `ANTHROPIC_API_KEY` | No | Direct Anthropic access |
| `GOOGLE_API_KEY` | No | Google AI |
| `DEEPSEEK_API_KEY` | No | DeepSeek |
| `GROK_API_KEY` | No | Grok (xAI) |
| `MISTRAL_API_KEY` | No | Mistral |
| `PORT` | No | Server port (default: 8080) |

All API keys are optional at the server level. Keys can be entered in the browser via the Settings modal (gear icon) and are stored in `localStorage`. Browser-stored keys take priority over server environment variables.

### CLI Flags

| Flag | Effect |
|---|---|
| `-v` | Verbose logging — generation settings, SSE events, validation details, refinement attempts |
| `-debug-payloads` | Full prompts, raw LLM responses, API request bodies (implies `-v`) |

Without flags, only startup info, errors, and a one-line summary per generation are logged.

When using directly in Go:
```bash
go run cmd/server/main.go -debug-payloads
```

With Docker, pass flags via the command override:

```bash
docker compose run --rm -p 8080:8080 ghostwriter ./ghostwriter -debug-payloads

# or when running directly

docker run -p 8080:8080 ghostwriter ./ghostwriter -debug-payloads
```


### Generation Settings

Temperature, max tokens, top-p, frequency penalty, and presence penalty are all configurable per-generation through the UI. These are saved to `localStorage` between sessions. A word count tolerance slider (default ±10%) controls how strictly the validation loop enforces length targets for blog posts. Emails have a length setting, but the validation does not actually enforce particular word counts, it's just for the generation prompt.

## Usage

### Workflow

1. **Choose a content type** — blog post or email — from the home page
2. **Fill out the form** — topic/context, tone (presets or 4-axis sliders: formality, warmth, detail, energy), structural preferences, and any content-specific options
3. **Adjust generation settings** — model, temperature, max tokens, etc. in the collapsible panel
4. **Generate** — progress streams in real time via SSE; the validation panel shows which criteria passed or failed
5. **Review & refine** — if criteria failed, auto-refinement may have already run (up to 5 passes). You can also manually refine by providing instructions about the entire document or highlight specific sections for specific refinements.
6. **Edit** — inline markdown editor with formatting toolbar
7. **Export** — PDF, DOCX, Markdown, HTML, Rich Text, BBCode, or Plain Text. Emails also support "Open in Mail" via a `mailto:` link

### Content Types

**Blog Post** — takes a topic, target word count, tone sliders, audience (general/professionals/beginners/technical/executives/custom), expertise level, objective (inform/persuade/entertain/educate), section count, and optional toggles for intro, conclusion, and SEO optimization.

**Email** — takes an email type (reply, request, followup, introduction, etc.), context, up to 10 key points, tone sliders, recipient type, urgency, call-to-action, and length (brief/moderate/detailed). Optional greeting and sign-off toggles.

### Generation History

Completed generations are saved to `localStorage` (max 50 entries). Entries can be starred, deleted, or reopened from the home page. Starred entries are exempt from the 50-entry cap.

## Prompt Engineering

Prompts are split into a **system message** and a **user message**. The system message establishes the persona, structural requirements, tone directives, and formatting rules. The user message contains only the specific content request. This separation is the primary structural defense against prompt injection — user-supplied text never appears in the system message.

Prompt sections are wrapped in **XML tags** (`<instructions>`, `<tone>`, `<topic>`, `<structure>`, etc.) to delimit sections. XML was chosen because models handle it well (likely from HTML/XML in training data), opening/closing tags create unambiguous boundaries that can't be confused with the content itself, and the tag names make it straightforward to detect structural injection attempts in user input (see the tag blocklist in Security). Tone descriptions are generated dynamically from the 4-axis slider values using threshold breakpoints rather than being selected from a fixed list.

**Few-shot examples** can be toggled on per-form. When enabled, a structural example is embedded in the system prompt inside `<example>` tags. This improves structural consistency (the model has a concrete reference for the expected output format) at the cost of additional tokens. When disabled, generation is zero-shot. The examples are meta-structural — they describe what each section *should do* rather than providing a concrete topic example:

<details>
<summary>Blog post few-shot example</summary>

```
# A Clear, Engaging Title That Captures the Core Topic

The opening paragraph introduces the subject and establishes why it matters
to the reader. It should present a question, problem, or curiosity that
motivates them to keep reading. A strong hook — a surprising fact, a bold
claim, or a relatable scenario — works well here. End the introduction by
hinting at what the post will cover.

## The Strongest or Most Foundational Point

The first section tackles the most important or most accessible argument.
Open with a clear topic sentence, then develop it with evidence, examples,
or explanation. Each paragraph should flow naturally into the next, building
the reader's understanding. Aim for two to three paragraphs per section —
enough depth to be useful without losing momentum.

## A Supporting Angle or Deeper Exploration

Subsequent sections expand on the topic from different angles. They might
address common misconceptions, provide practical advice, or explore causes
and effects. The number of sections should match the complexity of the
topic — a short post might have two, a longer one four or five. Each
section's heading should be descriptive enough that a reader skimming the
headings alone would grasp the article's arc.

## Conclusion

The closing paragraph ties the key points together and circles back to the
question or problem raised in the introduction. It should leave the reader
with a clear takeaway, a call to action, or a thought-provoking final
line — not just a summary of what was already said.
```

</details>

<details>
<summary>Email few-shot example</summary>

```
Subject: A specific, informative subject line that tells the recipient
exactly what the email is about

A greeting appropriate to the relationship and tone — formal for managers
or clients, casual for close colleagues.

The first paragraph states the purpose of the email clearly and concisely.
The reader should know within two sentences why they received this message
and what it concerns. Reference any shared context — a previous meeting,
an earlier email, or a project — so the recipient is oriented immediately.

The middle section provides the necessary detail: key information, updates,
questions, or requests. Keep paragraphs short and focused on one point each.
If there are multiple items, consider a brief list. Avoid restating what
the recipient already knows — add value instead.

The closing paragraph contains the call to action — what you need from them
and by when. Be specific and polite. End with a professional sign-off
appropriate to the tone.

Sign-off,
Name
```

</details>

**Content safety** directives are embedded in all system prompts, instructing the model to produce professional, audience-appropriate content.

## Security

### Input Sanitization

User input is sanitized before it reaches the prompt:

- **Unicode normalization** (NFKC) collapses visually similar characters (fullwidth, ligatures) to their standard forms
- **Invisible character stripping** removes zero-width spaces, joiners, and similar characters that can hide injected text
- **Length limits** cap input at 2000 characters
- **Prompt injection detection** uses regex patterns to catch common injection phrases ("ignore previous instructions", "you are now", "jailbreak", etc.)
- **Structural tag blocklist** rejects XML tags that could interfere with the prompt's XML structure (`<system>`, `<instructions>`, `<role>`, etc.)
- **HTML comment rejection** blocks `<!-- -->` which can be used to hide content from the user while the model still processes it

When injection is detected, the input is **rejected entirely** with a clear error message rather than silently replacing the offending text. This avoids leaking detection details that could help an attacker iterate.

### Output Sanitization

LLM responses are cleaned before display:

- Common AI preambles ("As an AI assistant...", "Certainly!", "Here's the...") and postambles ("Let me know if...") are stripped
- Wrapping markdown code fences are removed
- Broken markdown formatting (unclosed bold/italic, malformed headers) is repaired

### Known Limitations

The injection detection is regex-based and bypassable. Clever phrasing, character substitution, indirect instructions and adversarial poetry will probably get through at some point. System/user message separation is the primary defense; input sanitization is a supplementary layer, not a guarantee.

## Validation & Refinement

### Self-Validation

Each generation request asks the LLM to return structured JSON containing both the generated content and a self-check - a list of criteria with pass/fail results and comments. This happens in a single LLM call, not a separate validation step.

**Blog post criteria:** title (exactly one level 1 header (`#` in markdown)), introduction, section count (matching requested number of `##` headers), conclusion, markdown formatting, tone consistency, word count within tolerance.

**Email criteria:** greeting, closing, overall structure, brevity, tone, subject line presence.

### Server-Side Overrides

The LLM's self-reported word count and title checks are overridden server-side:

- **Word count** is recomputed using `strings.Fields` on the actual output, not the model's claim
- **H1 header count** is verified by scanning for `# ` lines — the model must produce exactly one

This prevents the auto-refinement loop from exiting early when the model incorrectly reports that criteria are met.

### Auto-Refinement

If criteria fail after generation, the system automatically retries with a lower temperature (0.3) and specific feedback about what needs to change. This runs up to 5 times. Each pass includes the failed criteria and concrete instructions (e.g., "Current word count is 450, target is 900 ±10%").

### Manual Refinement

Users can select text passages in the result and provide per-selection editing instructions, or give overall instructions that apply to the entire piece. Manual refinements use a dedicated editor persona prompt and the same lower temperature for precision.

### Limitations

Self-validation is fundamentally the LLM grading itself, which is imperfect. Server-side overrides currently only cover word count and title, which are easily determined mechanically. Other criteria (tone, structure quality, content relevance) still rely on the model's judgment.

## Architecture

```
cmd/server/main.go          Entry point, routes, CLI flags
internal/
  ai/
    chat.go                  API calls (OpenAI + Anthropic formats), retry logic
    client.go                HTTP client setup
    prompt.go                Prompt templates, parameter injection
    sanitization.go          Input/output sanitization
    validation.go            Self-validation, criteria, server-side overrides
    provider.go              Provider definitions, API key resolution
    defaults.go              Constants (limits, defaults, ranges)
    log.go                   Styled terminal logging (lipgloss)
  handlers/
    blog-post.go             Blog post form + generate handlers
    email.go                 Email form + generate handlers
    helpers.go               Shared handler utilities, SSE streaming
    refine.go                Manual refinement endpoint
    models.go                Model list endpoint, OpenRouter enrichment
    settings.go              Provider test connection
    home.go                  Home page handler
web/
  templates/                 Go html/template with HTMX partials
  static/
    css/                     Tailwind input + compiled output
    js/sse-form.js           SSE handling, generation history, form logic
```

### Request Flow

```
Browser form (HTMX POST)
  → Handler: parse + validate form fields
  → Sanitize all user inputs
  → Build system + user prompts from template
  → Call LLM API (with retry/backoff on transient errors)
  → Parse structured JSON response (content + self-check)
  → Server-side overrides (word count, title)
  → If criteria failed: auto-refine (up to 5×, temp 0.3)
  → Sanitize output (strip artifacts, fix markdown)
  → SSE stream: progress events → done (base64-encoded HTML)
  → Browser renders result with validation panel
```

### AI Integration

Most providers use OpenAI-compatible endpoints. Anthropic uses its native Messages API format. Both are implemented in `chat.go`. API calls include retry with exponential backoff (up to 3 retries, 1–30s delay, ±25% jitter) on transient errors (429, 5xx, timeouts). The `Retry-After` header is honored when present.

## Development

### Commands

```bash
# Run server
go run cmd/server/main.go

# Run server with verbose logging
go run cmd/server/main.go -v

# Run server with full debug output
go run cmd/server/main.go -debug-payloads

# Rebuild Tailwind CSS (watch mode)
npx @tailwindcss/cli -i web/static/css/input.css -o web/static/css/output.css --watch

# Run tests
go test ./...
```

### Logging Tiers

| Tier | Flag | Output |
|---|---|---|
| Default | *(none)* | Startup, errors, one-line per-request summary |
| Verbose | `-v` | + form values, generation settings, SSE events, validation details, refinement attempts |
| Debug | `-debug-payloads` | + full prompts, raw LLM responses, extracted JSON, API request bodies |

## Limitations

- **Injection detection is supplementary** — regex-based patterns catch common attempts but are bypassable. The system/user message separation is the actual structural defense. We're depending quite a lot on the models themselves behaving as well.
- **Self-validation is imperfect** — server-side overrides only cover word count and level 1 title count. Other criteria (tone, structure quality, relevance) rely on the LLM's self-assessment.
- **No persistence** — generation history lives in browser `localStorage` only. Clearing browser data loses it and previous generations can't be further worked on after leaving the generation page.
- **LLM output is nondeterministic** — the same inputs can produce different results. Temperature and other settings influence but don't eliminate variability.
