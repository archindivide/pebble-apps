# Pebble Apps

Welcome to the **Pebble Apps** repository. This collection provides the
documentation, tooling, and Claude skills needed to develop watchfaces and
applications for the Pebble smartwatch platform.

## Repository layout

- `docs/` – Project steering documentation, guidelines, and workflows.
- `.claude/skills/` – Claude skills that automate common development tasks.
- `src/` – (optional) Sample source code for watchfaces and apps.
- `scripts/` – Build and helper scripts.

## Getting started

1. Install the Pebble SDK: https://developer.pebble.com/guides/sdk/
2. Clone the repo (already done):
   ```bash
   git clone https://github.com/archindivide/pebble-apps.git
   cd pebble-apps
   ```
3. Use the provided Claude skills, e.g.:
   ```bash
   # Create a new watchface project named MyWatchface
   /skill watchface-create MyWatchface
   ```

For more details, see the steering documentation in `docs/STEERING.md`.

Happy hacking! :watch:
