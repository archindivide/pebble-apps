---
name: watchface-create
description: Scaffold a new Pebble watchface project using the Pebble SDK.
---

# Watchface Create Skill

This skill automates the creation of a new Pebble watchface project.

## Usage

```bash
/skill watchface-create <WatchfaceName>
```

- `<WatchfaceName>`: Desired name for the watchface (alphanumeric, no spaces).

## What it does

1. Creates a directory `src/<WatchfaceName>/`.
2. Adds a basic `appinfo.json` and C source files (`src/<WatchfaceName>/src/main.c`).
3. Initializes a `pebble` project with `pebble new <WatchfaceName>`.
4. Commits the new files to the repository (optional).

## Example

```bash
/skill watchface-create MyWatchface
```

After running, you will have a ready‑to‑build watchface in `src/MyWatchface/`.

**Note:** Ensure the Pebble SDK is installed and `pebble` is in your `PATH`.
