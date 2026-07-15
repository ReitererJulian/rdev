# Hyprland

Hyperland is different than other Linux desktops like KDE or GNOME. 
It is highly customizable via text and uses tiling windows instead of floating windows used for Windows and MacOS.
Everything can be changed and personalized like taskbar, terminal.
This makes it Incredibly clean and simple looking while still staying functional.

> You get a blank canvas that you can form just by using text

## Wayland vs X11

Both are `Display-Server-Protocols` which are the base for how programs even draw windows and register inputs (Mouse, Keyboard). 
Without such a protocol graphical interfaces would not exist, just a text based console like `TTY` (`Teletypewirter`)

### X11

`X11` was created 1984 and is older than most current operating systems.
For decades it was the only standard for Linux.

It is build upon a central `X-Server`, which manages everything (Rendering, Input, Compositing...) in different layers.
This architecture is its weakness in the current time and it struggles to keep up with todays security and performance demand. The technology is simply to old to handle modern graphics cards and things like multi monitor setups. 


### Wayland

`Wayland` was developed to **replace** `X11`

Its architecture is much simpler and straight forward. 
It is not built upon layers like `X11` but the compositor (`Hyprland`) **is** the Display-Server itself. 

Using that architecture many problems are fixed:

- `Security` - Programs cant read inputs of other windows
- `Performance` - Less overhead
- `Clean Multi-Monitor handling`

#### Why does X11 still exist?

After all those years it would be time for `X11` to retire. 
But why is it still present?

Many older programs are not written for `Wayland` and therefor cant understand it. 
There are ways to `translate` `X11` for `Wayland` by using packages like `xorg-xwayland`

---

## Why use Hyprland?

- Fluid Animations - Know for extremely smooth animations 
- Efficiency - Keyboard driven workflow
- Wayland native - Built for Wayland -> better performance, security than older X11
- Modern Customization - Things like blur, round edges
- Massive community - Many pre-made designs (`dotfiles`) [Dotfiles Github](https://github.com/topics/hyprland-dotfiles)

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
Everything is configured inside of text file usually located at: `~/.config/hypr/hyprland.conf`

Other config files for things like `hyprpaper` are in different locations 

Changes take effect instantly after saving the file. No need to reboot or restart anything.

The configuration files is divided into a few categories:

- Monitor: Resolution, refresh rate
- Input: Keyboard layouts, mouse sensitivity
- General: Border sizes, active colors, gaps
- Decoration: Opacity, active blur
- Animations: Fine-tuning the speed and curves
- Binds: Setting up keyboard shortcuts

---

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
