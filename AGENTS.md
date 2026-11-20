# AGENTS.md

Guidance for AI agents working in this repo. Humans: see `README.md`.

## What this is

`hong-bao` (package `ripplelaunch`) is a dormant 2014 Node.js web app for buying XRP. Treat it as a historical showcase, not a live service.

## Stack

- Node.js with Express `^4.7.4`, ejs `^1.0.0`, superagent `^0.18.2`, bluebird `^2.3.0`, async `^0.9.0`, qs, body-parser, supertest `^0.13.0`.
- Front end: Bootstrap, jQuery, Backbone, underscore, the Ripple JS library 0.7.38 and a Famo.us view, all committed under `public/`.
- Tests use mocha-style `describe`/`it`, but mocha is not listed in `package.json`.
- Default branch: `master`.

## Layout

- `server.js`: starts Express on port 5656.
- `index.js`: the router (static files plus `/bridge/payments/:alipay_username/:amount`).
- `lib/`: `pathfinder.js`, `build_payment.js`, `currency_converter.js`, `federation_resolver.js`, `open_exchange_client.js`.
- `test/`: one file per `lib/` module plus an empty `router.js`.
- `public/`: browser app and vendored libraries.
- `docs/STATUS.md`: current state and the gap to the repo standard.

## Commands

- Install: `npm install` (not verified on a current Node).
- Run: `node server.js`, port 5656.
- Test: `npm test` is known not to work. The script is `"test": "npm test"`, a loop. Running mocha directly (`npx mocha test/`) would need live Ripple and gatewayd services for most tests, and `test/pathfinder.js` uses `assert` without requiring it. Say plainly in any PR if you could not run them.

## Rules

- Add or update tests with every code change.
- Never commit secrets. The repo already holds an exchange-rate API id in `lib/open_exchange_client.js`. Do not copy it anywhere, and do not add new keys. Use environment variables.
- Use Conventional Commits (`docs:`, `fix:`, `feat:`, `chore:`).
- Keep `docs/STATUS.md` current when behaviour or docs change.

## What agents may and may not do

- May: improve docs, fix clear bugs, add tests, propose changes as pull requests.
- May not: archive the repo, publish packages, rewrite git history, rotate keys, or change the default branch without Steven's say-so.
- Do not touch the vendored files in `public/lib` and `public/js/vendor`.
