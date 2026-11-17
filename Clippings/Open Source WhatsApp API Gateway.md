---
title: "Open Source WhatsApp API Gateway"
source: "https://www.open-wa.org/"
author:
  - "[[Yudhi Armyndharis]]"
published: 2025-01-01
created: 2026-10-22
description: "OpenWA - The free, open source WhatsApp API Gateway with a pluggable architecture. Self-hosted, swap your database/storage/cache/engine, production-ready, no vendor lock-in."
tags:
  - "clippings"
---
## Everything you need to ship.

A complete WhatsApp integration platform — **100% free and open source**, production-ready out of the box.

### Core

- Full REST API
- Multi-Session Support
- Real-time Webhooks (HMAC)
- Web Dashboard (9 Locales)
- Scoped API Key Auth
- Swagger Docs

### Messaging

- Text Messages
- Images & Videos
- Documents & Audio
- Message Reactions
- Bulk Messaging
- Delivery Status

### Infrastructure

- SQLite / PostgreSQL
- Redis Cache + Queues
- S3 / MinIO Storage
- Multi-arch Docker
- Non-root Container
- Health & Migrations

## Built on a pluggable core.

Swap your database, storage, cache, and even the WhatsApp engine — all from config. **Zero code changes.**

### Pluggable Architecture

Database (SQLite / PostgreSQL), storage (Local / S3 / MinIO), and cache (Memory / Redis) are swappable adapters — configured, not coded. Move from local dev to production scale without touching application logic.

SQLitePostgreSQLLocalS3MinIORedis

### Dual WhatsApp Engine

Choose your engine per deployment via `ENGINE_TYPE`. Ship with the battle-tested `whatsapp-web.js` (Puppeteer) by default, or switch to the lightweight `baileys` WebSocket engine when you'd rather skip the browser entirely.

whatsapp-web.jsbaileys

## Why developers choose OpenWA.

```js
OpenWA
```
```js
Free Forever
```

| Feature | W. Core | W. Plus | W. Cloud |
| --- | --- | --- | --- |
| Price | Free | $50+/mo | $30+/mo |
| Open Source |  |  |  |
| Multi-Session | Limited |  |  |
| Web Dashboard |  |  |  |
| PostgreSQL |  |  | N/A |
| Webhook UI |  |  |  |
| Source Code |  |  |  |
| Self-Hosted |  |  |  |

Comparison reflects publicly available feature listings as of 2026. Competitor names are abbreviated. Features and pricing may change — verify on their official sites before deciding.

## Live in 5 minutes.

**One command with Docker**, or a quick local setup for development — no complicated config, no surprises.

```js
# Clone and start with Docker (single-container quick start)
git clone https://github.com/rmyndharis/OpenWA.git
cd OpenWA
docker compose -f docker-compose.dev.yml up -d

# Dashboard & API are bundled on one port:
# http://localhost:2785
```

```js
# Clone and run locally
git clone https://github.com/rmyndharis/OpenWA.git
cd OpenWA

# Install dependencies (includes dashboard)
npm install

# Start API + Dashboard with hot reload
npm run dev

# Dashboard: http://localhost:2886
```

Dashboard`:2785`

REST API`:2785/api`

Swagger`:2785/api/docs`

In `npm run dev` (local) the dashboard runs on its own Vite server at `:2886` with hot reload. In Docker it's bundled into the API image and served on `:2785`. For production, deploy using `docker compose up -d`, with optional scaling profiles: `--profile postgres`, `--profile redis`, `--profile minio`, or `--profile full`.

## Built on a modern, trusted stack.

Proven, production-grade tools — chosen for **reliability, not novelty**.

