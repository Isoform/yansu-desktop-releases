# R2 Upload Configuration

Required GitHub Secrets for uploading releases to Cloudflare R2.

## Required Secrets

| Secret Name | Description | Example Value |
|-------------|-------------|---------------|
| `R2_ACCESS_KEY_ID` | Cloudflare R2 API Token Access Key ID | `abc123...` |
| `R2_SECRET_ACCESS_KEY` | Cloudflare R2 API Token Secret Key | `xyz789...` |
| `R2_ENDPOINT` | R2 S3-compatible API endpoint | `https://<account-id>.r2.cloudflarestorage.com` |
| `R2_BUCKET` | R2 bucket name | `yansu-desktop-releases` |
| `R2_PUBLIC_URL` | Public URL for R2 bucket (used in version.json URLs) | `https://pub-xxx.r2.dev` or custom domain |

## R2 Setup Steps

### 1. Create R2 Bucket

1. Cloudflare Dashboard → R2 → Create Bucket
2. Name: `yansu-desktop-releases`

### 2. Enable Public Access

1. Select the bucket → Settings → Public Access → Allow Access
2. Copy the public bucket URL (format: `https://pub-<id>.r2.dev`)

### 3. Create API Token

1. R2 → Manage R2 API Tokens → Create API Token
2. Permissions: **Object Read & Write**
3. Apply to specific bucket: `yansu-desktop-releases`
4. Copy the Access Key ID and Secret Access Key

### 4. Find R2 Endpoint

```
https://<account-id>.r2.cloudflarestorage.com
```

Account ID is in: Cloudflare Dashboard → R2 → Overview

## R2 Directory Structure

```
bucket/
├── version.json                           ← Always points to latest version
└── releases/
    └── v0.1.35/
        ├── Yansu-darwin-arm64.app.tar.gz
        ├── Yansu-darwin-arm64.gz
        ├── Yansu-darwin-amd64.app.tar.gz
        ├── Yansu-darwin-amd64.gz
        ├── Yansu-linux-amd64.gz
        └── Yansu-windows-amd64.gz
```

## version.json Format

```json
{
  "version": "0.1.35",
  "release_notes": "Bug fixes and improvements.",
  "assets": {
    "darwin-arm64": "https://pub-xxx.r2.dev/releases/v0.1.35/Yansu-darwin-arm64.app.tar.gz",
    "darwin-amd64": "https://pub-xxx.r2.dev/releases/v0.1.35/Yansu-darwin-amd64.app.tar.gz",
    "linux-amd64": "https://pub-xxx.r2.dev/releases/v0.1.35/Yansu-linux-amd64.gz",
    "windows-amd64": "https://pub-xxx.r2.dev/releases/v0.1.35/Yansu-windows-amd64.gz"
  }
}
```
