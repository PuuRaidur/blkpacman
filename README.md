# blkpacman, the BlackArch mirrorlist package manager

## Intro 

This is a BlackArch mirrorlist package manager meant for Arch-based distros to install cybersecurity tools.
Searches official Arch repos -> BlackArch repo -> disables BlackArch repo in `/etc/pacman.conf` by default.

## Why?

BlackArch mirrorlist replaces core system packages like `glibc`, `openssl`, `linux` etc. if left enabled during `sudo pacman -Syu` which may cause your system to break (nuking). Unless needed, `blkpacman` keeps the repo disabled.

## Setup

### First, add the BlackArch repo to `/etc/pacman.conf`:

1. `curl -O https://blackarch.org/strap.sh`

2. `chmod +x strap.sh`

3. `sudo ./strap.sh`

Now the BlackArch repo is in `pacman.conf`:

```bash
[blackarch]
Include = /etc/pacman.d/blackarch-mirrorlist
```

### Second, make `blkpacman` a global script:

1. `git clone https://github.com/PuuRaidur/blkpacman.git`

2. `cd blkpacman`

3. `cp ./blkpacman ~/.local/bin/`

4. `chmod +x ~/.local/bin/blkpacman`

Note that `~/.local/bin/` has to be in your `PATH`. If it isn't:

1. `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.$(basename $SHELL)rc`
(auto-detects bash/zsh)

2. `source ~/.$(basename $SHELL)rc`

## Usage

`blkpacman <pkg...>`: Mixed install -> official + BlackArch repo

`blkpacman -s <term>`: Search for packages in BlackArch repo

`blkpacman -i <pkg>`: Show info about a BlackArch package

`blkpacman -l`: List all BlackArch categories

`blkpacman -c <name>`: Install all tools in a provided BlackArch category

`blkpacman -b <pkg...>`: Install a package from BlackArch repo explicitly

`blkpacman -m`: Update BlackArch mirrorlist

`blkpacman -u`: Upgrade installed BlackArch packages

`blkpacman -S`: Show whether BlackArch repo is enabled/disabled

`blkpacman -h`: Show usage guide