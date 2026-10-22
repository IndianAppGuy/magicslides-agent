# Codex end-to-end run (22 Oct 2026)

Installed with `npx skills add <this repo> -a codex` (to `.agents/skills/magicslides`). Apps were disabled so the run had to use the bundled script and the saved API key:

```
codex exec --disable apps -s workspace-write -c sandbox_workspace_write.network_access=true "Make me a 5-slide presentation on 5 habits of great remote engineers. Use the creative-pulse template. Just make it."
```

codex-cli 0.162.1. Codex read `SKILL.md`, then ran:

- `'node .agents/skills/magicslides/scripts/magicslides.mjs tools'`
- `"node .agents/skills/magicslides/scripts/magicslides.mjs get_template_schema '{\"templateKey\":\"creative-pulse\",\"slides\":5}'"`
- `'node .agents/skills/magicslides/scripts/magicslides.mjs create_presentation_from_slots @output/remote-engineers.json'`

## Final answer

Created **5 Habits of Great Remote Engineers** — five slides using **creative-pulse**.

[Present](https://www.magicslides.app/s/f80af071-f323-46b4-a0f6-0ca2d68c3dfe/present) · [Download PPTX](https://www.magicslides.app/s/f80af071-f323-46b4-a0f6-0ca2d68c3dfe/pptx) · [Download PDF](https://www.magicslides.app/s/f80af071-f323-46b4-a0f6-0ca2d68c3dfe/pdf) · [Edit in MagicSlides](https://www.magicslides.app/ai-slide?mode=studio&conv=f80af071-f323-46b4-a0f6-0ca2d68c3dfe)

Note: Codex strips env vars whose names contain `KEY` from shell commands, so the first run reported the key as missing. That's why `magicslides.mjs login` exists. It saves the key to `~/.config/magicslides/api-key`.
