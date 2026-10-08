---
name: create-template
description: Create a blank design doc from the Vesta template — local markdown, Feishu, or another doc platform.
disable-model-invocation: true
---

# Create a design doc from the template

Template: `../../templates/vesta-design-doc-template.md`

Only create the doc from the template. Do not write its content. If the user doesn't say where, ask once.

- **Local markdown**: copy the template file to the given directory. Don't overwrite an existing file.
- **Feishu**: use the `lark-*` skills to create a doc from the template. [agents reference for install lark cli](https://github.com/larksuite/cli#quick-start-ai-agent)
  Feishu has no comment block and mangles `<!-- -->` on import, so first convert every comment in a working copy (never edit the template itself) into a callout, keeping its full text and one `<p>` per line:
  `<callout emoji="💡" background-color="light-gray"><p>…</p></callout>`.
  Escape markdown-special characters in that text. After creating, fetch the doc and check that no `<!--` remains and no guidance text is lost.
- **Other platform**: use that platform's skill or connector if one is available; otherwise copy it locally and tell the user.

Reply with the path or link.
