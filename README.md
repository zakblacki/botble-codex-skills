# Botble Codex Skills

Reusable Codex skills for current Botble CMS development: plugins, themes, ecommerce, translations, APIs, seeders, testing, and code review.

The rules are aligned with the [Botble AI Assistant Guide](https://docs.botble.com/cms/ai-assistant-guide.html) and its Laravel 13+, PHP 8.3+, and Vite-based architecture.

## Available Skills

- `botble-code-review`
- `botble-conventions`
- `botble-database-seeders`
- `botble-ecommerce`
- `botble-plugin-development`
- `botble-rest-api`
- `botble-testing`
- `botble-theme-development`
- `botble-translations`

## Install with skills.sh

List the skills detected in this repository:

```bash
npx skills add https://github.com/zakblacki/botble-codex-skills --list
```

Install one skill globally for Codex:

```bash
npx skills add zakblacki/botble-codex-skills --skill botble-conventions --global --agent codex
```

Install all nine skills globally for Codex without prompts:

```bash
npx skills add zakblacki/botble-codex-skills --skill '*' --global --agent codex --yes
```

Global skills are available across projects. Depending on the CLI version and sharing mode, canonical copies may appear under `~/.agents/skills/` while being registered for Codex. Verify the effective Codex inventory with `npx skills ls --global --agent codex`. Restart Codex if the new skills do not appear immediately.

To install from a local clone before pushing it:

```bash
npx skills add . --skill '*' --global --agent codex --yes
```

### Important: `config.toml`

Do not point a `[[skills.config]]` entry at this repository's `README.md`. A skill is a directory containing `SKILL.md`, and global Codex installation already makes these skills discoverable. No `config.toml` entry is required for the installation commands above.

## Manual Install

Copy any skill folder from `skills/` into your Codex skills directory.

Windows:

```text
C:\Users\<you>\.codex\skills\
```

macOS/Linux:

```text
~/.codex/skills/
```

Install every skill manually on macOS/Linux:

```bash
mkdir -p ~/.codex/skills
cp -R skills/botble-* ~/.codex/skills/
```

Restart Codex after installing manually.

## ChatGPT Personal Skills

Codex filesystem skills and ChatGPT Personal Skills do not sync automatically. To use these in ChatGPT web or mobile, upload each skill folder separately from **Plugins > Skills > Create > Upload from computer**, subject to your plan and workspace permissions.

## Updating

Refresh skills installed through the CLI:

```bash
npx skills update --global
```

## Sources

- [Botble AI Assistant Guide](https://docs.botble.com/cms/ai-assistant-guide.html)
- [Botble Vite asset compilation](https://docs.botble.com/cms/asset-compilation.html)
- [skills CLI](https://github.com/vercel-labs/skills)
- [OpenAI: Skills in ChatGPT](https://help.openai.com/en/articles/20001066)
