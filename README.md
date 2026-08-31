# synpkg

One package manager over four sources: the Arch repositories, the AUR,
BlackArch and Flathub. It searches all of them in a single list, tells you
where each result came from, and installs from whichever one has it.

## Finding and installing

```bash
synpkg search htop                 # the repositories
synpkg search --all image editor   # repos, BlackArch, AUR and Flathub at once
synpkg info firefox
synpkg install neovim              # falls back to the AUR for a name no repo has
synpkg install --no-aur neovim     # …or refuse to build from source
synpkg remove neovim               # with its unneeded dependencies
```

`synpkg provides <name>` answers "what do I install to get a program called
this" — repositories only, so it is fast enough to answer while somebody is
still typing. That is what a launcher asks when a typed name matches nothing
installed.

## Updating

```bash
synpkg upgrade            # refresh the databases and upgrade
synpkg ignore <package>   # hold one back
synpkg held               # what is being held
```

A held package is a third state, distinct from installed and available, so a
hold is visible rather than being an edit in a config file you forget about.

## Notes

Repository operations go through pacman, so nothing here invents its own
database or its own idea of what is installed. It draws its own progress bar
rather than relying on pacman's, because `ILoveCandy` and the rest are
pacman's own configuration and are not read by a front end.

A GUI calling into synpkg must pass `--noconfirm`; without it the process
waits on a prompt nobody can see.

## Install

```bash
git clone https://github.com/velle999/synpkg
cd synpkg && makepkg -si
```

makepkg fetches the source for this PKGBUILD's exact version from this
repository's releases, so a clone can only ever build the source it was
written against. `.SRCINFO` lists what it needs.

## Where this comes from

Developed in [the SynapseOS monorepo](https://github.com/velle999/SYNAPSE),
in `synpkg/`. **This repository is generated from it** — the PKGBUILD, a
generated `.SRCINFO` and this README — so issues and patches belong there.

synpkg 0.1.0-44 · GPL-2.0-or-later
