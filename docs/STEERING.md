# Steering Documentation – Pebble Apps

## Overview

The **Pebble Apps** repository is a central hub for creating, testing,
and publishing Pebble smartwatch watchfaces and applications. It combines
human‑readable documentation with Claude AI skills to streamline the
development workflow.

## Development Environment

- **Pebble SDK** – Required for building watchfaces (C) and apps (JavaScript).
  Install via the official instructions: https://developer.pebble.com/guides/sdk/
- **Node.js** – For JavaScript apps and tooling. Recommended version: 20.x.
- **Git** – Version control. This repo tracks source, docs, and skill files.
- **Claude AI** – Use the skills in `.claude/skills/` via the Claude Code UI
  or the CLI (`/skill <skill-name>`).

## Watchface Development Process

1. **Scaffold** – Run the skill `watchface-create` to generate a new watchface
   skeleton:
   ```bash
   /skill watchface-create <WatchfaceName>
   ```
2. **Implement** – Edit the generated C source under `src/<WatchfaceName>/`.
3. **Build** – Use the Pebble CLI:
   ```bash
   pebble build src/<WatchfaceName>
   ```
4. **Test** – Run the watchface in the Pebble emulator:
   ```bash
   pebble install src/<WatchfaceName>/build/<WatchfaceName>.pbw
   ```
5. **Publish** – Follow the Pebble developer portal guidelines.

## App Development Process

1. **Scaffold** – Run the skill `app-create`:
   ```bash
   /skill app-create <AppName>
   ```
2. **Code** – Implement JavaScript/HTML in `src/<AppName>/`.
3. **Build** – Use the Pebble CLI:
   ```bash
   pebble build src/<AppName>
   ```
4. **Test** – Install in the emulator as above.

## Testing & CI

- **Unit tests** – Add C tests under `src/<project>/test/` and run
  `pebble test`.
- **CI** – Optionally configure GitHub Actions (see `.github/` folder) to
  automatically build on push.

## Contribution Guidelines

- Follow the [Contributor Covenant Code of Conduct].
- Keep each commit focused and include the attribution line
  `Co-Authored-By: Claude Code <noreply@anthropic.com>`.

## Skills Overview

| Skill | Description |
|-------|-------------|
| `watchface-create` | Scaffold a new Pebble watchface project. |
| `app-create` | Scaffold a new Pebble app project. |
| `build-all` | Build all watchfaces and apps in the repository. |
| `run-emulator` | Launch the Pebble emulator with a specific binary. |

Use `/skill <skill-name> --help` for details.

---

*Generated with Claude Code* – keep this file up‑to‑date as the project evolves.
