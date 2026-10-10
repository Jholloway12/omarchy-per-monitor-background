# Per-Monitor Background

Give each monitor its own background in Omarchy, using the background picker you already know.

Double-click the desktop on any monitor and pick an image. Only that monitor changes. There's no bar widget, hotkey or config file to learn.

This is a small change to Omarchy's built-in background plugin (`omarchy.background`), which it replaces. Everything else works the same, including the theme switch animation and right-button double-click for the theme switcher.

## Requirements

- Omarchy 4 (Quattro) with its Quickshell-based shell.
- No external dependencies.

## Install

```bash
omarchy plugin add https://github.com/Jholloway12/omarchy-per-monitor-background --enable
omarchy restart shell
```

Enabling it turns off the built-in `omarchy.background` automatically. A shell restart makes sure the new background service is the one running.

## Use

- **Double-click** the desktop on a monitor. The usual background picker opens with the current theme's images.
- **Pick an image.** It's applied to the monitor you double-clicked, and the other monitors keep theirs.
- **Right-button double-click** still opens the theme switcher.

### How picks are kept

- Picks are saved in `~/.local/state/omarchy/background-monitors.json`, keyed by monitor name (as listed by `hyprctl monitors`), so they survive restarts.
- Any change to the shared background clears all picks and puts every monitor back on it. That includes switching themes, `omarchy theme bg next` and `omarchy theme bg set`. This keeps one theme's image from staying on screen under another theme.
- The lock screen keeps using the shared background.

## Remove

```bash
omarchy plugin remove io.github.jholloway12.per-monitor-background
omarchy plugin enable omarchy.background
omarchy restart shell
```

To also forget saved picks, delete `~/.local/state/omarchy/background-monitors.json`.

## Notes

- This replaces Omarchy's background plugin with a modified copy of it. It won't pick up upstream fixes to that plugin until it's updated here.
- Changes to the plugin's code take effect after `omarchy restart shell`.
- Looking for more control? [Backdrop](https://github.com/lgse/backdrop) adds a bar panel with files, colors and gradients per display. [Wallpaper Per Monitor](https://github.com/vitorcanoas/omarchy-wallpaper-per-monitor) handles portrait and landscape defaults for rotated displays.

## License

MIT. Based on Omarchy's `omarchy.background` plugin, © David Heinemeier Hansson, also MIT. See [LICENSE](LICENSE).
