---
name: savee-public-api
description: Read the authenticated user's saves, boards, and home feed from Savee.com via its Public REST API. Use when the user wants to fetch their Savee data — latest saves, home feed, or saves on a specific board — from a script, embed, or agent.
---

# Savee Public API

A read-only REST API that returns the authenticated user's saves, boards, and feed as JSON. Available to paid users with a personal access token.

## Auth

Every request needs `Authorization: Bearer sv_live_…`. The user generates a token at <https://savee.com/settings/> → "API Access". Treat it like a password — anyone with it can read the account.

## Base URL

`https://api.savee.com/v1/`

## Live OpenAPI spec

The authoritative request/response shapes live at <https://api.savee.com/v1/openapi.json>. Fetch it whenever you need a field-by-field reference; this skill only documents the human-friendly summary and worked examples.

Endpoints at a glance:

- `GET /v1/me` — the authenticated user
- `GET /v1/saves` — the user's own saves, newest first
- `GET /v1/feed` — saves from people the user follows
- `GET /v1/boards` — every board the user can see (returned all at once, not paginated)
- `GET /v1/boards/{boardID}/saves` — saves on a specific board

All list endpoints except `/v1/boards` accept `?limit=` (default 30, max 100) and `?cursor=` (opaque — pass `next_cursor` back verbatim).

## When to use this skill

Pattern-match on intents like:

- "fetch my latest saves on Savee"
- "show me my Savee feed"
- "embed my saves on my website"
- "list my Savee boards"
- "build a dashboard / agent that reads from Savee"

See `examples/` for the two most common flows.

## Errors

Uniform JSON shape: `{ "error": { "code": "...", "message": "..." } }`. Notable codes:

- `401 UNAUTHORIZED` — missing or invalid token. Ask the user to regenerate.
- `402 PAYMENT_REQUIRED` — the account doesn't have an active Savee subscription.
- `403 FORBIDDEN` — the Public API isn't enabled for this account yet.
- `429 TOO_MANY_REQUESTS` — wait `Retry-After` seconds before retrying.

Rate limits are 60 req/min and 5000 req/hr per token.
