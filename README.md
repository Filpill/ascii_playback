# ascii_playback

A bash script that plays ASCII animations in the terminal on an infinite loop.

## Usage

```
play_ascii [-q QUALITY] [-f FPS] [-a ANIMATION]
```

### Options

| Flag | Description | Default |
|------|-------------|---------|
| `-q` | Quality tier: `low`, `medium`, `high` | `low` |
| `-f` | Frames per second | `15` |
| `-a` | Play a specific animation by name (e.g. `planet`, `fire`, `wave`) | all animations |
| `-h` | Show help | |

Press `Ctrl+C` to stop.

## Examples

```bash
# Play all animations at default quality and FPS
play_ascii

# Play only the fire animation at high quality, 24 FPS
play_ascii -a fire -q high -f 24

# Play all animations at medium quality
play_ascii -q medium
```

## Features

- **Infinite loop** — cycles through all available animations continuously, or loops a single animation if `-a` is specified.
- **Auto-zoom** — uses `xdotool` to automatically adjust terminal font size so the frame fits on screen. Zoom is restored when the script exits.
- **Auto-scale & centre** — frames are scaled up to the largest integer factor that fits both axes, then centred in the terminal.
- **Clean exit** — hides the cursor during playback and restores it (along with terminal zoom) on `Ctrl+C`.

## Dependencies

| Tool | Required | Purpose |
|------|----------|---------|
| `bash` | Yes | Script runtime |
| `awk` | Yes | Frame rendering and delay calculation |
| `tput` | Yes | Terminal dimension queries |
| `xdotool` | Optional | Auto-zoom via `Ctrl+−` / `Ctrl+=` key events |

If `xdotool` is not available, auto-zoom is silently skipped and the frame is rendered at whatever size the current terminal allows.

## Animations

Frames are stored under `animations/<name>/<quality>/frame_NNNNN.txt`.

| Animation | Qualities |
|-----------|-----------|
| cat | low, medium, high |
| coin | low, medium, high |
| computer | low, medium, high |
| cube | low, medium, high |
| cube-wave | high |
| fire | low, medium, high |
| fire-2 | low, medium, high |
| grok | low, medium, high |
| hands | low, medium, high |
| mail | low, medium, high |
| planet | low, medium, high |
| psychedelic-grid | high |
| rocket | low, medium, high |
| topographic-contours | high |
| triforce | high |
| wave | low, medium, high |

> Note: animations that only have a `high` quality tier will be skipped when running with `-q low` or `-q medium`.
