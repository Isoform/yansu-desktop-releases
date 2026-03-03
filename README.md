# Yansu Desktop

A native macOS, Linux, and Windows desktop client for Yansu.

## Download

Go to [**Releases**](https://github.com/Isoform/yansu-desktop-releases/releases/latest) to download the latest version.

| Platform | File |
|----------|------|
| macOS (Apple Silicon) | `Yansu-darwin-arm64.dmg` |
| macOS (Intel) | `Yansu-darwin-amd64.dmg` |
| Linux (amd64) | `Yansu-linux-amd64.gz` |
| Windows (amd64) | `Yansu-windows-amd64.exe` |

## Installation

### macOS

1. Download the `.dmg` for your chip (arm64 = Apple Silicon, amd64 = Intel)
2. Open the `.dmg` and drag **Yansu.app** to Applications
3. The app updates itself automatically after first launch

> If macOS blocks the app on first open:  
> **System Settings → Privacy & Security → Open Anyway**

### Windows

1. Download `Yansu-windows-amd64.exe` from the latest release
2. Run the `.exe` — no installation required
3. The app updates itself automatically after first launch

### Linux

```bash
curl -L https://github.com/Isoform/yansu-desktop-releases/releases/latest/download/Yansu-linux-amd64.gz -o Yansu.gz
gunzip Yansu.gz
chmod +x Yansu
./Yansu
```

## Verifying Downloads

Each release includes a `checksums.txt` with SHA-256 hashes.

```bash
sha256sum -c checksums.txt --ignore-missing
```
