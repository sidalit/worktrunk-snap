<div align="center">

<img src="snap/gui/worktrunk.png" alt="Worktrunk logo" width="128" />

# Worktrunk

**Git worktree management from your terminal**

[![worktrunk](https://snapcraft.io/worktrunk/badge.svg)](https://snapcraft.io/worktrunk)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Worktrunk](https://worktrunk.dev), a Git worktree manager.

</div>

---

## Getting Started

<a href="https://snapcraft.io/worktrunk"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install worktrunk
worktrunk list
```

For automatic directory switching, add the appropriate line to your shell configuration:

```bash
eval "$(worktrunk config shell init bash --cmd worktrunk)"   # ~/.bashrc
eval "$(worktrunk config shell init zsh --cmd worktrunk)"    # ~/.zshrc
worktrunk config shell init fish --cmd worktrunk | source   # ~/.config/fish/config.fish
```

To use the upstream command name, run `sudo snap alias worktrunk wt` and replace `--cmd worktrunk` with `--cmd wt` above.

## Configure

| Setting | Location or accepted value | Default |
| --- | --- | --- |
| User configuration | `~/snap/worktrunk/common/.config/worktrunk/config.toml` | Upstream defaults |
| Project configuration | `.config/wt.toml` inside each repository | No project hooks |
| `WORKTRUNK_CONFIG_PATH` | Path to an accessible configuration file | User configuration above |
| `WORKTRUNK_WORKTREE_PATH` | Upstream worktree path template | Sibling `<repository>.<branch>` directory |

See [upstream configuration](https://worktrunk.dev/config/) for all application settings. Git is included; configure its identity if it is not already set in the repository:

```bash
worktrunk.git config --global user.name "Your Name"
worktrunk.git config --global user.email "you@example.com"
```

For `/media` or `/mnt`, connect `sudo snap connect worktrunk:removable-media`.

## Limitations

- Hooks and `--execute` run inside the snap. Host-installed AI agents, editors, build tools, `gh` and `glab` are unavailable; run them separately after switching worktrees.
- Host Git configuration, credential helpers, SSH keys and signed commits are unavailable. Use repository-local or snap-local Git settings; perform authenticated remote operations with your host Git.
- Repositories under hidden directories directly inside your home are inaccessible. Automatic host shell configuration and agent-plugin installation are unsupported; use the shell initialization lines above.
- Bash, Zsh and Fish directory switching use a shared temporary directory in the snap's user data. Nushell and PowerShell integration are not adapted for confinement.

## Build

```bash
git clone https://github.com/sidalit/worktrunk-snap.git
cd worktrunk-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/worktrunk-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/max-sixty/worktrunk/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/worktrunk-snap/blob/main/LICENSE).
