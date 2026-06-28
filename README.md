# Noctiri Drift &nbsp; [![build badge](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml/badge.svg)](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml)

A Fedora Atomic custom image combining the [Niri](https://niri-wm.github.io/niri/) compositor and the [Noctalia](https://noctalia.dev) shell.

**Base:** Fedora Atomic ([Universal Blue](https://universal-blue.org/) `base-main`)

**Key packages:**
- [niri](https://niri-wm.github.io/niri/) — scrollable-tiling Wayland compositor
- [noctalia-shell](https://noctalia.dev) — desktop shell for Niri
- [greetd](https://sr.ht/~kennylevinsen/greetd/) + [tuigreet](https://github.com/apognu/tuigreet) — login manager

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- Rebase to the image:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/lofidevops/noctiri-drift:latest
  ```
- Reboot to complete the installation:
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## Verification

> [!NOTE]
> Image signing is not yet enabled but is planned for a future release.


