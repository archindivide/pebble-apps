---
name: app-create
description: Scaffold a new Pebble app project using the Pebble SDK.
---

# App Create Skill

Automates creating a new Pebble app project.

## Usage

```bash
/skill app-create <AppName>
```

- `<AppName>`: Desired name for the app (alphanumeric, no spaces).

## What it does

1. Creates `src/<AppName>/`.
2. Adds a starter `appinfo.json` and JavaScript entry point (`src/<AppName>/src/main.js`).
3. Runs `pebble new <AppName>` with the appropriate template.
4. Optionally adds a default UI HTML file.

## Example

```bash
/skill app-create MyApp
```

You now have a basic app scaffold ready for development.

**Prerequisite:** Pebble SDK installed and `pebble` CLI in your `PATH`.
