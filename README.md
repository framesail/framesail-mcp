# Framesail MCP Server

[![framesail-mcp MCP server](https://glama.ai/mcp/servers/framesail/framesail-mcp/badges/score.svg)](https://glama.ai/mcp/servers/framesail/framesail-mcp)

Official remote MCP server for [Framesail](https://framesail.com) — create long-form (faceless YouTube) videos end to end from any MCP client: script, locked character references, storyboard, voiceover, and final video editing — with characters and style held consistent across every shot.

Making long-form AI video today means 8+ tabs stitched by hand — an LLM for the script, a voice model, an image model, a video model — with characters drifting between tools and style resetting at every export. Framesail replaces the patchwork: the whole pipeline runs in one place and manages your video's context end to end.

Six stages: **Style** (paste images, videos, or YouTube links and Framesail reverse-engineers the look, voice, and direction), **Script** (write it yourself or generate it in your narrative style), **Reference images** (auto-generated for every character, place, and prop), **Voiceover** (one narrator or many characters, with word-level timing), **Storyboard** (planned scene by scene), and **Editor** (captions, music, SFX, then export).

No black box: you control every prompt, asset, model, and setting.

This repository documents the hosted server. The service itself is closed-source and runs at:

```
https://api.framesail.com/mcp
```

- **Transport:** streamable HTTP
- **Auth:** OAuth 2.1 (Dynamic Client Registration + PKCE) or `fsk_` API keys
- **Registry:** [`com.framesail/framesail`](https://registry.modelcontextprotocol.io) (official MCP registry) · [Glama connector](https://glama.ai/mcp/connectors/com.framesail/framesail)
- **Docs:** [framesail.com/developers](https://framesail.com/developers) · [API reference](https://framesail.com/developers/docs)

## Connect

**claude.ai / Claude Desktop** (OAuth — no key handling):

> Settings → Connectors → Add custom connector → `https://api.framesail.com/mcp`

A browser login opens; approve the consent screen and you're connected.

**Claude Code:**

```sh
claude mcp add --transport http framesail https://api.framesail.com/mcp \
  --header "Authorization: Bearer fsk_..."
```

**Cursor / other MCP clients:** point at the URL above with an `Authorization: Bearer fsk_...` header. Create keys on your [account page](https://framesail.com/app/account); every connection (OAuth or key) shows up there and is revocable.

## What the tools cover

The full production pipeline, as tools — every tool carries a title and safety annotations (`readOnlyHint` / `destructiveHint`):

| Stage | Examples |
|---|---|
| Channels & projects | create/list channels, projects, styles |
| Script | generate a script from a brief, scan it into character/environment/object assets |
| References | generate locked reference images per asset, set the art style |
| Voiceover | render word-timed narration (ElevenLabs / MiniMax voices) |
| Storyboard | plan one frame per shot against the locked references |
| Render | animate segments, assemble, export the finished MP4 |
| Account | whoami, credit balance, job status |

Anonymous `initialize` and `tools/list` are supported, so directories and health checks can verify the server without an account. Tool calls require authentication.

## Access

API & MCP access is available on Framesail's Pro and BYOK plans — see [pricing](https://framesail.com/pricing). With BYOK, jobs covered by your own provider keys (OpenAI, Gemini, Anthropic, fal, ElevenLabs, MiniMax) bill zero platform credits.

## Support

- [support@framesail.com](mailto:support@framesail.com)
- [Discord](https://discord.gg/jaWgxfhHbZ)
