# R2 Upload Configuration

This document describes the required GitHub Secrets for uploading releases to Cloudflare R2.

## Required Secrets

Add the following secrets to the `Isoform/yansu-desktop-releases` repository:

### R2 Authentication

| Secret Name | Description | Example Value |
|-------------|-------------|---------------|
| `R2_ACCESS_KEY_ID` | Cloudflare R2 API Token Access Key ID | `abc123...` |
| `R2_SECRET_ACCESS_KEY` | Cloudflare R2 API Token Secret Key | `xyz789...` |
| `R2_ENDPOINT` | R2 S3-compatible API endpoint | `https://<account-id>.r2.cloudflarestorage.com` |
| `R2_BUCKET` | R2 bucket name | `yansu-desktop-releases` |
| `R2_PUBLIC_URL` | Public URL for R2 bucket (for version.json URLs) | `https://pub-xxx.r2.dev` or custom domain |

## Setting up R2

### 1. Create R2 Bucket

1. Go to Cloudflare Dashboard → R2 → Create Bucket
2. Name: `yansu-desktop-releases`
3. Location: Automatic (or choose a region)

### 2. Enable Public Access

1. Select the bucket → Settings → Public Access
2. Click "Allow Access"
3. Copy the public bucket URL (format: `https://pub-<id>.r2.dev`)
4. (Optional) Configure custom domain for better branding

### 3. Create API Token

1. Go to R2 → Manage R2 API Tokens → Create API Token
2. Permissions: **Object Read & Write**
3. Apply to specific bucket: `yansu-desktop-releases`
4. Copy the **Access Key ID** and **Secret Access Key** (shown only once)

### 4. Find R2 Endpoint

The endpoint URL format is:
```
https://<account-id>.r2.cloudflarestorage.com
```

You can find your account ID in:
- Cloudflare Dashboard → R2 → Overview → Account ID

## R2 Directory Structure

After the pipeline runs, the R2 bucket will have this structure:

```
yansu-desktop-releases/
├── version.json                                    ← Always points to latest version
└── releases/
    ├── v0.1.35/
    │   ├── Yansu-darwin-arm64.app.tar.gz
    │   ├── Yansu-darwin-arm64.gz
    │   ├── Yansu-darwin-amd64.app.tar.gz
    │   ├── Yansu-darwin-amd64.gz
    │   ├── Yansu-linux-amd64.gz
    │   └── Yansu-windows-amd64.gz
    └── v0.1.36/
        └── ...
```

## version.json Format

The root `version.json` manifest contains:

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

## Testing

To verify the R2 upload works:

1. Add the secrets to the repository
2. Trigger a workflow manually via GitHub Actions → "Release Yansu Desktop" → Run workflow
3. Check the R2 bucket after the workflow completes
4. Verify `version.json` is accessible at: `https://pub-xxx.r2.dev/version.json`

## Troubleshooting

### Upload fails with "Access Denied"

- Verify the API token has **Object Read & Write** permissions
- Ensure the token is applied to the correct bucket

### version.json URLs are wrong

- Check that `R2_PUBLIC_URL` secret matches your public bucket URL
- If using a custom domain, make sure it's properly configured in R2 settings

### Files not accessible after upload

- Ensure the bucket has **Public Access** enabled
- Check bucket CORS settings if accessing from web apps
