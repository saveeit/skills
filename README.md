# Savee agent skills

[Agent Skills](https://skills.sh/) for [Savee](https://savee.com). Drop them into Claude, Cursor, or any agent that supports the format, and the agent can work with your Savee account through natural language — no client code required.

## What's inside

| Skill | Path | What it does |
| --- | --- | --- |
| `api` | [`skills/api/`](skills/api/) | Read the signed-in user's saves, boards, and home feed via the Savee Public REST API. |

## Install

```sh
npx skills add https://github.com/saveeit/skills --skill api
```

## Configure

The `api` skill talks to a paid Savee account. After installing:

1. Generate a personal access token at <https://savee.com/settings/> → **API Access**. Tokens are scoped to your account and look like `sv_live_…`. Treat them like a password.
2. Expose the token to your agent as the environment variable `SAVEE_TOKEN` (or whatever variable your agent host expects — point it at the value from step 1).

The skill never stores your token; it only tells the agent that one is needed and how to use it.

## Try it

Once installed, prompts like these should activate the `api` skill:

- "Fetch the latest 10 saves from my Savee account and summarize them."
- "Pull my Savee feed and group the saves by who posted them."
- "List my Savee boards and show how many saves each one has."
- "Build a JSON file with every save on my 'Posters' board."

If the agent doesn't pick the skill up, mention "Savee" or "savee.com" explicitly in the prompt.

## Updates

The skill points at the live OpenAPI document (<https://api.savee.com/v1/openapi.json>), so it picks up new endpoints and fields automatically — no skill update needed when the API changes. Republish only when worked examples or framing change.

## Issues

Bug reports and feature requests welcome at <https://github.com/saveeit/skills/issues>. For API-level questions (rate limits, endpoint behavior, error codes) see the developer docs at <https://docs.savee.com>.
