# Botble Codex Skills

Codex skills for Botble CMS development: plugins, themes, ecommerce, translations, APIs, seeders, testing, and code review.

Source: https://botble.com/how-to-build-claude-code-skills-for-botble-cms-development

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

Install one skill by name:

```bash
npx skills add https://github.com/zakblacki/botble-codex-skills --skill botble-conventions
```

Install the plugin development skill:

```bash
npx skills add https://github.com/zakblacki/botble-codex-skills --skill botble-plugin-development
```

The `skills` CLI currently does not install all skills with `--skill '*'`. Install all skills by running one command per skill.

### Install All Skills on Windows PowerShell

```powershell
$skills = @(
    'botble-code-review',
    'botble-conventions',
    'botble-database-seeders',
    'botble-ecommerce',
    'botble-plugin-development',
    'botble-rest-api',
    'botble-testing',
    'botble-theme-development',
    'botble-translations'
)

foreach ($skill in $skills) {
    npx skills add https://github.com/zakblacki/botble-codex-skills --skill $skill
}
```

### Install All Skills on macOS/Linux

```bash
for skill in \
  botble-code-review \
  botble-conventions \
  botble-database-seeders \
  botble-ecommerce \
  botble-plugin-development \
  botble-rest-api \
  botble-testing \
  botble-theme-development \
  botble-translations
 do
  npx skills add https://github.com/zakblacki/botble-codex-skills --skill "$skill"
done
```

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

Example:

```bash
cp -R skills/botble-plugin-development ~/.codex/skills/
cp -R skills/botble-conventions ~/.codex/skills/
```

Restart Codex after installing manually.
