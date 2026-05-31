# blkpacman, the BlackArch repo package manager

## Intro 

This is a BlackArch repo package manager meant for Arch-based distros to install cybersecurity tools.
Searches official Arch repos -> BlackArch repo -> disables BlackArch repo in `/etc/pacman.conf`

## Why?

BlackArch repo replaces core system packages like `glibc`, `openssl`, `linux` etc. if left enabled during `sudo pacman -Syu`, breaking your system. Unless needed, `blkpacman` keeps the repo disabled.

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

`blkpacman [package...]`: Install package(s) by searching official repos first, then BlackArch one

`blkpacman -e`: Enable BlackArch repo permanently

`blkpacman -d`: Disable BlackArch repo permanently

`blkpacman -t`: Toggle BlackArch repo on/off

`blkpacman -s`: Show whether BlackArch repo is enabled/disabled

`blkpacman -S [package...]`: Search BlackArch repo for specific package(s)

`blkpacman -h`: Show help