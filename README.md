<p align="center">
  <img src="./assets/logo.svg" width="200" alt="AI Skills — code brackets in a badge with skill nodes" />
</p>

<h1 align="center">✨ AI Skills Collection</h1>

<p align="center">
  <a href="https://github.com/alexander-danilenko/ai-skills/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" />
  </a>
</p>

> 🚀 Personal skills library for AI coding assistants (Claude Code, Cursor, Codex, OpenCode, GitHub Copilot)

## 📦 Installation

Install all skills:

```bash
npx skills add alexander-danilenko/ai-skills --skill '*'
```

Install a single skill:

```bash
npx skills add alexander-danilenko/ai-skills --skill agents-md-pro
```

To view the list of available skills, run:

```bash
npx skills add alexander-danilenko/ai-skills --list
```

## 🌟 Contrib Skills

Skills from other repos I use daily:

```bash
ARGUMENTS=(--agent claude-code --global) && \
npx skills add anthropics/skills --skill skill-creator "${ARGUMENTS[@]}" && \
npx skills add Jeffallan/claude-skills --skill '*' "${ARGUMENTS[@]}"
```

## 🤝 Contributing

These are personal skills for my workflow. Feel free to fork and adapt for your own use.

When adding or updating skills, use [Anthropic's skill-creator skill](https://github.com/anthropics/skills/tree/main/skills/skill-creator) so new skills match the expected format and conventions.

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
