# AB Tasty — Evi Content Prompt Agent

**Structured prompts for the Evi Content AI visual editor. Ready to paste. Any industry.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Works with Claude](https://img.shields.io/badge/works%20with-Claude-blue.svg)](https://claude.ai)

Works with **Claude** · **ChatGPT** · **Gemini** · any LLM that supports system prompts

---

## What Is This?

Evi Content is AB Tasty's AI visual editor. You describe a modification in natural language — Evi generates the JavaScript to inject it into your page, live, without deployment.

The quality of what Evi generates depends entirely on the quality of your prompt.

**This skill gives any LLM the structure, constraints, and templates to generate optimal Evi Content prompts** — specific, concise, and technically sound — for any industry and any type of A/B variation.

---

## Available Skill

### [`abtasty-evi-prompt-agent`](./abtasty-evi-prompt-agent.md) — Evi Content Prompt Generator

> **Structured input. Optimized prompt. Ready to paste into Evi.**

Turns your test context (selector, objective, style, behavior) into a prompt that Evi can interpret without ambiguity. Embeds AB Tasty-specific technical guardrails silently so you don't have to think about them.

#### What It Handles

| Category | Examples |
|---|---|
| **Animation / Visual Effect** | Fade-in on load, scroll-triggered reveal, hover glow |
| **CTA / Button Optimization** | Color shift, pulse, text replacement, scale on hover |
| **Widget / Injected Element** | Progress bars, banners, toast notifications, overlays |
| **Personalization** | Dynamic content from dataLayer, cookie, localStorage |
| **Form / Checkout Enhancement** | Field validation states, focus effects, error feedback |

#### Required Inputs

Before generating, the agent asks for:

| Input | Description |
|---|---|
| **Selector** | CSS selector of the target element (`#add-to-cart`, `.hero-title`) |
| **Objective** | One sentence — what should change visually or behaviorally |
| **Style** | Exact values preferred: hex colors, px sizes, ms durations |
| **Behavior** | Trigger, timing, conditions, fallback |
| **Language** | Language of the output prompt (French, English, etc.) |

If any input is missing, the agent asks before generating.

#### Technical Guardrails (Applied Silently)

The skill embeds AB Tasty-specific constraints into every prompt it produces:

- **`position: fixed` elements** → always appended to `document.body` (AB Tasty's wrapper breaks fixed positioning otherwise)
- **Dynamic DOM** → `MutationObserver` used when page JS re-initializes content
- **dataLayer access** → recursive search function, never index-based (`dataLayer[4]`)
- **Loop scoping** → `let`/`const` enforced to prevent closure bugs on dynamic elements
- **Event listeners** → `stopImmediatePropagation()` avoided unless strictly necessary
- **Prompt non-cumulability** → each variation is its own prompt; previous prompts must be deleted in Evi before creating a new one — they do not stack

#### Output Format

Every prompt is delivered in a labeled, copyable block:

```
─────────────────────────────────────
EVI CONTENT PROMPT — Variation B — v1
─────────────────────────────────────
[CONTEXT]
Page: product page
Target element: #add-to-cart

[OBJECTIVE]
Make the add-to-cart button pulse periodically to attract attention.

[VISUAL SPEC]
- Scale: 1.05x at peak
- Transition: ease-in-out
- Duration: 600ms per cycle

[BEHAVIOR]
- Trigger: on page load, after 2000ms delay
- Timing: repeat every 3s
- Fallback: none required

[CONSTRAINTS]
- Minimal JS only, no IIFE, no external libraries
─────────────────────────────────────
```

[View full skill →](./abtasty-evi-prompt-agent.md)

---

## How to Install

### Option 1 — Claude Project (recommended)

1. Open [claude.ai](https://claude.ai) and create a new Project
2. Go to **Project instructions**
3. Paste the full content of [`abtasty-evi-prompt-agent.md`](./abtasty-evi-prompt-agent.md)
4. Save — every conversation in that project now uses the agent

### Option 2 — Any LLM with system prompt support

Copy the content of [`abtasty-evi-prompt-agent.md`](./abtasty-evi-prompt-agent.md) into your system prompt field. Works with ChatGPT (custom instructions), Gemini, Mistral, and any other LLM.

### Option 3 — Per conversation

Paste the skill content at the start of any conversation with your preferred LLM.

---

## Usage Example

```
User:
- Selector: #add-to-cart
- Objective: Make the add-to-cart button pulse periodically to attract attention
- Style: scale 1.05x at peak, ease-in-out, 600ms per cycle
- Behavior: trigger on page load after 2s delay, repeat every 3s
- Language: English

Agent:
─────────────────────────────────────
EVI CONTENT PROMPT — Variation B — v1
─────────────────────────────────────
[CONTEXT]
Page: product page
Target element: #add-to-cart

[OBJECTIVE]
Make the add-to-cart button pulse periodically to attract attention.

[VISUAL SPEC]
- Scale: 1.05x at peak
- Transition: ease-in-out
- Duration: 600ms per cycle

[BEHAVIOR]
- Trigger: on page load, after 2000ms delay
- Timing: repeat every 3s
- Fallback: none required

[CONSTRAINTS]
- Minimal JS only, no IIFE, no external libraries
─────────────────────────────────────
```

> **Note on injected widgets (banners, toasts, overlays):** when the objective is to inject a new element with `position: fixed`, the target element in the prompt becomes `document.body` — not the original selector. The selector provided by the user is used as the trigger context, not the injection point. The agent handles this automatically.

---

## Contributing

Fork it, adapt it to your stack or industry, submit a PR. Issues and suggestions welcome.

---

## License

MIT — free to use, modify, and distribute.
