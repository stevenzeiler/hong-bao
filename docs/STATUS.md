# Status

Last reviewed: 2026-11-20 (github-audit pass 02, docs only).

## What works

Nothing was run in this pass. From reading the code:

- The Express server is small and should start with `node server.js` once dependencies are installed **(not verified)**.
- `public/` holds a complete static front end for the buy flow.

## What's broken or unknown

- `npm test` calls itself and never runs a test.
- mocha is not a dependency; most tests need live Ripple and gatewayd services, and `test/pathfinder.js` uses `assert` without requiring it.
- `test/router.js` is a placeholder with an empty `describe` block.
- The card-payment endpoint (`POST /stripe`) is documented in `public/api.html` but not implemented in `server.js`.
- The services it talked to in 2014 (Ripple endpoints, Open Exchange Rates account, card account, `s1.ripple.com` websocket usage) may be gone or changed.
- Secrets in source: `lib/open_exchange_client.js` (line 5) holds an Open Exchange Rates app id, and `public/js/main.js` (line 30) holds a card-payment public key. The public key is meant to be public. The app id is a credential. It is still in git history, so rotation and any history cleanup are Steven's call.
- Editor swap files `.index.html.swp` and `public/src/.DS_Store` are committed.
- `package.json` points to a repository named `ripplelaunch.com` and has an empty description.

- `LICENSE` names "Steven Zeiler and contributors" because Abiy Seifu also contributed code. Whether his contributions are covered by the ISC license is Steven's call.

## What's next

1. Decide whether to keep this as a read-only showcase or archive it (Steven's decision).
2. If keeping it: fix the test script, add mocha as a dev dependency, move keys to environment variables.

## Not yet from the standard

- CONTRIBUTING.md
- SECURITY.md
- .editorconfig
- .github issue and pull request templates
- Dependabot configuration
- `ci.yml` with gitleaks
- Rename `master` to `main`
- CloudEvents catalog
- Product one-pager
