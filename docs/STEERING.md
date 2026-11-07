# Steering Documentation – Pebble Apps

## Overview

The **Pebble Apps** repository is a central hub for creating, testing, and publishing Pebble smartwatch watchfaces and applications. It combines human‑readable documentation with Claude AI skills to streamline the development workflow.

## Development Environment

- **Pebble SDK** – Required for building watchfaces (C) and apps (JavaScript). Install via the official instructions: https://developer.pebble.com/guides/sdk/ (or the community‑maintained rebble.io mirrors).
- **Node.js** – For JavaScript (Alloy) apps and tooling. Recommended version: 20.x.
- **Git** – Version control. This repo tracks source, docs, and skill files.
- **Claude AI** – Use the skills in `.claude/skills/` via the Claude Code UI or the CLI (`/skill <skill-name>`).

## Watchface Development (C SDK)

1. **Scaffold** – Run the skill `watchface-create` to generate a new watchface skeleton:
   ```bash
   /skill watchface-create <WatchfaceName>
   ```
2. **Core Files** – The scaffold creates:
   - `src/<WatchfaceName>/src/main.c` – entry point.
   - `src/<WatchfaceName>/appinfo.json` – metadata for the Pebble Store.
   - Basic resource folder (`resources/`) for bitmap assets.
3. **Implement** – Edit the generated C source. Common APIs you’ll use (see the **Pebble C SDK API reference**):
   - **Window & Layer**: `window_create()`, `layer_set_update_proc()`, `layer_add_child()`.
   - **Graphics**: `graphics_draw_text()`, `graphics_draw_bitmap()`, `graphics_context_set_fill_color()`.
   - **Time & Events**: `tick_timer_service_subscribe()`, `handle_tick()`, `bluetooth_connection_service_subscribe()`.
   - **Background Worker**: `worker_launch()`, `worker_message_subscribe()`.
   - **Resources**: `resource_get_handle()`, `resource_get_bitmap()` for images and fonts.
   > The full list of functions, types, and constants is documented at the **C SDK** pages [[C SDK Docs]](https://developer.rebble.io/docs/c/).
4. **Build** – Use the Pebble CLI:
   ```bash
   pebble build src/<WatchfaceName>
   ```
5. **Test** – Run the watchface in the Pebble emulator:
   ```bash
   pebble install src/<WatchfaceName>/build/<WatchfaceName>.pbw
   ```
   Use `pebble logs` to view runtime output and debug prints.
6. **Publish** – Follow the Pebble developer portal guidelines (appinfo.json versioning, screenshots, store description).

## App Development (Alloy JavaScript SDK)

Alloy is Pebble’s modern, pure‑JavaScript SDK (built on Moddable). It lets you write watch‑apps with familiar JavaScript idioms and a component‑based UI.

1. **Scaffold** – Run the skill `app-create` which internally calls the Alloy template:
   ```bash
   /skill app-create <AppName>
   ```
   This creates `src/<AppName>/` with an `appinfo.json`, a `src/main.js` entry point, and an `index.html`‑style UI using the **Piu**/`Poco` UI framework.
2. **Core Files** – The scaffold includes:
   - `src/<AppName>/src/main.js` – JavaScript entry point.
   - `src/<AppName>/resources/` – optional assets (images, fonts).
   - `src/<AppName>/appinfo.json` – metadata required for the store and for the SDK.
3. **Implement** – Use the Alloy API to create windows, layers, and handle events. Typical patterns:
   ```javascript
   const UI = require('ui');
   const main = new UI.Window({
     fullscreen: true,
   });
   const text = new UI.Text({
     text: 'Hello Pebble! ',
     font: 'gothic-24-bold',
     color: 'white',
   });
   main.add(text);
   main.show();
   ```
   - **UI Frameworks**: Piu and Poco components (`ui/window`, `ui/text`, `ui/image`).
   - **Sensors**: `Pebble.getAccelerometer()`, `Pebble.getHeartRateMonitor()`.
   - **Networking**: Use `fetch()` (via the Pebble proxy) as described in the **Alloy Networking guide** [[Alloy Networking]](https://developer.rebble.io/guides/alloy/networking/).
   - **Storage**: `localStorage`‑like API (`Pebble.getLocalStorage()`).
4. **Build** – Same Pebble CLI command works for Alloy projects:
   ```bash
   pebble build src/<AppName>
   ```
5. **Test** – Install the generated `.pbw` in the emulator (`pebble install …`). Use `pebble logs` to view console output.
6. **Publish** – Follow the same `appinfo.json` versioning and store submission process as for watchfaces.

## Testing & CI

- **Unit tests** – Add C unit tests under `src/<project>/test/` and run `pebble test`. For Alloy, you can use the Moddable `modtest` framework or Jest for pure‑JS logic.
- **GitHub Actions** – Example workflow (`.github/workflows/build.yml`):
  ```yaml
  name: Build Pebble project
  on: [push, pull_request]

  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - name: Install Pebble SDK
          run: |
            curl -L https://sdk.rebble.io/pebble-sdk.tar.gz | tar xz
            export PATH=$PWD/pebble-sdk/bin:$PATH
        - name: Install Node (Alloy)
          uses: actions/setup-node@v4
          with:
            node-version: "20"
        - name: Build all projects
          run: pebble build src/*
  ```
  This workflow builds every watchface and app on each push, ensuring the generated `.pbw` files compile cleanly.

## Contribution Guidelines

- Follow the [Contributor Covenant Code of Conduct].
- Keep each commit focused and include the attribution line `Co-Authored-By: Claude Code <noreply@anthropic.com>`.
- When adding new watchfaces or apps, update the **Skills Overview** table with any new helper skills you create.

## Skills Overview

| Skill | Description |
|-------|-------------|
| `watchface-create` | Scaffold a new Pebble watchface project (C SDK). |
| `app-create` | Scaffold a new Pebble app project (Alloy JavaScript). |
| `build-all` | Build all watchfaces and apps in the repository. |
| `run-emulator` | Launch the Pebble emulator with a specific binary. |
| `test-all` | Run unit tests for all C watchfaces and Alloy apps. |

Use `/skill <skill-name> --help` for details.

## References

- **Pebble C SDK API reference** – https://developer.rebble.io/docs/c/ (covers `window_*`, `layer_*`, `graphics_*`, tick timer, Bluetooth, resources, etc.)
- **User Interface guide** – https://developer.rebble.io/docs/c/User_Interface/
- **Alloy JavaScript SDK** – https://developer.rebble.io/guides/alloy/ (Getting‑Started, UI components, networking, storage)
- **Alloy Networking guide** – https://developer.rebble.io/guides/alloy/networking/
- **CloudPebble blog (SDK announcement)** – https://repebble.com/blog/cloudpebble-returns-plus-pure-javascript-and-round-2-sdk
- **Zenn tutorial – Developing Pebble Apps with JavaScript** – https://zenn.dev/stc1988/articles/e022df8cc51023?locale=en

---

*Generated with Claude Code* – keep this file up‑to‑date as the project evolves.
