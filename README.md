# HOW-TO setup a GBA dev environment on an Arch-based GNU/Linux (2022/08)

# Prerequisites

- a keyboard

# Base dev packages (make, etc..)

    sudo pacman -S base-devel

# devkitPro

## Add keyring to pacman

    sudo pacman-key --recv BC26F752D25B92CE272E0F44F7FD5492264BB9D0 --keyserver keyserver.ubuntu.com

    sudo pacman-key --lsign BC26F752D25B92CE272E0F44F7FD5492264BB9D0

    wget https://pkg.devkitpro.org/devkitpro-keyring.pkg.tar.xz

    sudo pacman -U devkitpro-keyring.pkg.tar.xz

## Add servers to /etc/pacman.conf (at the end)

    [dkp-libs]
    Server = https://pkg.devkitpro.org/packages

    [dkp-linux]
    Server = https://pkg.devkitpro.org/packages/linux/$arch/

## Resync pacman's DB

    sudo pacman -Syu

## Install the GBA dev packages

    sudo pacman -S gba-dev

## Add env exports to your favourite shell profile

I use ZSH (default on Manjaro KDE), so at the bottom of `~/.zshrc`, add :

    export DEVKITPRO=/opt/devkitpro
    export DEVKITARM=/opt/devkitpro/devkitARM
    export DEVKITPPC=/opt/devkitpro/devkitPPC

Should be the same with other interpreters

Run `source` to immediately apply changes to your local term:

    source ~/.zshrc

# Emulator, AUR + GDB dependencies

    sudo pacman -S mgba-qt yay python2
    yay -S ncurses5-compat-libs

# Visual Code

    yay -S visual-studio-code-bin

## Useful extensions

- C/C++ Extension Pack
- Arm Assembly
- *THEME*: Obsidian Dark

# Optional

I like to change some permissions on the `examples` folder (make it read/writable for `other`, ie: you):

    cd /opt/devkitpro
    sudo chmod -R o+rw examples/

# PRESTO!