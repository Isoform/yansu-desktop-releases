# Yansu Desktop

A native macOS, Windows, and Linux desktop client for Yansu.

## Download

Go to [**Releases**](https://github.com/Isoform/yansu-desktop-releases/releases/latest) and pick the file that matches your OS and CPU. Filenames are versioned, e.g. `Yansu-0.1.33-darwin-arm64.dmg`.

| Platform | CPU | File |
|----------|-----|------|
| macOS | Apple Silicon | `Yansu-<version>-darwin-arm64.dmg` |
| macOS | Intel | `Yansu-<version>-darwin-x64.dmg` |
| Windows | x64 | `Yansu-<version>-windows-x64.zip` |
| Linux | x64 | `Yansu-<version>-linux-x64.tar.gz` |
| Linux | arm64 | `Yansu-<version>-linux-arm64.tar.gz` |

After installation, Yansu checks for updates ~3 seconds after launch and then every 30 minutes; new versions are applied in-place and the app restarts automatically.

## Installation

### macOS

1. Download the `.dmg` matching your chip (`arm64` for Apple Silicon, `x64` for Intel).
2. Open the `.dmg` and drag **Yansu.app** to **Applications**.
3. Launch Yansu from Applications or Spotlight.

> If macOS blocks the app on first open with a "cannot be opened" warning:
> **System Settings → Privacy & Security → Open Anyway**.

### Windows

The Windows release is shipped as a `.zip` because the app needs the bundled DLLs (sherpa-onnx) and helper binaries (quick-chat-spotlight, bun, ffmpeg, git, rtk, yansu-cli) to sit next to `Yansu.exe`. **Do not run `Yansu.exe` directly from inside the zip** — Windows extracts it to a temp folder without the siblings and you'll get a `sherpa-onnx-c-api.dll was not found` error.

1. Download `Yansu-<version>-windows-x64.zip`.
2. Right-click → **Extract All…** to a permanent location such as `C:\Program Files\Yansu\` or `%LOCALAPPDATA%\Yansu\`.
3. Open the extracted folder and run **Yansu.exe**.
4. Optional: right-click `Yansu.exe` → **Pin to Start** / **Create shortcut → Send to → Desktop**.

### Linux

The Linux release is a `.tar.gz` containing the `Yansu` binary plus its runtime bundles. Extract the whole archive and run from the extracted directory — the binary expects its siblings (`bun-bundle/`, `ffmpeg-bundle/`, etc.) to be in the same folder.

```bash
# x64
curl -L -o Yansu.tar.gz \
  https://github.com/Isoform/yansu-desktop-releases/releases/latest/download/Yansu-<version>-linux-x64.tar.gz

# or arm64
curl -L -o Yansu.tar.gz \
  https://github.com/Isoform/yansu-desktop-releases/releases/latest/download/Yansu-<version>-linux-arm64.tar.gz

mkdir -p ~/yansu && tar -xzf Yansu.tar.gz -C ~/yansu
~/yansu/Yansu
```

Replace `<version>` with the version from the release page (e.g. `0.1.33`).

## Verifying Downloads

Each release includes a `checksums.txt` with SHA-256 hashes of every artifact.

```bash
sha256sum -c checksums.txt --ignore-missing
```

On macOS use `shasum -a 256 -c checksums.txt --ignore-missing`; on Windows, `certutil -hashfile <file> SHA256` and compare manually.

## Auto-Update

Yansu pulls its update manifest from `https://release.yansu.app/version.json`, which lists the latest version and a SHA-256-verified archive URL per platform. Updates are extracted into a `.yansu-update-*` temp directory next to the running executable and applied via per-file atomic rename, so a failed download or partial extraction leaves your installation on the prior version rather than half-upgraded.

## Reporting Issues

Bugs or feature requests: open an issue at [Isoform/yansu-desktop-releases/issues](https://github.com/Isoform/yansu-desktop-releases/issues).
