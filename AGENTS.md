# aiquota

Single-file Python 3 CLI (`aiquota`) that shows weekly Claude Code / Codex quota
with a pace marker. Standard library only; do not add dependencies.

## Boundaries

- Read-only toward the providers: never write to `~/.claude/.credentials.json`,
  `~/.claude.json`, `~/.claude-*/`, `~/.codex/auth.json` or any other CLI
  config. Do not refresh OAuth tokens.
- Never print tokens, emails or account IDs; the UI shows plan names only.
- Keep the Claude endpoint polled at most once per `FETCH_TTL` (it returns 429
  when hammered). Watch-mode redraws must not trigger extra fetches.
- User-facing strings live in `STRINGS`; add every new key to both `en` and `vi`.

## Checks

No test suite yet. Before committing:

```sh
python3 -m py_compile aiquota
AIQUOTA_LANG=en COLUMNS=40 ./aiquota
AIQUOTA_LANG=vi COLUMNS=72 ./aiquota
```

Every frame line must have the same visible width at a given `COLUMNS`
(strip ANSI escapes before measuring).

Regenerate `docs/screenshot.png` from a real terminal when the layout changes.
