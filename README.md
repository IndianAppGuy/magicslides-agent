# MagicSlides for AI agents

Your agent writes the content. [MagicSlides](https://www.magicslides.app/?ref=github-agent) turns it into a designed
presentation and gives back a **Present link, a PPTX, a PDF and an editor link**. You can pick from 161 templates.

It works in Claude Code, Codex, Cursor, Gemini CLI, OpenClaw, Hermes and any agent that reads
[Agent Skills](https://agentskills.io) or speaks MCP.

![A real deck made by an agent with this skill](assets/demo-deck.gif)

*The deck above is real. One `create_presentation_from_slots` call built it in 18 seconds, with no edits. It's also in
[PPTX](https://www.magicslides.app/s/2175dd89-54bc-420a-9b07-88239f7f8098/pptx) and
[PDF](https://www.magicslides.app/s/2175dd89-54bc-420a-9b07-88239f7f8098/pdf).*

## Install

Get a free API key first: **https://www.magicslides.app/dashboard/settings/api?ref=github-agent**. Agents that sign in over MCP
with OAuth don't need one.

| Agent | Install |
|---|---|
| **Any agent** ([skills.sh](https://skills.sh)) | `npx skills add IndianAppGuy/magicslides-agent` |
| **Claude Code** | `/plugin marketplace add IndianAppGuy/magicslides-agent` then `/plugin install magicslides@magicslides` |
| **Codex** | `npx skills add IndianAppGuy/magicslides-agent -a codex` · MCP: `codex mcp add magicslides --url https://www.magicslides.app/api/mcp/mcp` then `codex mcp login magicslides` |
| **OpenClaw** | `openclaw skills install @theindianappguy/magicslides` (or `clawhub install @theindianappguy/magicslides`) |
| **Hermes Agent** | `hermes skills install IndianAppGuy/magicslides-agent/skills/magicslides` |
| **Gemini CLI** | `gemini extensions install https://github.com/IndianAppGuy/magicslides-agent` |
| **Cursor** | [![Add MagicSlides MCP to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=magicslides&config=eyJ1cmwiOiJodHRwczovL3d3dy5tYWdpY3NsaWRlcy5hcHAvYXBpL21jcC9tY3AifQ==) or `npx skills add IndianAppGuy/magicslides-agent -a cursor` |
| **Claude.ai / ChatGPT / any MCP client** | Remote MCP server `https://www.magicslides.app/api/mcp/mcp` (Streamable HTTP, OAuth) |

Then set your key:

```bash
export MAGICSLIDES_API_KEY=ms-api-...
# Some sandboxes (Codex, for example) hide env vars that contain KEY. Save the key once instead:
node ~/.agents/skills/magicslides/scripts/magicslides.mjs login ms-api-...
```

Now ask your agent: *"Make me a 7-slide pitch deck for my startup."*

## How it works

```
list_templates ──► user picks a design ──► get_template_schema ──► agent writes every slot
      ──► create_presentation_from_slots ──► Present · PPTX · PDF · Edit links
```

- **MCP agents** call the hosted server's tools directly. The Claude Code plugin and the Gemini extension set that up for you.
- **Shell-only agents** use [`skills/magicslides/scripts/magicslides.mjs`](skills/magicslides/scripts/magicslides.mjs).
  It's a zero-dependency Node 18+ script that calls the same server with your API key:

```bash
node scripts/magicslides.mjs whoami
node scripts/magicslides.mjs list_templates '{"topic":"seed pitch"}'
node scripts/magicslides.mjs get_template_schema '{"templateKey":"editorial-pitch","slides":5}'
node scripts/magicslides.mjs create_presentation_from_slots @deck.json
```

| Tool | What it does |
|---|---|
| `list_templates`, `get_template_schema` | Browse the 161 designs and get the slots to fill |
| `create_presentation_from_slots` | Build a deck from copy you wrote, at no AI cost |
| `create_presentation` | MagicSlides writes the copy from a topic |
| `get_presentation`, `update_presentation` | Edit a deck in place |
| `create_doc`, `create_sheet`, `create_meeting_notes` | Docs, spreadsheets and meeting notes |
| `list_frame_templates`, `create_frames`, `create_custom_frame` | Short animated 9:16 reels |

The full agent instructions are in [`skills/magicslides/SKILL.md`](skills/magicslides/SKILL.md).

## Repo layout

```
skills/magicslides/SKILL.md          the skill (Agent Skills standard), shared by every ecosystem
skills/magicslides/scripts/          zero-dependency API helper
.claude-plugin/ + .mcp.json          Claude Code plugin + marketplace
plugin.json + mcp.json               Agent Plugins standard (Codex, ChatGPT, Cursor)
gemini-extension.json + GEMINI.md    Gemini CLI extension
proof/                               transcripts of real end-to-end runs
```

## Links

[Website](https://www.magicslides.app/?ref=github-agent) ·
[MCP docs](https://www.magicslides.app/mcp?ref=github-agent) ·
[Pricing](https://www.magicslides.app/pricing?ref=github-agent) ·
[Privacy](https://www.magicslides.app/privacy-policy) ·
[Terms](https://www.magicslides.app/terms-of-use) ·
Support: support@magicslides.app

MIT licensed.
