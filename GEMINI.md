# MagicSlides

When the user asks for a presentation, ppt, pptx, slides, deck or pitch deck, or to turn a
document/PDF/article into slides, use the `magicslides` MCP tools and follow the workflow in
`skills/magicslides/SKILL.md`: `list_templates` → user picks → `get_template_schema` →
fill every slot → `create_presentation_from_slots` (or `create_presentation` for templates
that aren't bring-your-own) → reply with the Present, PPTX, PDF and Edit links verbatim.

If the tools return an auth error, tell the user to get a free key at
https://www.magicslides.app/dashboard/settings/api?ref=gemini-cli and run
`gemini extensions config magicslides`, or run `/mcp auth magicslides` to sign in.
