# Hyprland

Hyperland is different than other Linux desktops like KDE or GNOME. 
It is highly customizable via text and uses tiling windows instead of floating windows used for Windows and MacOS.
Everything can be changed and personalized like taskbar, terminal.
This makes it Incredibly clean and simple looking while still staying functional.

> You get a blank canvas that you can form how you want by using text

## Why use Hyprland?

- Fluid Animations - Know for extremely smooth animations 
- Efficiency - Keyboard driven workflow
- Wayland native - Built for Wayland -> better performance, security than older X11
- Modern Customization - Things like blur, round edges
- Massive community - Many pre-made designs (`dotfiles`)

## Tiling vs Floating

Like mentioned at the top Hyprland uses `Window Tiling` while Windows and MacOS use `Floating Windows`

How is `tiling` different:
- No overlapping
- Windows scale automatically
- Organizes you screen in a so called `Master-stack Layout`

## Key Components

| *Component*              | *Purpose*                                               | *Popular Examples*            |
|------------------------|-------------------------------------------------------|-----------------------------------|
| **Status Bar**         | Displays clock, battery, Wi-Fi, and active workspaces | `waybar`                          |
| **App Launcher**       | Search and launch applications                        | `rofi-wayland`, `wofi`, `fuzzel`  |
| **Notification Daemon**| Handles system and application notifications          | `mako`, `dunst`                   |
| **Wallpaper**          | Sets and manages the desktop background               | `hyprpaper`, `swww`               |
| **Terminal**           | Fast, GPU-accelerated terminal emulator               | `foot`, `kitty`, `alacritty`      |

## Configuration

Here is where Hyprland shines.
Everything is configured inside a single plain text file usually located at: `~/.config/hypr/hyprland.conf`

Changes take effect instantly after saving the file. No need to reboot or restart anything.

The configuration files is divided into a few categories:

- Monitor: Resolution, refresh rate
- Input: Keyboard layouts, mouse sensitivity
- General: Border sizes, active colors, gaps
- Decoration: Opacity, active blur
- Animations: Fine-tuning the speed and curves
- Binds: Setting up keyboard shortcuts

## Important Concepts

### Keybinds

Since Hyprland relies heavily on keyboard inputs, key binds are essential and the core of your workflow.
They use a specific syntax: `bind = MODIFIER, KEY, ACTION, ARGUMENTS`

```bash
# Example binds inside hyprland.conf
bind = SUPER, Q, exec, foot        # Opens the terminal "foot"
bind = SUPER, C, killactive,       # Closes the currently active window
bind = SUPER, M, exit,             # Exits Hyprland completely
bind = SUPER, E, togglefloating,   # Switches a window from tiling to floating mode
```

### Window Rules

You can force specific applications to always behave a certain way. For example, you can make your media player always open floating

```bash
# Example window rules
windowrulev2 = float, class:(vlc)
```