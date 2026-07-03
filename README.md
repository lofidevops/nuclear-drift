# Noctiri Drift &nbsp; [![build badge](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml/badge.svg)](https://github.com/lofidevops/noctiri-drift/actions/workflows/build.yml)

A Fedora Atomic custom image combining the [Niri](https://niri-wm.github.io/niri/) compositor and the [Noctalia](https://noctalia.dev) shell.

**Base:** Fedora Atomic ([Universal Blue](https://universal-blue.org/) `base-main`)

**Key packages:**
- [niri](https://niri-wm.github.io/niri/) — scrollable-tiling Wayland compositor
- [noctalia-shell](https://noctalia.dev) — desktop shell for Niri
- [greetd](https://sr.ht/~kennylevinsen/greetd/) + [tuigreet](https://github.com/apognu/tuigreet) — login prompt that launches the Niri/Noctalia session directly

## Preview

To preview Noctiri Drift without touching bare metal, you can run it inside a virtual machine:

1. **Install GNOME Boxes** on your host machine.
2. **Create a new virtual machine** using Fedora Silverblue (or any Fedora Atomic desktop).
3. **Complete the Fedora install** inside the VM and log into the stock system once.

Once you have a working Fedora Atomic VM, you're ready to rebase it to Noctiri Drift with the installation instructions below.

## Install

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

You can follow these same steps on a VM or a physical machine; the only difference is where you installed Fedora Atomic.

1. **Install Fedora Silverblue** (or any Fedora Atomic desktop) by following the preview instructions above or <a href="https://docs.fedoraproject.org/en-US/atomic-desktops/installation/">hardware instructions</a>.

2. **Open a terminal and update the system** (optional but recommended)

   ```sh
   rpm-ostree upgrade
   sudo systemctl reboot
   ```

   This puts your base system on the latest update before you switch to Noctiri Drift.

3. **Validate access to the Noctiri Drift image**

   First, confirm that the image is reachable and readable from your machine:

   ```sh
   skopeo inspect --config docker://ghcr.io/lofidevops/noctiri-drift:latest
   ```

   - If this command succeeds, you know:
     - The image exists at that URL.
     - Your network and registry access to GitHub Container Registry are working.
   - If it fails, fix authentication or network issues before proceeding.

4. **Rebase from Silverblue to Noctiri Drift**

   In the same terminal:

   ```sh
   rpm-ostree rebase ostree-unverified-registry:ghcr.io/lofidevops/noctiri-drift:latest
   ```

   This tells Fedora's atomic system to:

   - Pull the Noctiri Drift image from `ghcr.io`.
   - Unpack it into an ostree deployment.
   - Set that deployment as the next root filesystem.

5. **Reboot into Noctiri Drift**

   Once the rebase completes:

   ```sh
   sudo systemctl reboot
   ```

   After the reboot, you should be running the Noctiri Drift image. Your login screen and desktop session should now be provided by Noctiri Drift instead of stock Silverblue.

## Update

To update your system:

```
rpm-ostree upgrade
sudo systemctl reboot
```

## Troubleshooting

If the rebase fails or you want to double‑check that the container image is valid, you can test it with Podman (or Docker):

```sh
podman pull ghcr.io/lofidevops/noctiri-drift:latest
# or docker pull ghcr.io/lofidevops/noctiri-drift:latest
```

This:

- Verifies that your machine can pull the **full image** from GitHub Container Registry.
- Confirms that the OCI image is structurally sound.

If `podman pull` or `docker pull` fails, fix that first. It usually means:

- Network problems,
- GHCR authentication issues, or
- A problem with the image itself.

Once `skopeo inspect` and `podman pull` both work, any remaining errors from `rpm-ostree rebase` are almost certainly in the rpm‑ostree/ostree tooling itself rather than access to Noctiri Drift.

## Verification

> [!NOTE]
> Image signing is not yet enabled but is planned for a future release.
