# Per-Monitor Background

Give each monitor its own background in Omarchy, using the background picker you already know.

![Two monitors with different backgrounds: a daytime launch on the portrait monitor, a sunset launch on the landscape monitor](preview.jpg)

Double-click the desktop on any monitor and pick an image. Only that monitor changes. There's no bar widget or config file to learn. If windows cover the desktop, the background picker hotkey can do the same for the focused monitor (see below).

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

### From the keyboard or the Omarchy menu

When windows cover the desktop, you can open the picker for the focused monitor instead:

```bash
omarchy-shell background pickFocused        # the focused monitor
omarchy-shell background pick DP-2          # a named monitor
```

Out of the box, Omarchy's background picker hotkey (SUPER + CTRL + SPACE) and **Menu → Style → Background** still change the shared background on every monitor, which clears per-monitor picks. To make both per-monitor, add this line inside the braces of `~/.config/omarchy/extensions/omarchy-menu.jsonc`:

```jsonc
"style.background": {"icon":"","label":"Background","aliases":["background","wallpaper"],"action":"omarchy-shell background pickFocused"},
```

The hotkey opens that same menu item, so this one line covers both. Keep the icon, label and aliases: Omarchy 4.0.4 resets any field an override leaves out. Without the `background` alias, the hotkey opens the main menu instead of the picker. The plugin never edits your config for you. To undo it, delete the line.

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

To also forget saved picks, delete `~/.local/state/omarchy/background-monitors.json`. If you added the `style.background` line to `omarchy-menu.jsonc`, remove it too.

## Notes

- This replaces Omarchy's background plugin with a modified copy of it. It won't pick up upstream fixes to that plugin until it's updated here.
- Changes to the plugin's code take effect after `omarchy restart shell`.
- Looking for more control? [Backdrop](https://github.com/lgse/backdrop) adds a bar panel with files, colors and gradients per display. [Wallpaper Per Monitor](https://github.com/vitorcanoas/omarchy-wallpaper-per-monitor) handles portrait and landscape defaults for rotated displays.

## License

MIT. Based on Omarchy's `omarchy.background` plugin, © David Heinemeier Hansson, also MIT. See [LICENSE](LICENSE).

The preview shows backgrounds from the [Liftoff theme](https://github.com/tcballard/omarchy-theme-liftoff). Its launch photograph is credited to SpaceX; see that theme's [CREDITS.md](https://github.com/tcballard/omarchy-theme-liftoff/blob/main/CREDITS.md). The plugin's MIT license doesn't cover the preview image.
