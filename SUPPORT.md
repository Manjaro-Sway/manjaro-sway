# FAQ

## Install

### How can I unzip the multi-part zip (.zip + .z01)?

If your archive manager doesn't support multipart zips already (p7zip installed), you can just merge the two files using cat:

```bash
cat *.z* >tmp.zip
unzip tmp.zip
```

### How can I restart the installer?

```bash
sudo -E calamares
```

## Shortcuts

### How can I list the predefined shortcuts?

You can reach a quick introduction pressing `Super + Shift + ?`

### How can I (re-)declare shortcuts?

You can add your $bindsym lines to a file in `~/.config/sway/config.d/`:

```bash
$bindsym $mod+Shift+e exec $shutdown
```

to remove existing shortcuts (for example to reuse them elsewhere) you can `$unbindsym` them:

```bash
$unbindsym $mod+w
```

## Upgrades

### how do I upgrade the ~/.config after an update?

After upgrading packages, you will sometimes need to update your skeleton: `skel`

This has the potential to override your customizations (even though we try to not do that). You will find a backup as `~/.config-backup-xxx` in case you messed it up!

### how do I upgrade the greeter configuration?

```bash
sudo curl -s https://raw.githubusercontent.com/Manjaro-Sway/iso-profiles/sway/community/sway/desktop-overlay/etc/greetd/config.toml -o /etc/greetd/config.toml
```

### Why are pacman downloads so slow?

You can add fasttrack mirrors using this command:

```bash
sudo pacman-mirrors --geoip && sudo pacman -Syyu
```

### Why are your packages not in the regular Manjaro Repositories?

Submissions to the Manjaro Repositories are partly manual and thus hard to align with our release process. On the contrary, we try to remove our packages from the official package sources again.

### Can I switch Manjaro lifecycle branches?

Switching between Manjaro lifecycle branches is easy:

```bash
sudo pacman-mirrors --api --set-branch {branch}
sudo manjaro-sway-mirrors
sudo pacman -Syyu
```

### How can I track updates?

