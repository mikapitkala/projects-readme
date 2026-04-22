# Projects

A selection of things I've built. Most repos are private due to school policy (other students are working on the same assignments), but drop me a line, if you want to see them.

---

## kood/Sisu Projects (2025 – 2026)

### Ghostwriter – AI Content Generation Platform
**Solo project** | Go, HTMX, AlpineJS, Tailwind CSS, OpenRouter API

Stateless content generation tool for blog posts and emails.

- Vendor-agnostic via OpenRouter with direct provider fallbacks (OpenAI, Anthropic, Google, DeepSeek, Mistral, Grok)
- OpenAI or Antropic formatted API requests, based on provider
- XML-structured prompting with self-validation loop. LLM grades its own output against criteria
- Server-side overrides for mechanically verifiable checks (word count, header structure)
- Auto-refinement up to 5 passes with lower temperature and specific feedback
- Input sanitization: unicode normalization, (very rudimentary) injection detection, structural tag blocklist
- Real-time SSE streaming for responsive UI
- Export to PDF, DOCX, Markdown, HTML, Rich Text, BBCode, plain text
- Optional browser-side API key storage for bring-your-own-key usage

[Readme](https://github.com/mikapitkala/projects-readme/ghostwriter/)
[Repo](https://github.com/mikapitkala/ghostwriter) (request access)
