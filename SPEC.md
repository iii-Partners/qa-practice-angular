# SPEC: Hello viiibin v2

> This is the canonical viiibin practice-repo SPEC.md template.
> Every `qa-practice-*` repo customizes the **User story** and
> **Acceptance criteria** below for its framework. The shape stays the same —
> both the agent (which reads this as its prompt) and the Playwright validator
> (which parses acceptance criteria into assertions) depend on it.

## User story

A user opens the app and sees a header with the text **"Hello viiibin v2"**.
Below the header is a button labeled **"Click me"**. Clicking the button
shows an alert with the text **"Practice complete."**.

The implementation must be idiomatic for the project's framework — use the
framework's standard component model, file layout, and interactivity
primitives. No custom routers or framework-replacement libraries.

## Acceptance criteria

The Playwright validator (`apps/web/tests/e2e/customer-framework-practice.spec.ts`)
parses each line below and runs it as a strict assertion against the running
preview. Add or remove lines per practice repo, but keep the syntax exact.

- [ ] text-on-page: "Hello viiibin v2"
- [ ] element-visible: button:has-text("Click me")
- [ ] click-then-text: button:has-text("Click me") → "Practice complete."
- [ ] no-console-error
- [ ] no-network-404

### Assertion grammar

| Line prefix | Asserts | Example |
|---|---|---|
| `text-on-page: "<exact string>"` | The given string appears verbatim somewhere on the rendered page (whitespace-collapsed) | `text-on-page: "Hello viiibin v2"` |
| `element-visible: <css selector>` | An element matching the selector is visible (uses Playwright `:visible`) | `element-visible: button:has-text("Click me")` |
| `click-then-text: <css selector> → "<exact string>"` | Click the selector, then assert the given text appears (in an alert dialog, toast, or new element) | `click-then-text: button:has-text("Click me") → "Practice complete."` |
| `no-console-error` | No `console.error` calls fired during the test session | (no argument) |
| `no-network-404` | No HTTP request returned a 404 during the test session | (no argument) |

Strings are matched **exactly** (case-sensitive, after whitespace collapse).
LLM-judged matching is explicitly out of scope — the spec is reproducible by
design.

## Constraints (advisory)

These don't fail the test, but they're part of the agent's prompt:

- Don't add new dependencies unless the framework requires them
- Don't replace the project's package manager (use whatever the lockfile
  indicates — `package-lock.json` → npm, `yarn.lock` → yarn, `pnpm-lock.yaml`
  → pnpm)
- Don't restructure the project's directory layout
- Use the framework's standard hydration/interactivity directive when
  applicable (e.g., `client:load` in Astro, `"use client"` in Next.js
  App Router)