Major changes specific to this flavor of manjaro are mostly being done in the [desktop-settings repo](https://github.com/Manjaro-Sway/desktop-settings).

### I installed the minimal version, can I install all the extras afterwards?

Sure, just run this:

```bash
curl -s https://raw.githubusercontent.com/Manjaro-Sway/iso-profiles/sway/community/sway/Packages-Desktop | grep -oP '(?<=>extra )[^ ]*' | sudo pacman -S --noconfirm -
```

## Customizing

### How can I customize sway without losing my customizations after an upgrade?

You can add variable overrides in `~/.config/sway/definitions.d/` and add more sway configuration inside `~/.config/sway/config.d/`. please refer to the [arch wiki](https://wiki.archlinux.org/title/Sway) and the [sway wiki](https://github.com/swaywm/sway/wiki) for lots of ideas and hints. Make sure the files in either location end in .conf for them to be loaded.

### How can I create my own color theme?

Best you start off with a copy of the current theme.

```bash
cp /usr/share/sway/themes/matcha-green/definitions ~/.config/sway/definitions.d/theme.conf
```

Do your customizations in `~/.config/sway/definitiond.d/theme.conf`.

### How can I customize waybar without losing my customization after an upgrade?

Copy over and edit the customization template, it will get picked up automatically:

```bash
cp ~/.config/waybar/config.jsonc.example ~/.config/waybar/config.jsonc
```

### How can I customize the foot terminal without losing my customization after an upgrade?

Copy over and edit the customization template, it will get picked up automatically:

```bash
cp ~/.config/foot/foot.ini.example ~/.config/foot/foot.ini
```

### How can I add my own and override existing sworkstyle icons?

Copy over and edit the customization template, it will get picked up automatically:

```bash
cp ~/.config/sworkstyle/config.toml.example ~/.config/sworkstyle/config.toml
```

You can find missing icons in the sworkstyle logs, `/tmp/sworkstyle.log`.

## Setup and configuration

### How can I move the waybar from top to bottom?

Change the waybar position by creating or updating your `~/.config/waybar/config.jsonc`:

```jsonc
{
    "include": [
        "/usr/share/sway/templates/waybar/config.jsonc"
    ],
    "position": "bottom"
}
```

### How can I log in inside a virtual machine?

While it seems to work out of the box in some kvm/qemu/libvirt environments, you need to enable 3D acceleration at least in VirtualBox and Gnome Boxes.

### How can I use the amazing mps-youtube?

[set your own api key in mps-youtube](https://github.com/mps-youtube/mps-youtube/wiki/Troubleshooting#youtube-error-403-the-request-cannot-be-completed-because-you-have-exceeded-your-quota)

### How do I get an active bluetooth after login?

Refer to this [link](https://wiki.archlinux.org/title/Bluetooth#Auto_power-on_after_boot)

### How can I add more keyboard layouts to sway?

Copy over our configuration example:

```bash
cp ~/.config/sway/config.d/XX-keyboard.conf.example ~/.config/sway/config.d/01-keyboard.conf
```

refer to `man sway-input` and the [arch wiki](https://wiki.archlinux.org/title/Sway#Keymap) for more pointers.

### Why doesn't it start with nvidia drivers?

Likely you're using proprietary drivers, unsupported by sway. You can try it anyway by pressing `F3` in the greeter and selecting `Sway (unsupported GPU)`.

### How can I configure another path for the screenshots to be saved?

By default screenshots are being stored in `$HOME/Screenshots`. If you'd like to change that, just add/change a line `XDG_SCREENSHOTS_DIR="$HOME/Screenshots"` in `~/.config/user-dirs.dirs`.

### How do I disable the window focus flashing animation?

add this to `.config/sway/definitions.d/autostart.conf`:

```
set $flashfocus ""
```

### How can I configure adaptive brightness?

Install wluma:

```sh
pacman -S wluma
```

It may work out of the box. If it doesn't:

```sh
cp -r /etc/xdg/wluma ~/.config/
```

and [configure](https://github.com/maximbaz/wluma#configuration) `~/.config/wluma/config.toml` according to your needs.

### How can I extend the zsh configuration?

You can add you own zsh configuration to `~/.config/zsh/config.d/`.

### How can I disable the help onscreen menu permanently?

```bash
rm $HOME/.config/nwg-wrapper/help.sh
```

### Why do my auto-login settings from the installer have no effect?

greetd, our login messenger, is not supported by the manjaro installer. refer [here](https://wiki.archlinux.org/title/Greetd#Autologin) for help.

### How can I disable the night light feature?

add this to `.config/sway/definitions.d/autostart.conf`:

```
set $wlsunset ""
```

### How can I set a fixed geo location for the night-light feature?

Update the waybar module by creating or updating your `~/.config/waybar/config.jsonc` with appropriate values for latitude and longitude:

```jsonc
{
    "include": [
        "/usr/share/sway/templates/waybar/config.jsonc"
    ],
    "custom/sunset": {
        "interval": "once",
        "tooltip": false,
        "return-type": "json",
        "format": "{icon}",
        "format-icons": {
            "on": "",
            "off": ""
        },
        "exec": "latitude=50.1 longitude=8.7 /usr/share/sway/scripts/sunset.sh",
        "on-click": "/usr/share/sway/scripts/sunset.sh toggle; pkill -RTMIN+6 waybar",
        "exec-if": "/usr/share/sway/scripts/sunset.sh check",
        "signal": 6
    },
}
```

### How can I disable the dynamic workspace icons?

add this to `.config/sway/definitions.d/autostart.conf`:

```
set $workspace_icons ""
```

### How can I disable the window auto-tiling?

add this to `.config/sway/definitions.d/autostart.conf`:

```
set $autotiling ""
```

### How can I disable the clipboard history?

add this to `.config/sway/definitions.d/autostart.conf`:

```
set $cliphist_watch ""
set $cliphist_store ""
```

### How can I remove an auto-starting application?

Refer to the autostart section of our [definitions](https://github.com/Manjaro-Sway/desktop-settings/blob/b43c6733b2830157a57097216c132891d93c7e4f/community/sway/etc/sway/definitions) to find the variables.

Add an entry to `.config/sway/definitions.d/autostart.conf` for each command you'd like to disable:

```
set $flashfocus ""
```

### How can I delete the clipboard history?

You can middle click on the icon on waybar or run `cliphist wipe` command inside your terminal.

### How can I purge the clipboard history on logout?

add a definition `~/.config/sway/definitions.d/cliphist.conf`:

```
set $purge_cliphist_logout true
```

### How can I follow the windows as I move them?

add a definition `~/.config/sway/definitions.d/window-follow.conf`:

```
set $focus_after_move true
```

### How can I determine the app_id for a running application?

This lists all ids of the opened applications:

```
swaymsg -t subscribe -m '[ "window" ]' | jq -r --unbuffered .container.app_id
```

### How can I assign a window to a specific workspace?

```
assign [class="Emacs"] workspace number 1
```

### How can I enable github notifications?

install and authenticate with the github cli:

```bash
pacman -S github-cli
gh auth login
```

### How can I use w/a/s/d for directional navigation?

create a new file `~/.config/sway/definitions.d/02-directional.conf`

```bash
# unassign the rofi menu from $mod+d
$unbindsym $mod+d
# assign the menu to whatever you like
$bindsym $mod+Shift+d exec $menu

# unassign the window stacking menu from $mod+s
$unbindsym $mod+s
# assign the stacking mode to whatever you like
$bindsym $mod+Shift+s layout stacking

# unassign the window tabbing menu from $mod+s
$unbindsym $mod+w
# assign the tabbing mode to whatever you like
$bindsym $mod+Shift+w layout tabbed

# assign the directional keys
set $left a
set $down s
set $up w
set $right d
```

### How can I change the wallpaper/background image?

Add a config file to definitions e.g. `.config/sway/definitions.d/01-background.conf`:

```
set $background /usr/share/backgrounds/whatever/file/you/like.png
```

### How can I take a Screenshot?

Press the `Print` button on your keyboard and you will be presented with some options on the waybar. Depending on what you would like to take a screenshot of, you have to press a combination of keys. To take a full screenshot of the current screen just press - `Shift + o` on your keyboard.

### I get weird screen distortions (with an intel iGPU)

Try to disable Panel Self Refresh (PSR), a power saving feature used by Intel iGPUs.
A temporary solution is to disable this feature using the [kernel parameter](https://wiki.archlinux.org/title/Kernel_parameters) i915.enable_psr=0.

### How do I enable numlock on startup?

Check the identifier for your keyboard:

```bash
swaymsg -t get_inputs | jq -r '.[].identifier' | grep -i keyboard
```

Add the following in your sway config:

```
input "1:1:AT_Translated_Set_2_keyboard" xkb_numlock enabled
```

### How do I enable `ssh-agent` on startup?

1. Enable the `gcr-ssh-agent.socket` systemd user unit:

   ```bash
   systemctl --user enable gcr-ssh-agent.socket
   ```
2. Set `SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/gcr/ssh"` in your environment, for example by adding

   ```bash
   export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/gcr/ssh"
   ```

   to a file in `$HOME/.config/profile.d`

See [the Arch Wiki](https://wiki.archlinux.org/title/GNOME/Keyring#gcr-ssh-agent) for more information.
