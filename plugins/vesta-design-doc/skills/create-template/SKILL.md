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
- **Other platform**: use that platform's skill or connector if one is available; otherwise copy it locally and tell the user.

Reply with the path or link.
