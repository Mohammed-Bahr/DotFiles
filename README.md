# 🌌 Niri & Noctalia Configuration

A modern, scrollable tiling Wayland setup powered by **Niri** and the **Noctalia** desktop shell. This configuration delivers an infinite horizontal scrolling workflow with smooth animations, custom shaders, rounded window aesthetics, and comprehensive multimedia controls.

---

## 📑 Table of Contents

- [✨ Key Features](#-key-features)
- [🖥️ Architecture & Shell Integration](#️-architecture--shell-integration)
- [🎨 Visual Styling & Theming](#-visual-styling--theming)
- [🪟 Window & Column Rules](#-window--column-rules)
- [⌨️ Keybindings Reference](#️-keybindings-reference)
  - [Applications & System](#applications--system)
  - [Navigation & Focus](#navigation--focus)
  - [Window & Column Manipulation](#window--column-manipulation)
  - [Workspaces & Monitors](#workspaces--monitors)
  - [Layout Sizing & Modes](#layout-sizing--modes)
  - [Media & Hardware Controls](#media--hardware-controls)
  - [Screenshots & Utilities](#screenshots--utilities)
- [📁 Configuration Structure](#-configuration-structure)

---

## ✨ Key Features

- **Infinite Scrolling Layout**: Windows are arranged in horizontal columns that scroll seamlessly across the screen.
- **Noctalia Desktop Shell**: Native integration with the Noctalia daemon for app launching, status bar, dock, wallpaper cycling, notifications, and lockscreen.
- **Dynamic Overview Mode (`Mod + Space`)**: Zoomed-out workspace overview with backdrop-anchored wallpaper.
- **Inkwell Ripple Custom Shaders**: GLSL custom shader animations for window transitions.
- **Smart Window Management**: Presets for column widths (1/3, 1/2, 2/3), vertical tabbed column display, and column consume/expel operations.
- **Fine-Tuned App Rules**: Optimized rules for MPV (VRR), Firefox Picture-in-Picture, Zoom, WezTerm, and Quickshell widgets.
- **Wayland Desktop Integration**: XDG Desktop Portal support, Bibata cursor theming, and PipeWire / WirePlumber audio controls.

---

## 🖥️ Architecture & Shell Integration

### Autostart Services
* **Noctalia Shell**: Automatically started at login with `noctalia --daemon` to provide the desktop UI shell, status bar, and dock.

### Environment & Theming
* **Portal Integration**: `QT_QPA_PLATFORMTHEME="xdgdesktopportal"`, `GTK_USE_PORTAL="1"`.
* **Cursor**: `MacTahoe` (Size: 24) — with options for `MacTahoe-light`, `nordic_cursors_scalable`, `ArcDusk-cursors`, `Sunset-cursors`, `Adwaita`, and `Bibata-Modern-Ice`.
* **Desktop Identification**: `XDG_CURRENT_DESKTOP="KDE"`, `KDE_SESSION_VERSION="6"`.

### Layer & Overview Rules
* **Backdrop Wallpaper**: The wallpaper layer (`noctalia-wallpaper`) is configured with `place-within-backdrop true` so the desktop background stays visible in Overview mode (`Mod + Space`).
* **Background Blur Suppression**: Selective disablement of blur layers behind panel components to maintain crisp rendering performance.

---

## 🎨 Visual Styling & Theming

* **Gaps**: `20px` spacing between columns and windows.
* **Corner Radius**: `12px` rounded corners with geometry clipping.
* **Focus Ring**: `4px` focus ring with `#A7C1E1` active color and `#505050` inactive color.
* **Drop Shadows**: Custom soft drop shadows (`softness 30`, `spread 5`, offset `y=5`, color `#0007`).
* **Tab Indicators & Colors** (from `noctalia.kdl`):
  * Active Color: `#e6b450` (Gold Accent)
  * Urgent Color: `#d95757`
  * Tab Indicator: `#e6b450` (Active) / `#76530e` (Inactive)
  * Insert Hint: `#e6b45080`

---

## 🪟 Window & Column Rules

| Application | Rule Applied | Reason / Effect |
| :--- | :--- | :--- |
| **MPV** (`^mpv$`) | `variable-refresh-rate true` | Enables on-demand VRR/G-Sync for smooth video playback. |
| **Firefox PiP** (`^Picture-in-Picture$`) | `open-floating true` | Detaches video overlay into a floating window. |
| **Quickshell / Noctalia** | `open-floating true` | Prevents desktop widgets from tiling into workspace columns. |
| **Zoom** (`zoom`) | `open-floating true`, no radius | Ensures floating meeting windows and unclipped context menus. |
| **WezTerm** | `default-column-width {}` | Bypasses initial configure layout bug. |

---

## ⌨️ Keybindings Reference

> **Modifier Key (`Mod`)**: Refers to `Super` (Windows Key).

### Applications & System

| Shortcut | Action |
| :--- | :--- |
| `Mod + D` | Toggle Noctalia App Launcher |
| `Mod + T` | Open Terminal (`alacritty`) |
| `Mod + E` | Open File Manager (`nautilus`) |
| `Mod + Shift + /` | Show Niri Hotkey Overlay Sheet |
| `Super + Alt + L` | Lock Screen (`swaylock`) |
| `Mod + Shift + E` | Quit Niri (with confirmation) |
| `Ctrl + Alt + Delete` | Quit Niri |
| `Mod + Shift + P` | Power Off Monitors |
| `Mod + Escape` | Toggle Keyboard Shortcut Inhibition (for VMs / Remotes) |

### Navigation & Focus

| Shortcut | Action |
| :--- | :--- |
| `Mod + H` / `Mod + Left` | Focus column left |
| `Mod + L` / `Mod + Right` | Focus column right |
| `Mod + J` / `Mod + Down` | Focus window down within column |
| `Mod + K` / `Mod + Up` | Focus window up within column |
| `Mod + Home` / `Mod + End` | Focus first / last column |
| `Mod + Shift + V` | Switch focus between floating and tiling windows |

### Window & Column Manipulation

| Shortcut | Action |
| :--- | :--- |
| `Mod + Q` | Close focused window |
| `Mod + Ctrl + H` / `Left` | Move column left |
| `Mod + Ctrl + L` / `Right` | Move column right |
| `Mod + Ctrl + J` / `Down` | Move window down within column |
| `Mod + Ctrl + K` / `Up` | Move window up within column |
| `Mod + Ctrl + Home` / `End` | Move column to first / last position |
| `Mod + [` / `Mod + ]` | Consume or expel window to/from neighboring column |
| `Mod + ,` | Consume window below focused window |
| `Mod + .` | Expel bottom window out to a new column |

### Workspaces & Monitors

| Shortcut | Action |
| :--- | :--- |
| `Mod + Space` | **Toggle Workspace Overview** |
| `Mod + 1` .. `Mod + 9` | Focus workspace 1 through 9 |
| `Mod + Ctrl + 1` .. `Mod + 9`| Move focused column to workspace 1 through 9 |
| `Mod + U` / `Mod + Page_Down` | Focus workspace down |
| `Mod + I` / `Mod + Page_Up` | Focus workspace up |
| `Mod + Ctrl + U` / `Page_Down` | Move column to workspace down |
| `Mod + Ctrl + I` / `Page_Up` | Move column to workspace up |
| `Mod + Shift + U` / `Page_Down` | Move entire workspace down |
| `Mod + Shift + I` / `Page_Up` | Move entire workspace up |
| `Mod + Mouse Wheel Up/Down` | Scroll workspaces (rate-limited to 150ms) |
| `Mod + Shift + H/J/K/L` | Focus monitor Left / Down / Up / Right |
| `Mod + Shift + Ctrl + H/J/K/L` | Move column to monitor Left / Down / Up / Right |

### Layout Sizing & Modes

| Shortcut | Action |
| :--- | :--- |
| `Mod + R` | Cycle preset column widths (`1/3` ➔ `1/2` ➔ `2/3`) |
| `Mod + Shift + R` | Cycle preset window heights |
| `Mod + Ctrl + R` | Reset window height |
| `Mod + F` | Maximize column |
| `Mod + Shift + F` | Fullscreen window |
| `Mod + M` | Maximize window to screen edges |
| `Mod + Ctrl + F` | Expand column to fill available space |
| `Mod + C` | Center focused column |
| `Mod + Ctrl + C` | Center all visible columns |
| `Mod + -` / `Mod + =` | Adjust column width by `-10%` / `+10%` |
| `Mod + Shift + -` / `+` | Adjust window height by `-10%` / `+10%` |
| `Mod + V` | Toggle floating mode for window |
| `Mod + W` | Toggle vertical tabbed column display |

### Media & Hardware Controls

| Key | Action |
| :--- | :--- |
| `XF86AudioRaiseVolume` | Volume Up (+10%, capped at 100%) via `wpctl` |
| `XF86AudioLowerVolume` | Volume Down (-10%) via `wpctl` |
| `XF86AudioMute` | Toggle Audio Output Mute |
| `XF86AudioMicMute` | Toggle Microphone Mute |
| `XF86AudioPlay` | Media Play / Pause (`playerctl`) |
| `XF86AudioStop` | Media Stop (`playerctl`) |
| `XF86AudioNext` / `Prev` | Media Next / Previous Track |
| `XF86MonBrightnessUp` | Increase Brightness via Noctalia |
| `XF86MonBrightnessDown` | Decrease Brightness via Noctalia |

### Screenshots & Utilities

| Shortcut | Action |
| :--- | :--- |
| `Mod + Shift + S` | Interactive region screenshot (`grim` + `slurp`) copied to clipboard and saved to `~/Pictures/Screenshots` |
| `Print` | Capture screenshot |
| `Ctrl + Print` | Capture active screen |
| `Alt + Print` | Capture active window |
| `Mod + Shift + W` | Cycle to next wallpaper via Noctalia |

---

## 📁 Configuration Structure

```
~/.config/niri/
├── config.kdl     # Main Niri configuration (Layout, Binds, Window Rules, Animations, Layer Rules)
├── noctalia.kdl   # Color palette & accent definitions (Border, Focus Ring, Tab Indicators)
└── README.md      # Feature documentation and keybindings guide
```
