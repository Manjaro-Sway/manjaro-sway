# manjaro sway edition
[![repo_build](https://github.com/boredland/arch-repo/workflows/repo_build/badge.svg)](https://github.com/boredland/arch-repo/actions)
[![iso_build](https://github.com/boredland/manjaro-sway/workflows/iso_build/badge.svg?event=repository_dispatch)](https://github.com/boredland/manjaro-sway/actions)

## description

i recently saw, that there was a decent manjaro sway distribution for arm. this is my approach to port a lot from those configurations to a regular manjaro sway built, with some smaller and bigger changes:

- trying to use a decent cli solution whenever available
- pre-package some tools for software development
- automate stuff where feasible

## where can I download an iso?

images are build and uploaded in a relatively regular interval to [github releases](https://github.com/boredland/manjaro-sway/releases)

there will be two different isos:

- full: containing everything from [manjaro sway settings](https://github.com/boredland/arch-repo/blob/master/custom/manjaro-sway-settings-git/PKGBUILD) and the [iso overlay](https://github.com/boredland/manjaro-iso-profiles/blob/main/community/sway/Packages-Desktop)
- minimal: same as full - minus the "extra" packages from the [iso overlay](https://github.com/boredland/manjaro-iso-profiles/blob/main/community/sway/Packages-Desktop)

## how to upgrade?

after upgrading packages, you will sometimes need to update you skeleton:

```
cp -rf /etc/skel/.config/* ~/.config
```

keep in mind that this could cause problems with customizations you made. make a backup pls.

## what are the commands?

you can reach a quick introduction pressing `Super + Shift + ?`

## what doesn't work yet?

- blurry fonts in xwayland

Otherwise: [you tell me](https://github.com/boredland/manjaro-sway/issues). I'd be happy to try to even out everything. PRs will be accepted in the repos listed below.

## sources

- [iso profile](https://github.com/boredland/manjaro-iso-profiles/tree/main/community/sway)
- [desktop settings](https://github.com/boredland/manjaro-sway-settings)

## building

1. check out the iso profile
2. `buildiso -p sway`

## screenshots

![desktop](public/_includes/desktop.png?raw=true)
![help menu](public/_includes/help.png?raw=true)
![htop](public/_includes/htop.png?raw=true)
![launcher](public/_includes/launcher.png?raw=true)
![nmtui](public/_includes/nmtui.png?raw=true)
![pamac](public/_includes/pamac.png?raw=true)
![ranger](public/_includes/ranger.png?raw=true)
![qutebrowser](public/_includes/qutebrowser.png?raw=true)
![mako](public/_includes/mako.png?raw=true)

## credentials

```
user: manjaro
password: manjaro
```

## first boot

1. make chromium use native window decorations

![chromium](public/_includes/chromium.png?raw=true)

2. enable [this flag] (chrome://flags/#enable-webrtc-pipewire-capturer)(`chrome://flags/#enable-webrtc-pipewire-capturer`) to allow screensharing in chromium

3. [set your own api key in mps-youtube](https://github.com/mps-youtube/mps-youtube/wiki/Troubleshooting#youtube-error-403-the-request-cannot-be-completed-because-you-have-exceeded-your-quota)

4. fasttrack mirrors: `sudo pacman-mirrors --geoip && sudo pacman -Syyu`

5. auto enable bluetooth on boot: `echo "AutoEnable=true" >> /etc/bluetooth/main.conf`

## credits

- initial inspiration came from the [sway branch in the manjaro iso profiles repo](https://gitlab.manjaro.org/profiles-and-settings/iso-profiles/-/tree/sway)
- most of the work is (with some modifications) copied from the [manjaro sway arm overlay](https://gitlab.manjaro.org/manjaro-arm/applications/arm-profiles/-/tree/master/overlays/sway)
- the background image is [beautifully made by reddit user u/atlas-ark](https://www.reddit.com/r/wallpaper/comments/kmh680/1920x1080_all_resolutions_available_dark_light/?utm_source=share&utm_medium=web2x&context=3)