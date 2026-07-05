# xc-vod-manager

A self-hosted manager for an [Xtream Codes](https://en.wikipedia.org/wiki/Xtream_Codes) box. It imports movies from M3U playlists, enriches them with metadata from TMDB and ThePornDB, streams URL-based VODs through Xtream Codes, and lets you manage all of it from a web dashboard.

## Install

Run this as **root / sudo on the Xtream Codes box**:

```sh
curl -fsSL https://github.com/wisem2540/xc-vod-manager-releases/releases/latest/download/xc-vod-manager.tar.gz -o /tmp/xcvm.tgz
mkdir -p /tmp/xcvm && tar -xzf /tmp/xcvm.tgz -C /tmp/xcvm --strip-components=1
cd /tmp/xcvm && sudo sh ./install/install.sh
```

## What the installer does

- **Auto-detects** your existing Xtream Codes install (and its bundled PHP).
- Creates a **locked-down, non-root service user** to run the app.
- Installs the **app and web dashboard** — defaults to port **8090**, and prints a randomly generated dashboard password **once** on first install.
- Prompts once for an **existing XC admin** so it can create a **least-privilege importer account** for its own use (those admin credentials are **not stored**).
- Applies the **relay patch** to Xtream Codes so URL-based VODs stream through XC, keeping a **timestamped backup** of the original file.

The installer is idempotent — it is safe to re-run to upgrade, and it never clobbers your settings or the dashboard password.

## Requirements

- An **Xtream Codes** box running **Ubuntu / Debian** (systemd).
- **root / sudo** access.
- **Outbound internet** access (for release downloads and metadata lookups).

## After installing

1. Open **`http://YOUR-BOX-IP:8090/`** in a browser.
2. Log in with username **`admin`** and the password printed by the installer.
3. Add your first M3U playlist under **Sources**, then import.

## Updating

- **In-place from the dashboard:** use the **Update** tab, which checks this release channel and upgrades in place.
- **Or re-run the install command** at the top of this page — it upgrades over an existing install without losing your settings.

## Uninstall

```sh
sudo /tmp/xcvm/install/uninstall.sh
```

Add `--purge` to also remove the app config, panel secret, and service user:

```sh
sudo /tmp/xcvm/install/uninstall.sh --purge
```

---

*This repository hosts **releases only**. The source is maintained privately.*