![Node.js](https://www.open-wa.org/assets/tech/nodejs.svg) Node.js 22 ![NestJS](https://www.open-wa.org/assets/tech/nestjs.svg) NestJS 11 ![TypeScript](https://www.open-wa.org/assets/tech/typescript.svg) TypeScript 5 ![React](https://www.open-wa.org/assets/tech/react.svg) React 19 ![PostgreSQL](https://www.open-wa.org/assets/tech/postgresql.svg) PostgreSQL ![Redis](https://www.open-wa.org/assets/tech/redis.svg) Redis + BullMQ ![Docker](https://www.open-wa.org/assets/tech/docker.svg) Docker Multi-arch ![Socket.IO](https://www.open-wa.org/assets/tech/socketio.svg) Socket.IO

TypeORM for data access · Vite + TanStack Query + i18next power the dashboard · Helmet & NestJS Throttler harden the API · Pluggable WA engine: `whatsapp-web.js` (default) or `baileys` via `ENGINE_TYPE`.

## An ecosystem, not just an API.

Connect OpenWA to **the tools you already use**.

### [n8n Nodes](https://github.com/rmyndharis/OpenWA-n8n)

Official community nodes — `@rmyndharis/n8n-nodes-openwa` — for building WhatsApp automations across hundreds of services.

Install in n8n →

### [ioBroker Adapter](https://github.com/ThorstenBoettler/ioBroker.openwa)

Community-maintained adapter for home & IoT automation, with Blockly blocks for text, image, video, audio and document messages.

View adapter →

### [Official SDKs](https://github.com/rmyndharis/OpenWA/tree/main/sdk)

Hand-written, fully-typed client libraries for the REST API — JavaScript/TypeScript (`@rmyndharis/openwa`), Python (`rmyndharis-openwa`) and PHP (`rmyndharis/openwa`), published to npm, PyPI and Packagist.

Get the SDKs →

## Make it yours. Build a plugin.

OpenWA is **yours to shape**. Got an idea? Spin up a plugin — it comes alive on real WhatsApp events through typed lifecycle hooks: send replies, query chats and contacts, reach your own services, all behind a safe, permission-gated API. **No fork, no core changes.** Build it, share it with the community, and make the gateway do exactly what you imagined.

- React to events
- Send & reply
- Query & call out

## Shipping, in the open.

Every release, pulled live from the source `CHANGELOG.md` — no copy-paste, **always current**.

Added
- Add Number Checker page in dashboard for single and bulk WhatsApp recipient pre-validation, in every dashboard language.
- Add the opt-in `message.receipt` event for per-recipient group and status receipts on Baileys (#1748).
- Record plugin install, update, uninstall, enable, disable and configuration changes in the audit log.
- Add `QUEUE_PREFIX` to set the Redis key prefix of the BullMQ queues, so deployments that share a Redis stop taking each other's webhook jobs.
- +6 more in this release

Changed
- Support Guzzle 8 in the PHP SDK while retaining Guzzle 7 compatibility (#1870).
- Reject empty PHP SDK `defaultHeaders` lists before sending requests; use `''` for an empty header value (#1870).
- Convert legacy message types in a one-time migration instead of on every boot, which read the whole messages table before the HTTP port opened.
- Open the HTTP port after at most 60 s of plugin restore; plugins still restoring finish in the background.
- +9 more in this release

Fixed
- Keep deleted sessions free of late message, status and bulk writes.
- Retain sending limits while hooks or preparation are pending, including across UTC midnight.
- Preserve whatsapp-web.js readiness when an earlier QR render completes.
- Cancel stale Message Tester actions after logout, key changes or leaving the page.
- +40 more in this release

Added
- Allow chat-restricted API keys to subscribe to chat WebSocket events.
- Allow chat-restricted MCP keys to read and send within their chat allowlist using the REST authorization rules.
- Carry `chatId` in `message.ack` and `message.failed` payloads so a webhook `chatId` or `kind` filter scopes delivery events per chat.
- Filter stored messages by time, direction, type or message reference, with stable message-time pagination; the JavaScript, Python, Java and Go SDKs take these filters from SDK 0.6.0, and the PHP SDK already forwards any query key.
- +9 more in this release

Changed
- On PostgreSQL, inbound media that waits `2 x MEDIA_DOWNLOAD_TIMEOUT_MS` without a free slot arrives with the omitted marker instead of being downloaded.
- On PostgreSQL, a chat's messages are stored in arrival order, so a text waits for earlier media in its chat.
- On PostgreSQL with whatsapp-web.js, a held message's contact and quoted-message lookups wait at most `MEDIA_DOWNLOAD_TIMEOUT_MS`.
- The JavaScript SDK release job runs `npm audit` over the SDK tree before it installs, tests and publishes.
- +18 more in this release

Fixed
- Bound each webhook and ingress queue command at 2 s once Redis has connected, so a Redis that stops answering falls back to direct delivery and inline dispatch instead of holding every dispatch and ingress request.
- Keep the dashboard chat's scroll-to-bottom button in view while the reader is scrolled up, where it moved with the thread and was off screen.
- Land the dashboard chat's scroll-to-bottom button at the bottom when an older page arrives meanwhile, where the animated jump could end far above it.
- Keep the dashboard's reaction popover inside the thread, where the emoji nearest one of its edges was clipped and could not be picked.
- +119 more in this release

Documentation
- The integration docs say `integration_delivery_failures` is written only for failed inbound deliveries.
- The API reference, database design, runbook and glossary describe when the webhook outbox copy is retired after a sweep replay or a redrive, and which rows neither path recovers.
- Document the memory media messages and parked webhook deliveries hold during a media burst, and the settings that limit it.
- The storage migration guide says to check the store size and file count against the import caps before switching backends, and how to re-run an aborted import.
- +3 more in this release

Dependencies
- `handlebars` 4.7.9 to 4.7.10, closing two critical advisories in which a crafted template could inject JavaScript into compiled output.
- `vitest` 2.1 to 5 in the JavaScript SDK tree, closing its dev-only advisories, and `typescript` 5.9 to 7.
- `@modelcontextprotocol/sdk` 1.30.0 to 1.32.1, closing a high-severity advisory in its OAuth client (GHSA-6qxp-vccf-f47h).
- `sharp` ^0.35.4 to ^0.35.5, closing a high-severity advisory in its bundled librsvg (GHSA-wq5f-xc86-pv6w).
- +5 more in this release

Upgrade notes (behavior changes)
- Set `stop_grace_period` (Docker) or `terminationGracePeriodSeconds` (Kubernetes) to at least 75 s if you pinned your own 45 s value, plus the excess of `SHUTDOWN_DELAY_MS` over 3 s and of `WEBHOOK_SHUTDOWN_DRAIN_MS` over 5 s.
- A stop that runs 67 s past the shutdown delay now exits with status 1 instead of being killed (137), which matters if you alert on exit codes.
- A sandboxed plugin's `onDisable` now shares one 10 s cap with all other plugins at shutdown, and a worker still running then dies with the process.
- `docker-compose.dev.yml` now waits up to 75 s on a stuck stop instead of Docker's 10 s default.
- +26 more in this release

Security
- Drop a Baileys edit, revoke or reaction from another chat, an edit from the wrong author, or a one-to-one revoke from the other side, aimed at a message still being downloaded, on SQLite too; a contact who knew the id could trigger `message.edited`, `message.revoked` or `message.reaction` for someone else's message while it downloaded.
- Drop a Baileys edit, revoke or reaction that the stored message proves foreign (another chat, or a one-to-one change by the other party), also when the engine's own message store no longer holds the original; a contact who knew the id of a history-synced message, or one older than the newest `BAILEYS_MESSAGE_STORE_LIMIT` messages, could rewrite or erase it.
- Drop a Baileys message that reuses the id of one still being downloaded under another chat or sender, so it cannot take the id or stand in for the original when a later delete is judged.
- Drop the stored copy of a Baileys message that reuses the id of a message the gateway already holds under another chat, sender or direction, and hold an edit, delete or reaction that reads as foreign to that copy until the gateway has settled the message, so the real message's change is no longer ignored as foreign; a reusing message deleted by its sender while it downloads on SQLite, or skipped as ephemeral, is never settled and keeps its copy.
- +3 more in this release

[View full changelog on GitHub](https://github.com/rmyndharis/OpenWA/blob/main/CHANGELOG.md)

## Frequently Asked Questions

Got questions? We've got answers.

Yes. OpenWA is 100% free and open source under the MIT license — no licensing fees, no feature locks, and full source code access. You can use it in personal and commercial projects without any restrictions.

No. OpenWA is an independent, community-driven open-source project and has **no affiliation, association, authorization, endorsement, or official connection with Meta Platforms, Inc., WhatsApp LLC**, or any of their subsidiaries or affiliates.

This software is developed independently to help developers integrate WhatsApp capabilities into their own applications using self-hosted infrastructure. All registered trademarks and logos belong to their respective owners.

Because OpenWA is self-hosted and acts as a gateway on your own infrastructure, account safety is entirely determined by your messaging behavior. WhatsApp's automated spam detection filters look for bot-like patterns on their network, and any automated third-party integration carries some risk if abused.

To minimize these risks, OpenWA is specifically engineered with built-in protection mechanisms:

- **Simulated Human Behavior:** Configurable simulated typing indicators and randomized message delivery intervals.
- **Session Proxying:** Ability to route each session through a dedicated proxy IP to match account locations.
- **Strict Rate-Limiting:** Hardened limits to prevent bursting message delivery.
- **Official Engine Parity:** Stays aligned with standard web browser and network protocols to avoid protocol fingerprinting flags.

To keep your account safe, we strongly recommend warming up new numbers, avoiding cold outreach/spam, and using OpenWA primarily for transactional notifications, customer service, or opt-in communication.

Yes. OpenWA is designed for self-hosting with a single Docker command. The API and the dashboard are bundled together on port `2785`, making it easy to deploy to any cloud provider, VPS, or local server.

The default engine is `whatsapp-web.js` (a Puppeteer-based headless browser). You can also switch to the lightweight `baileys` engine (a WebSocket-based implementation) via the `ENGINE_TYPE` environment variable to save resources and run browserless.

Yes. OpenWA's pluggable architecture lets you swap the database (SQLite / PostgreSQL), media storage (Local / S3 / MinIO), and cache layer (Memory / Redis) purely from configuration without changing any code.

## Built in the open.

OpenWA is open from the first commit to the latest release. MIT licensed, free forever, and open to contributions of every kind — code, documentation, or a well-written bug report.

MITLicense

100%Free

OpenSource

### How to contribute

1. 01Fork the repository
2. 02Create your feature branch
3. 03Commit your changes
4. 04Push to the branch
5. 05Open a Pull Request

### The people behind OpenWA

Every developer who has shipped code, docs, or fixes — pulled live from GitHub. Thank you. ♥