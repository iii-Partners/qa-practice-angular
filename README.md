# qa-practice-angular

A viiibin **practice repo**. Bare Angular CLI scaffold paired with a
[`SPEC.md`](./SPEC.md) describing exactly what the agent should build.

## Use it

1. Open viiibin → New Project → Import from GitHub
2. Paste: `https://github.com/iii-Partners/qa-practice-angular`
3. Once the workspace loads, ask the agent: **"Read SPEC.md and build it."**
4. Watch the preview update with the implemented feature.

## What you get

- Angular 21 (standalone components, signals, control flow) + TypeScript
- Dev server bound to `0.0.0.0:3000` (so viiibin's preview proxy finds it)
- A clean `app.html` template — empty `<main />`, no demo content
- A standard `SPEC.md` with strict, parseable acceptance criteria

## Why "practice"?

This repo is part of viiibin's framework validation matrix
([milestone M57](https://github.com/iii-Partners/viiibin/milestone/103)).
The same SPEC across nine framework variants — React, Next.js, Astro, Vue,
Nuxt, Svelte/Kit, Remix, Angular — proves the platform handles each one
end-to-end. The repos are also a clean starting point for anyone evaluating
viiibin.

## Local sanity check

```bash
npm install
npm run dev    # http://localhost:3000
npm run build  # → dist/qa-practice-angular/browser/
```

## Framework notes

- Angular CLI defaults to `:4200` and `localhost` only — both
  `start` and `dev` are pinned to `ng serve --host 0.0.0.0 --port 3000` so
  viiibin's preview proxy finds the server reliably.
- viiibin's prep script appends `--host 0.0.0.0 --port 3000` to
  `npm run dev` for non-Vite, non-Next frameworks. Angular CLI tolerates the
  duplicate flags; the last value wins.
- Angular 21's `@angular/build:dev-server` enforces a host allowlist (CVE
  parity with Vite 5.4+). viiibin's preview proxy hits the sandbox via a
  random subdomain (`3000-<sandbox-id>.e2b.app`), which Angular blocks with
  a 403. `angular.json` here sets `serve.options.allowedHosts: ["all"]` to
  bypass that check inside the practice/sandbox environment. Tracking a
  proper platform fix in viiibin#1182 — when that ships, this override can
  be dropped (or made dev-only).
- Use Angular 21 idioms: standalone components, signals (`signal()`,
  `computed()`, `effect()`), the new control-flow syntax (`@if`, `@for`,
  `@switch`). The agent should default to these — no NgModules.
- Components should declare their template imports (e.g. `RouterOutlet`)
  in their `imports: []` array.

## License

MIT — see [LICENSE](./LICENSE).
