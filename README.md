# Yansu Desktop

Release artifacts for **Yansu Desktop** — a native macOS and Linux IDE client powered by AI agents.

## Download

Go to [**Releases**](https://github.com/Isoform/yansu-desktop-releases/releases/latest) to grab the latest version.

| Platform | File | Use |
|----------|------|-----|
| macOS (Apple Silicon) | `Yansu-darwin-arm64.dmg` | First install |
| macOS (Intel) | `Yansu-darwin-amd64.dmg` | First install |
| Linux (amd64) | `Yansu-linux-amd64.gz` | See below |

> **Windows** support is in progress.

## Installation

### macOS

1. Download the `.dmg` matching your chip (arm64 = Apple Silicon, amd64 = Intel)
2. Open the `.dmg` and drag **Yansu.app** to your Applications folder
3. Launch Yansu — the app manages its own updates from this point on

> The app is ad-hoc signed. If macOS blocks it on first launch:  
> **System Settings → Privacy & Security → Open Anyway**

### Linux

```bash
# Download
curl -L https://github.com/Isoform/yansu-desktop-releases/releases/latest/download/Yansu-linux-amd64.gz -o Yansu.gz

# Extract and make executable
gunzip Yansu.gz
chmod +x Yansu

# Run
./Yansu
```

## Auto-Updates

Yansu checks this repository's `releases/latest` endpoint on startup. When a new version is available, it downloads the appropriate `.gz` binary and applies the update in-place. No manual intervention needed after the initial install.

## Verifying Downloads

Each release includes a `checksums.txt` with SHA-256 hashes for all artifacts.

```bash
# Verify a downloaded file
sha256sum -c checksums.txt --ignore-missing
```

## Release Pipeline

Releases are built automatically via GitHub Actions on macOS (arm64 + amd64) and Linux (amd64). The pipeline:

- Builds the Wails GUI app from source
- Bundles the ACP (Agent Control Protocol) runtime
- Ad-hoc signs the macOS `.app`
- Packages `.dmg` (installer) and `.gz` (auto-update binary) for each platform
- Generates SHA-256 checksums

Triggering a release:

```bash
# Via workflow_dispatch (GitHub UI → Actions → Release Yansu Desktop → Run workflow)
# Or via repository_dispatch:
gh api repos/Isoform/yansu-desktop-releases/dispatches \
  -f event_type=release \
  -f client_payload='{"version":"v0.13.0"}'
```

## Required Secrets

| Secret | Description |
|--------|-------------|
| `SOURCE_REPO_TOKEN` | PAT with read access to `Isoform/something` and `Isoform/claude-code-acp` |
