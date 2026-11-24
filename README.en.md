# FlagshipRouter Free Model Gateway

A one-click wrapper around [FlagshipRouter](https://github.com/theRizwan/FlagshipRouter) (a local OpenAI-compatible gateway built on 9router). Install, start, generate an API key, tick the models you want, and they appear in Ruodao's model list.

## What it does

- **One-click install** - downloads the upstream source, installs dependencies and builds the gateway, with progress visible and resumable after closing the panel.
- **Service lifecycle** - starts and stops the gateway, picks a free port when the default is taken, and keeps its data directory isolated.
- **API keys** - generates and stores the gateway key locally so the host can call it.
- **Model import** - lists the models the gateway exposes and imports selected ones into Ruodao's model manager.

## Requirements

- Ruodao desktop host on Windows with Node.js available.
- Network access for the first install.

## Permissions and privacy

- `network`, `process`.
- The gateway binds to localhost; no traffic is proxied through Ruodao servers.

## Links

- Upstream: https://github.com/theRizwan/FlagshipRouter
- Marketplace: https://ruodao.com/plugin-market

## License

MIT (integration layer); upstream follows its own license.
