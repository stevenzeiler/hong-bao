# hong-bao

The source of Ripple Launch (`ripplelaunch.com`): a mobile-first web app for buying XRP with a card and sending it to a Ripple address or name.

> **Status: dormant since 2014.** The last commit is from August 2014. This is a 2014 experiment built on the Ripple network, kept for the record. The services it talks to (Ripple's 2014 endpoints, the old gateway bridge, a payment account) are unlikely to work today, and the code has not been run or tested as part of this documentation pass.

The repo name is the Chinese word for a red envelope, a gift of money. The npm package is called `ripplelaunch`.

## What is in here

- `server.js` and `index.js`: a small Express server that serves `public/` and exposes one route, `GET /bridge/payments/:alipay_username/:amount`.
- `lib/`: building blocks for a USD to CNY payment: a Ripple pathfinder, a payment builder, a currency converter, a Ripple name (federation) resolver and an Open Exchange Rates client.
- `public/`: the browser app (Bootstrap, jQuery, Backbone, the Ripple JS library, a Famo.us version in `public/src/famous.js`) plus `api.html`, a short note on the `POST /stripe` request the buy flow was designed around.
- `test/`: mocha-style tests for the `lib/` modules.

## Install

    npm install

You need Node.js. The dependencies are 2014 versions (Express 4.7, superagent 0.18, bluebird 2). Whether they install cleanly on a current Node is unknown.

## Usage

    node server.js

The server listens on port 5656. Open `http://localhost:5656/`. The buy flow needs live Ripple, card-payment and exchange-rate services that were configured in 2014, so expect only the static pages to load.

## Configuration

There are no environment variables. The 2014 code keeps its service settings in the source:

- an Open Exchange Rates app id in `lib/open_exchange_client.js`
- a card-payment public key in `public/js/main.js`

If you revive this, move these into environment variables first. See `docs/STATUS.md`.

## How it works

1. The visitor chooses an amount and enters a Ripple name.
2. The name is resolved to a Ripple address through federation.
3. The browser sends the amount and a card token to the server (`POST /stripe`, described in `public/api.html`).
4. The server finds a payment path, and the browser follows progress over a websocket to the Ripple network.

Steps 3 and 4 are described from the front-end code and the API note. The server in this repo only contains the `/bridge/payments` route, so the card-payment endpoint may have lived elsewhere or been lost.

## Tests

    npm test

As committed, `package.json` sets the test script to `npm test`, which calls itself, so it does not run the tests. The tests in `test/` also need a mocha install and live services. See `AGENTS.md` and `docs/STATUS.md`.

## License

ISC, as declared in `package.json`. See `LICENSE`.
